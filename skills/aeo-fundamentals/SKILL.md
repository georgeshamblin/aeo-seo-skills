---
name: aeo-fundamentals
description: Use when working on AI visibility — a brand wants to show up in ChatGPT, Claude, Perplexity, Gemini, or Google AI Mode answers, or asks why competitors get recommended instead of them.
metadata:
  category: technique
  triggers: AEO, AI visibility, answer engine, ChatGPT recommendations, Perplexity, AI Mode, GEO
---

# AEO Fundamentals

## When to Use
- "Why doesn't ChatGPT recommend us?"
- Planning any AI-visibility engagement or audit
- Deciding where effort goes: site fixes vs content vs citations

## How answer engines pick brands

AI assistants answer "best X in Y" questions from three inputs, roughly in this order:

1. **Retrieval** — live web search (Perplexity, ChatGPT search, Google AI Mode) pulls
   pages that answer the question. If your site is invisible to crawlers or has no
   answer-shaped page, you cannot be retrieved.
2. **Citations** — engines lean heavily on third-party sources: directories, "best of"
   lists, review sites, local news, industry associations. A brand mentioned in three
   independent sources beats a brand only describing itself.
3. **Entity clarity** — the model must know *what you are*: exact name, category,
   location, services. Ambiguity (two brands with similar names, inconsistent NAP,
   thin homepage) reads as risk and gets skipped.

## The work, in priority order

| Priority | Work | Skill |
|---|---|---|
| 1 | Crawler access — nothing else matters if bots are blocked | ai-crawler-access |
| 2 | Entity clarity — schema, llms.txt, consistent NAP | structured-data-json-ld, writing-llms-txt, local-seo |
| 3 | Answer-shaped pages for the questions buyers ask | answer-shaped-content |
| 4 | Third-party citations | citations-and-mentions |
| 5 | Measurement — baseline before, re-scan after | aeo-measurement |

## Rules

- **AEO is built on SEO.** A site failing the technical-seo-audit skill will not win in
  AI answers by adding llms.txt on top. Fix the crawl layer first.
- **Never fabricate signals.** No fake reviews, invented awards, or fictional "as seen
  in" logos. Engines cross-check sources, and regulated professions face real liability.
- **Specificity beats volume.** One page that fully answers "tax accountant in
  Marysville CA" outranks ten thin pages, in both Google and AI answers.
- **Two clocks run independently.** Google indexing (days to weeks) and AI-assistant
  visibility (retrained/refreshed on their own schedules) don't move together. Set
  that expectation with clients up front.
