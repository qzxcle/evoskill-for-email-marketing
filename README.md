# EvoSkill for email marketing

A worked example of using [EvoSkill](https://github.com/sentient-agi/EvoSkill) to train a Claude Code skill that writes better marketing emails, by the Sentient team.

**How it works:** Claude gets a short campaign brief and writes an email. A second Claude grades that email against a real email from a top company, written for the same brief. EvoSkill keeps rewriting Claude's skills, round after round, to raise the grade. You then use the trained skill to write your own campaigns.

## What's in this repo

```
evoskill-for-email-marketing/
├── project-template/
│   ├── evoskill-config/
│   │   ├── config.toml        our EvoSkill settings, including the grading rubric
│   │   └── task.md            the task description Claude gets on every email
│   └── knowledge/
│       ├── cold-email-principles.md   our own notes on cold email
│       └── sources.md         the YC and a16z pages we used, as links
├── prompts/
│   ├── 01-build-knowledge.md  fetch the advice into knowledge/
│   ├── 02-collect-examples.md collect real emails for the answer key
│   ├── 03-build-dataset.md    turn them into the CSV EvoSkill trains on
│   └── 04-write-campaign.md   use the trained skill on a real campaign
├── evolved-skill/
│   └── saas-email-anatomy/SKILL.md   the skill EvoSkill wrote in our run
├── templates/
│   └── campaign-brief-template.md    the brief Claude reads before writing
└── results/
    └── run-report.md          our full run: scores, iterations, cost
```

## Our results

| | |
|---|---|
| Dataset | 26 real marketing emails from 6 companies (16 for training, 10 for validation) |
| Model | `claude-sonnet-4-6` |
| Iterations | 10 |
| Score | 76% → 79% |
| Total cost | $57.15 |

With only 10 validation emails, +3 points is about one email graded better, so treat it as a modest gain. The more interesting result is what Claude learned: the evolved skill sorts every brief into an email type (feature announcement, onboarding, welcome, deprecation notice) with its own structure and length, and it decided on its own that our cold-email notes don't fit product updates to existing customers. Full details are in [results/run-report.md](results/run-report.md).

## Which EvoSkill version this uses

We ran this on EvoSkill's `main` branch, commit `36f6f04`: the original loop, where a Proposer and a Generator write the skills and weaker rounds are discarded. EvoSkill v2 (release `v2.0.0`) uses a different architecture and setup, and this template hasn't been tested with it yet.

## What you need

- A Mac. The commands use zsh, `open -e` and `caffeinate`; Linux works with small changes.
- Git and [Claude Code](https://docs.claude.com/en/docs/claude-code/overview).
- An Anthropic API key with a monthly spending limit set in the Anthropic Console. Our run cost $57.15.
- An internet connection for the whole run, which takes a few hours.

## Quick start

### 1. Install EvoSkill

```
mkdir -p ~/Documents/evoskill && cd ~/Documents/evoskill
curl -fsSL https://raw.githubusercontent.com/sentient-agi/EvoSkill/main/install.sh | bash
echo 'export PATH="$HOME/Documents/evoskill/EvoSkill/.venv/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
evoskill --help
```

If you've never used Git on this Mac, also set `git config --global user.name` and `user.email`.

### 2. Create the folders

```
cd ~/Documents/evoskill
mkdir -p email-campaigns/knowledge answer-key/examples
cd email-campaigns
git init
```

`answer-key/` must stay outside the project folder. Claude can read everything inside the project, so if the real emails were in there, it would copy them and score perfectly without learning anything.

### 3. Build the knowledge library

Open Claude Code in `email-campaigns/` and paste [prompts/01-build-knowledge.md](prompts/01-build-knowledge.md). Copy [cold-email-principles.md](project-template/knowledge/cold-email-principles.md) into `knowledge/` too.

### 4. Build the dataset

Open Claude Code in `~/Documents/evoskill` and paste [prompts/02-collect-examples.md](prompts/02-collect-examples.md), then [prompts/03-build-dataset.md](prompts/03-build-dataset.md).

### 5. Set up EvoSkill

```
cd ~/Documents/evoskill/email-campaigns
evoskill init
```

Answer the prompts like this, using your own username in the path:

```
Which agent runtime? › claude
Dataset source? › CSV
Absolute path to dataset CSV? › /Users/YOUR-USERNAME/Documents/evoskill/answer-key/emails.csv
Question/input column name? › question
Answer column name? › ground_truth
Category column name? › category
Additional data directories? › (leave blank)
How do you want to run EvoSkill? › Local
```

Then replace `.evoskill/config.toml` and `.evoskill/task.md` with the two files in [project-template/evoskill-config/](project-template/evoskill-config/), set your dataset path in `config.toml`, and save your setup:

```
git add .
git commit -m "Set up EvoSkill project"
```

### 6. Run it

```
export ANTHROPIC_API_KEY=your-key-here
caffeinate -i evoskill run
```

Set the key only in this terminal window, never in `~/.zshrc` (see the gotchas below).

### 7. Find the winning skill

At the end, look for the line `[DONE] 10 iterations, best: iter-skill-N`. Switch to that version and read the skill:

```
git checkout program/iter-skill-N
cat .claude/skills/*/SKILL.md
```

### 8. Write a real campaign

```
git checkout -b campaigns
mkdir -p campaign/drafts
```

Fill in [templates/campaign-brief-template.md](templates/campaign-brief-template.md), save it as `campaign/brief.md`, open Claude Code in a new terminal window (one without the API key set), and paste [prompts/04-write-campaign.md](prompts/04-write-campaign.md).

## Skip the training

To try our evolved skill without running EvoSkill, copy it into any project where you use Claude Code:

```
mkdir -p .claude/skills
cp -R evolved-skill/saas-email-anatomy .claude/skills/
```

It was trained on product emails from a handful of SaaS and AI companies, so its style leans toward theirs.

## Gotchas we hit

- **"Invalid value" error when starting the run:** TextEdit turned the straight quotes in `config.toml` into curly ones. Fix it with `sed -i '' -e 's/“/"/g' -e 's/”/"/g' .evoskill/config.toml`, or turn off Edit → Substitutions → Smart Quotes before editing.
- **Most of your data goes unused by default:** `train_ratio` and `val_ratio` default to 0.18 and 0.12, which use only 30% of your examples. Our config sets them to 0.6 and 0.4.
- **Commit before running:** EvoSkill switches Git branches during the run, which fails in a repository with no commits.
- **Billing:** if `ANTHROPIC_API_KEY` is set, Claude Code uses it instead of your Claude subscription, even when you're logged in. Setting it only in the run's terminal window keeps your everyday Claude Code on your plan. Type `/status` in Claude Code to check.
- **`RuntimeError: Event loop is closed`:** a harmless cleanup warning that may appear after evaluations. The run continues.
- **"No skills yet" after the run:** the project is left on whichever version was tested last. Switch to the winning branch first (step 7).
- **`evoskill diff` may show the wrong version as best:** it picked iteration 8 in our run, while the best was iteration 3. Use the `[DONE]` line instead.
- **Small datasets are noisy:** with 10 validation emails graded 1.0, 0.5 or 0.0, one email changes the score by 5 points.

## What's not included, and why

- **The example emails and the dataset:** they're other companies' email copy. Prompts 02 and 03 rebuild them for you.
- **The full text of the YC and a16z articles:** they belong to their authors. [sources.md](project-template/knowledge/sources.md) lists the links, and prompt 01 fetches them.
- **Our own campaign brief, drafts and send data.**

The evolved skill is published as EvoSkill wrote it, except that we replaced a few examples it had quoted from real company emails with invented ones.

## License

[MIT](LICENSE), by the Sentient team.
