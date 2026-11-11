# 03: Turn the emails into a dataset

**Where to run:** the same Claude Code session as prompt 02.

**What it does:** writes a short brief for each email and saves the dataset EvoSkill trains on.

```
For each file in answer-key/examples/, write a short campaign brief: company, product, audience and the goal of the email, in 2-3 sentences, without copying its wording.

Save answer-key/emails.csv with three columns:
- question: the brief
- ground_truth: the full email text
- category: the company name

Use proper CSV quoting, then tell me how many rows it has.
```

During the run, EvoSkill shows Claude only the brief. Claude writes its own email, and the grader compares it with the real one using the rubric in `config.toml`.
