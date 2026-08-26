---
name: answer-shaped-content
description: Use when writing content meant to be cited or lifted by AI assistants — FAQs, comparison pages, pricing explanations, definition sections.
metadata:
  category: technique
  triggers: FAQ, answer engine content, comparison page, featured snippet, AI citations, content strategy
---

# Answer-Shaped Content

## When to Use
- Planning the content backlog for an AEO engagement
- Writing FAQ, pricing, comparison, or "what is X" content
- A page ranks but never gets cited in AI answers

## The shape engines can lift

Retrieval-augmented engines quote self-contained units: a question heading plus a
direct answer in the first sentence or two. Structure every answerable topic as:

```markdown
## How much does tax preparation cost in Yuba City?

Individual returns typically run $250 to $500 depending on complexity; business
returns start around $600. [2–4 sentences of honest nuance follow.]
```

- **Answer first, qualify second.** The first sentence must stand alone when quoted
  out of context — because it will be.
- Numbers, ranges, and concrete nouns get cited; "it depends, contact us" does not.
  If exact prices are impossible, give a truthful range and say what moves it.
- Mirror the FAQ in `FAQPage` JSON-LD with **identical text** (see
  structured-data-json-ld).

## The page types that win AI answers

| Page | Target question | Notes |
|---|---|---|
| Pricing / cost | "how much does X cost" | Highest-intent, least-supplied answer on the web |
| Comparison | "X vs Y", "alternative to Y" | Compare honestly against DIY/software/big brands; concede what the alternative does well — engines and readers both reward it |
| "Best X in [city]" support | "best [service] near me" | You can't crown yourself; publish the criteria a buyer should use, then be citable on each criterion |
| Definition / process | "what is X", "how does X work" | Establishes topical authority; internal-links to the service page |
| Persona FAQ | "[service] for [audience]" | e.g., self-employed, contractors, farms — specificity is the moat |

## Rules

- One question = one heading = one liftable block. Never bury three answers in one
  paragraph.
- Write at the reader's vocabulary, define jargon on first use — LLMs preferentially
  quote clear explanations over expert shorthand.
- Update dated facts (prices, laws, deadlines) on a schedule and show a "last
  updated" date near volatile content.
- **Truth is the strategy.** An engine that quotes your page to a user who then finds
  the claim false burns the citation permanently. Never let AI drafting invent
  statistics, credentials, or testimonials.
- Comparison pages name competitors factually — features, price ranges, fit. No
  disparagement you can't source; it's a legal risk and engines discount it.
