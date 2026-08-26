---
name: writing-llms-txt
description: Use when creating or editing an llms.txt file, or when a site needs a machine-readable summary for AI crawlers.
metadata:
  category: technique
  triggers: llms.txt, llms-full.txt, AI summary file, machine-readable site summary
---

# Writing llms.txt

## When to Use
- Adding `llms.txt` to any site
- Reviewing an existing one that reads like marketing copy
- After any change to services, locations, or contact details (it must stay in sync)

## Format

`llms.txt` lives at the site root (`https://example.com/llms.txt`), served as plain
text/markdown. Structure:

```markdown
# Brand Name

> One-paragraph factual summary: what the business is, what it does, where it is,
> who it serves. Written for a machine deciding whether to recommend you.

Two to four sentences of expansion: service lines, customer types, service area,
anything that disambiguates you from similarly named businesses.

## Pages

- [Home](https://example.com/): what's on it
- [Service page](https://example.com/service.html): what's on it

## Contact

- Phone: +1-555-555-5555
- Email: hello@example.com
- Address: 123 Main St, City, ST 12345
```

## Rules

- **Facts only.** No slogans, no "award-winning" without a named award, no
  superlatives. An LLM summarizing your site rewards density, not enthusiasm.
- **Disambiguate.** If the brand name is confusable with another company, say
  explicitly what you are NOT ("an independent accounting firm, not affiliated
  with X").
- **Match the site.** Every fact in llms.txt must appear on a real page and agree
  with the JSON-LD. Three sources of truth (page, schema, llms.txt) must never
  disagree — engines notice, and disagreement reads as unreliability.
- **List every indexable page** with a one-line description. Don't list noindexed or
  utility pages (thank-you, 404).
- **Keep it under ~2,000 words.** It's a summary, not a mirror. For large sites, link
  to an `llms-full.txt` with per-page detail rather than bloating the main file.
- **Update it in the same commit** as any NAP, service, or page change. A stale
  llms.txt is worse than none — it actively feeds wrong facts to engines.

## Verify

```bash
curl -s https://example.com/llms.txt | head -20
```

Confirm: 200 status, plain text (not an HTML 404 page), and the phone/address match
the site footer exactly.
