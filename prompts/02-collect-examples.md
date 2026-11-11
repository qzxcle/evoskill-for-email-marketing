# 02: Collect example emails

**Where to run:** Claude Code, started one folder up (`~/Documents/evoskill`), so it can reach `answer-key/`.

**What it does:** collects real emails from companies whose style you like. These become the answer key the grader compares against, so they must stay outside the project folder.

```
Find real marketing emails from these companies: OpenAI, Anthropic, Mistral AI, Proton, Linear, Stripe, Notion and Vercel.

Search email galleries like reallygoodemails.com, milled.com and emaillove.com.

Pick the 5 best emails per company: product launches, announcements, onboarding and newsletters. Save each email's text as a .txt file in answer-key/examples/, named company-short-title.txt, with the subject line on the first line. Skip any email whose text you can't read.
```

Swap in any companies you like. Your own past campaigns that performed well are an even better source.

In our run, Claude Code found 26 usable emails; it couldn't find any for Mistral AI or Proton.
