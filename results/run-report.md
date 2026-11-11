# EvoSkill run report

Our run from November 2026, as printed by EvoSkill at the end of `evoskill run`.

## Setup

| | |
|---|---|
| EvoSkill version | `main` branch, commit `36f6f04` (Proposer + Generator loop) |
| Agent runtime | Claude Code |
| Model | `claude-sonnet-4-6` (agent and grader) |
| Dataset | 26 real marketing emails from 6 companies: 16 for training, 10 for validation |
| Grading | LLM rubric (see `project-template/evoskill-config/config.toml`) |
| Iterations | 10 |

## Summary

| | |
|---|---|
| Baseline | 76.0% |
| Final | 79.0% |
| Improvement | +3.0 points |
| Skills kept | 4 of 10 proposed |
| Best program | `iter-skill-3` |
| Total cost | $57.15 |

## Iteration log

| Iter | Accuracy | Δ | Skills | Status |
|------|----------|---|--------|--------|
| 0 | 76.0% | — | 0 | baseline |
| 1 | 71.0% | -5.0% | 1 | kept |
| 2 | 72.0% | +1.0% | 1 | kept |
| 3 | 79.0% | +7.0% | 1 | ★ new best |
| 4 | 67.0% | -12.0% | 0 | discarded |
| 5 | 67.0% | +0.0% | 0 | discarded |
| 6 | 63.0% | -4.0% | 0 | discarded |
| 7 | 66.0% | +3.0% | 0 | discarded |
| 8 | 76.0% | +10.0% | 1 | kept |
| 9 | 76.0% | +0.0% | 0 | discarded |
| 10 | 71.0% | -5.0% | 0 | discarded |

Δ compares each iteration with the previous one, not with the baseline.

## Skills

All four kept versions are edits of a single skill, `saas-email-anatomy`:

| Version | Change | Accuracy impact |
|---|---|---|
| Iteration 1 | Created | -5.0% |
| Iteration 2 | Edited | +1.0% |
| Iteration 3 | Edited | +7.0% (best overall) |
| Iteration 8 | Edited | +10.0% vs. previous iteration |

The iteration 3 version is in `evolved-skill/saas-email-anatomy/SKILL.md`.

## How to read this

- The validation set is small: 10 emails graded 1.0, 0.5 or 0.0. One email moving from 1.0 to 0.5 shifts the score by 5 points, so +3 points is about one email graded better. Treat it as a modest gain.
- The more interesting result is what the skill learned: it classifies each email by type before writing, and it overrides our cold-email notes for product updates to existing customers.
- A harmless `RuntimeError: Event loop is closed` traceback appeared after several evaluations. It doesn't affect the run.
