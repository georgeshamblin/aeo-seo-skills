---
name: technical-seo-audit
description: Use when auditing a website's technical SEO — crawlability, indexability, meta tags, canonicals, redirects — or producing a findings list for a client.
metadata:
  category: technique
  triggers: SEO audit, technical audit, crawlability, indexability, canonical, site health
---

# Technical SEO Audit

## When to Use
- Any new client site (first deliverable)
- Before and after a launch or migration
- "Why isn't this page ranking/indexed?"

## Method

Audit the **live URL** with curl — never trust the source files, because headers,
CDNs, and build steps change what's actually served. Produce a findings table:
`# | Finding | Severity | Evidence | Fix | Status`. Severity: Critical (blocks
indexing/crawling) → High (costs rankings) → Medium → Low.

## The checklist

### Indexability (Critical tier — check first)
```bash
curl -sI https://example.com/ | grep -i x-robots        # must be empty or index,follow
curl -s https://example.com/ | grep -i 'name="robots"'  # no noindex
curl -s https://example.com/robots.txt                   # not blocking site or key bots
```
- noindex hides in **two places** — meta tag AND `X-Robots-Tag` header. Check both on
  every page type. A page can render perfectly while a header keeps it invisible.

### Protocol & canonicalization
- HTTP → HTTPS 301; www → apex (or vice versa) 301 — one canonical origin, everything
  else redirects to it with a single hop
- `<link rel="canonical">` present, absolute, self-referencing on canonical pages
- No mixed content (http:// assets on https pages)

### Per-page head
- `<title>` unique, ~50–60 chars, brand + primary topic
- Meta description present, ~150–160 chars, matches the page
- Exactly **one h1** per page; h2/h3 hierarchy without skips
- OG tags (`og:title`, `og:description`, `og:image` that returns 200)
- `lang` attribute on `<html>`

### Structure
- `sitemap.xml`: 200, lists only canonical indexable pages, referenced from robots.txt
- 404s return actual HTTP 404 (not a 200 "soft 404")
- Old/moved URLs 301 to their replacements (see redirects-and-migrations)
- Internal links use canonical URLs (no redirect chains)

### Extras that separate a good audit
- Security headers (see security-headers-static-sites) — quantify as "N of 6"
- `llms.txt` + AI crawler access (see ai-crawler-access)
- JSON-LD validity and page parity (see structured-data-json-ld)
- Image alt text, compressed images, no layout-shifting hero
- Page weight sanity: flag pages over ~1.5MB transferred

## Reporting rules

- **Every finding needs evidence** — the actual header value, the actual missing tag.
  "Verified live at [URL] on [date]," not "appears to."
- **Count what's already right.** "30 findings, 15 already solved" lands better than a
  wall of red, and it's honest.
- **Lead with the hero finding** — the one Critical item that explains the client's
  symptom (e.g., "robots.txt blocks every AI crawler").
- Never pad severity to inflate the report. An accountant-brained client checks.
