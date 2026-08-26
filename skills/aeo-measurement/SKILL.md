---
name: aeo-measurement
description: Use when measuring AI visibility — setting baselines, running before/after comparisons, choosing prompt sets, or reporting AEO results to a client.
metadata:
  category: technique
  triggers: AI visibility score, baseline, prompt set, before after, AEO reporting, visibility tracking
---

# AEO Measurement

## When to Use
- Starting any engagement (baseline BEFORE touching anything)
- After a launch or major change (the "after" column)
- Building a recurring client report

## Baseline first, always

The before/after comparison is the product. No baseline = no provable result, no
matter how good the work was. Capture it before the first fix ships.

A baseline is a **fixed prompt set** run against the major engines (ChatGPT,
Claude, Perplexity, Gemini/AI Mode, Grok), recording per prompt:

- Was the brand mentioned at all?
- Position/prominence (first recommendation vs afterthought)
- What was said (accurate? stale? confused with another entity?)
- Which competitors appeared
- Which sources were cited

## Building the prompt set

- Mirror real buyer questions, not vanity queries: "best tax accountant in Yuba
  City", "affordable bookkeeper for contractors near Marysville", "should I use
  TurboTax or hire an accountant" — not "tell me about [brand]"
- **Bucket by intent zone** and keep buckets balanced (≥4 prompts per bucket):
  direct-local ("in [city]"), nearby/region, service-specific, persona-specific,
  comparison/alternatives
- Size it to your tooling cap (e.g., a 50-prompt platform cap = one full set), and
  **freeze the set**. Changing prompts between runs destroys comparability — additions
  go in a new bucket scored separately.

## Cadence & expectations

- Re-scan ~1 week after launch, then monthly. Daily checking is noise — LLM answers
  have natural variance.
- Run each prompt fresh (no chat history, no logged-in personalization).
- **Two clocks:** Google indexing moves in days-to-weeks; AI answers move on the
  engines' own refresh schedules. Report them as separate lines so a flat AI score
  a week after launch doesn't read as failure.

## Reporting rules

- Report the score with its composition: "mentioned in 18 of 50 prompts (was 9),
  first-choice in 6 (was 1), zero entity confusion (was 3 prompts confusing us
  with [other brand])"
- Show the exact quotes — clients believe screenshots of ChatGPT saying their name
  more than any chart
- **Never cherry-pick.** If a bucket got worse, show it and diagnose it. One honest
  regression buys more trust than ten highlighted wins.
- Track competitor movement in the same table; "you passed [competitor] in 4
  buckets" is the sentence that renews engagements.
- Attribute honestly: answer variance exists, so claim trends across ≥2 runs, not
  single-run miracles.
