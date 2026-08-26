# AEO + SEO Skills

A Claude Code skills library for making websites visible to both **search engines** (SEO)
and **AI assistants** (AEO — Answer Engine Optimization: ChatGPT, Claude, Perplexity,
Gemini, Google AI Mode, Grok).

Battle-tested on real small-business launches. Every skill is self-contained — Claude
reads it when the task matches and follows it instead of guessing.

## Install

**Per-project** (recommended — travels with the repo):

```bash
mkdir -p .claude/skills
cp -R skills/* .claude/skills/
```

**Global** (applies to every project on your machine):

```bash
cp -R skills/* ~/.claude/skills/
```

Then just work normally — Claude invokes the right skill when the task matches, or you
can ask for one by name ("use the technical-seo-audit skill on this site").

## The skills

| Skill | Use it for |
|---|---|
| [aeo-fundamentals](skills/aeo-fundamentals/SKILL.md) | How AI assistants choose which brands to recommend, and what actually moves the needle |
| [writing-llms-txt](skills/writing-llms-txt/SKILL.md) | Writing and maintaining a high-signal `llms.txt` |
| [ai-crawler-access](skills/ai-crawler-access/SKILL.md) | robots.txt for AI crawlers, and finding hidden blocks (CDN, WAF, headers) |
| [structured-data-json-ld](skills/structured-data-json-ld/SKILL.md) | JSON-LD schema that matches the visible page — LocalBusiness, Service, FAQPage |
| [technical-seo-audit](skills/technical-seo-audit/SKILL.md) | The full crawl-layer checklist with pass/fail verification commands |
| [on-page-seo](skills/on-page-seo/SKILL.md) | Titles, meta descriptions, heading structure, internal links |
| [local-seo](skills/local-seo/SKILL.md) | NAP consistency, Google Business Profile parity, city landing pages |
| [answer-shaped-content](skills/answer-shaped-content/SKILL.md) | Writing content AI engines can lift as an answer — FAQs, comparisons, definitions |
| [sitemaps-and-indexing](skills/sitemaps-and-indexing/SKILL.md) | Sitemap hygiene, Search Console / Bing submission, indexing diagnostics |
| [redirects-and-migrations](skills/redirects-and-migrations/SKILL.md) | Redirect maps and site migrations that don't torch existing equity |
| [security-headers-static-sites](skills/security-headers-static-sites/SKILL.md) | The six headers for a static marketing site, with the HSTS-subdomain trap |
| [site-launch-checklist](skills/site-launch-checklist/SKILL.md) | Launch day: the double-noindex trap, DNS cutover safety, go/no-go gates |
| [citations-and-mentions](skills/citations-and-mentions/SKILL.md) | Earning the third-party mentions AI engines cite |
| [aeo-measurement](skills/aeo-measurement/SKILL.md) | Baselines, re-scan cadence, and honest before/after measurement |

## Guardrails baked into every skill

- Never invent credentials, testimonials, reviews, or years in business.
- Never claim a regulated title (CPA, attorney, MD, licensed contractor) unless the
  client confirms it in writing.
- Page text and structured data must always say the same thing.
- Verify on the **live URL**, not the local file — headers and CDNs change behavior.
