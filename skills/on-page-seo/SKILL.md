---
name: on-page-seo
description: Use when writing or optimizing page titles, meta descriptions, headings, or internal links on any web page.
metadata:
  category: technique
  triggers: title tag, meta description, heading structure, h1, internal linking, on-page
---

# On-Page SEO

## When to Use
- Writing any new page
- Optimizing existing pages after an audit
- Reviewing AI-generated page copy before it ships

## Title tags

- ~50–60 characters (Google truncates around 580px)
- Pattern: `Primary Topic | Brand` or `Brand | Primary Topic + Qualifier`
- Front-load the thing people search for: "Tax Preparation in Yuba City | Corbella
  Accounting" beats "Welcome to Our Website"
- Unique per page. Duplicate titles = pages competing with each other.

## Meta descriptions

- ~150–160 characters; a truthful pitch for the click, containing the topic phrase
- Written for humans — it's ad copy, not a keyword container
- Google rewrites bad ones; a good one earns the click AND is lift-ready text for AI
  summaries

## Headings

- Exactly one `<h1>` — the page's actual subject, not the brand slogan
- `<h2>`s are the page's outline; a reader (or an LLM) scanning only headings should
  understand the page
- **Question-form h2/h3s** ("How much does tax preparation cost?") double as AI-answer
  anchors — engines lift the heading + first paragraph as a unit
- Never skip levels (h1 → h3) and never choose headings by font size — that's CSS's job

## Body copy

- First paragraph answers "what is this page and who is it for" in plain language
- Specifics beat adjectives: services, prices or price ranges, cities served, years —
  every concrete fact is retrievable; "premier full-service solutions" is not
- One page = one topic. If a page tries to rank for two distinct intents, split it.

## Internal links

- Descriptive anchor text ("tax preparation services", never "click here")
- Every indexable page reachable within 2 clicks of the homepage
- Link to canonical URLs directly — no bouncing through redirects
- Cross-link related pages (service ↔ city ↔ FAQ) so engines see the topic cluster

## Rules

- Never keyword-stuff. Density thinking died in 2012; entity coverage (naming the
  services, places, and concepts a topic implies) is what modern retrieval rewards.
- Never ship copy with invented facts, credentials, or testimonials — see the
  repo-level guardrails. AI drafting makes this failure effortless; the review step
  exists to catch it.
- Alt text describes the image for a blind user; the SEO value is a side effect.
