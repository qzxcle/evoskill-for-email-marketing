---
name: saas-email-anatomy
description: REQUIRED before writing any SaaS marketing email — feature launches, product updates, onboarding, deprecation notices, or welcome emails. Invoke this skill BEFORE reading knowledge files or writing any copy.
compatibility: opencode
---

## Knowledge file conflict notice

The `cold-email-principles.md` file teaches cold outreach rules (100–140 words, one CTA, tagline subject lines). These rules apply ONLY to prospecting emails sent to strangers. They are WRONG for Feature Announcement and product update emails sent to existing customers. When the email type is Feature Announcement, the following overrides apply:

- **Word count**: 300–1200+ words depending on feature count (NOT 100–140 words)
- **CTAs**: one per major feature section (NOT one at the end)
- **Subject line**: simple factual descriptor or version number (NOT a clever tagline)
- **Sign-off**: required, with a real name (NOT omitted)

---

## Email type classification

Identify the email type before writing. Each type has distinct structure rules.

### 1. Feature Announcement (product update to existing customers)

Used when shipping new functionality to users who already have accounts.

**Subject line**: Use the simplest possible factual descriptor. For versioned releases: "Acme 2.4" or "2.4: Acme Developer Platform" (product name + version, or version colon descriptive name). For unversioned launches: a brief noun phrase ("Acme Developer Platform"). NEVER write a marketing tagline ("Less clicking, more doing" ✗, "What's new in Acme" ✗). The subject should read like a changelog heading, not an ad.

**Top-level structure**:
1. Greeting (Dear / Hey / Hi [first name or audience label])
2. Opening hook — 1–3 sentences establishing what shipped and why it matters
3. Feature sections (one per major feature)
4. Secondary features section (for large launches, see below)
5. Closing / sign-off with real name and title
6. P.S. lines (optional, see below)

**Per-section structure** (repeat for each major feature):
1. Feature heading (bold or headline style)
2. 2–5 sentence description — what it does, why it matters, concrete benefit
3. Customer quote (if available): embed immediately after the description, before the CTA. Format: quote text in italic or plain, attribution on the next line as "Name / Title at Company". Do NOT collect quotes at the bottom of the email. Each quote must be specific to the feature it accompanies.
4. CTA button or link ("Try it →", "Learn more", "Read the docs")

**Secondary features section**: Large platform launches with 6+ features commonly include a final "More updates" or "What else shipped" section covering smaller changes as a bulleted list (1 line each, no individual CTAs). Structure: bold feature name + one-sentence description. This avoids bloating the email with full sections for minor updates while still surfacing them.

Example:
```
More updates you'll love

**Bulk export**: Download any project as a CSV in one click.
**Webhooks**: Now fire on comment edits and deletions.
**Admin console**: Workspace settings now live on one dedicated page.
```

**Content depth scaling by feature count**:
- 1–2 features: 200–400 words
- 3–4 features: 400–700 words
- 5–7 features (platform launch): 700–1200 words
- 8+ features with secondary section: 1000–1500 words

**Multiple P.S. lines**: For large platform launches, stacking P.S. / P.P.S. / P.P.P.S. lines is acceptable and common. Use them for: event announcements, behind-the-scenes notes, unrelated minor updates (e.g., "P.P.P.S. One more thing: dark mode is here.").

---

### 2. Onboarding email

Sent to new signups to drive activation toward a first meaningful action.

**Structure**:
1. Greeting with first name
2. Welcome statement (1–2 sentences)
3. Single primary action with clear CTA
4. 2–4 supporting tips or next steps (bullet list or short sections)
5. Offer of help (reply / support link)
6. Sign-off with real name

**Tone**: Warm, encouraging, low pressure. Word count: 150–300 words.

---

### 3. Welcome email (post-signup confirmation)

Sent immediately on account creation. Purpose: confirm the signup, set expectations, deliver first value.

**Structure**:
1. Subject: "Welcome to [Product]" or "You're in"
2. Opening: acknowledge the signup
3. What to do next — one clear first step
4. Brief value reminder (what they'll get)
5. Sign-off

**Word count**: 100–200 words. One CTA only.

---

### 4. Deprecation / sunset notice

**Structure**:
1. Subject: factual, specific ("[Feature] is being deprecated on [date]")
2. What is changing and when (exact date)
3. Why (brief — users deserve a reason)
4. What to do instead (migration path)
5. Support offer
6. Sign-off

**Tone**: Direct, respectful, no euphemisms. No marketing language.

---

## Universal anatomy elements (all types)

- **Greeting**: Always present. Use first name when available. Never skip.
- **Sign-off**: Always present. Real name + title. Never omit.
- **Sender identity**: Make clear who is writing (person name, role, company).
- **Unsubscribe / legal footer**: Required for bulk sends.
- **Plain text fallback**: Write as if images may not load.

---

## Anti-patterns to avoid

| Anti-pattern | Why it fails |
|---|---|
| Opening with "I" | Weak; center the reader, not the sender |
| Subject line as tagline | Sounds like spam; reduces opens |
| One CTA for a 5-feature email | Buries the most relevant action per reader |
| Cold-email brevity (100–140 words) for product updates | Leaves out context users need to act |
| Quotes collected at the bottom | Loses the specificity that makes them persuasive |
| Missing greeting | Impersonal; signals automation |
| Missing sign-off | Feels truncated; erodes trust |
