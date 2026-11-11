# 04: Write a real campaign with the trained skill

**Where to run:** Claude Code, started inside your project folder, on the branch with the winning skill. Use a terminal window where `ANTHROPIC_API_KEY` is not set, so this runs on your Claude plan.

**Before you start:** fill in `templates/campaign-brief-template.md` and save it as `campaign/brief.md`. If you have a source document with the facts (a paper, a spec, a launch post), put it in `campaign/` too.

```
Read campaign/brief.md and use the saas-email-anatomy skill and the guides in knowledge/.

Write [NUMBER] versions of a [TYPE OF EMAIL] for [PRODUCT]: [LIST THE VERSIONS AND WHO EACH IS FOR], as described in the brief. [SAY WHETHER READERS ALREADY USE THE PRODUCT. If they don't: "Most readers don't use the product yet, so treat this as prospecting, not a product update to existing customers."] Match the style of the reference email in the brief.

Use only facts from the brief. If you're unsure about a number, check it in the source documents in campaign/.

Save each version with its subject line and preview text in campaign/drafts/.
```

The prospecting line matters. The skill learned mostly from product updates to existing customers, which tend to be long. Telling it this is cold outreach points it to the short-email rules instead.

Then refine in plain language, for example:

```
Make the second version shorter and more direct.
Give me three other subject lines for the first version.
```
