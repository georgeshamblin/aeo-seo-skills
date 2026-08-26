---
name: sitemaps-and-indexing
description: Use when creating sitemaps, submitting a site to Google Search Console or Bing, or diagnosing why pages aren't indexed.
metadata:
  category: technique
  triggers: sitemap.xml, Search Console, indexing, Bing Webmaster, crawled not indexed, URL inspection
---

# Sitemaps & Indexing

## When to Use
- Launch day (submission is a launch step, not a someday task)
- "Google hasn't indexed us"
- Adding/removing pages from a site

## Sitemap rules

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://example.com/</loc><lastmod>2026-08-26</lastmod></url>
  <url><loc>https://example.com/page.html</loc><lastmod>2026-08-26</lastmod></url>
</urlset>
```

- **Canonical, indexable URLs only.** No redirects, no noindexed pages (thank-you,
  404), no http:// duplicates, no parameter variants. A sitemap listing a noindexed
  URL sends Google contradictory signals.
- `lastmod` honest or absent — faking freshness gets the field ignored domain-wide
- Referenced from robots.txt: `Sitemap: https://example.com/sitemap.xml`
- Update in the same commit that adds/removes a page

## Submission (once per site)

**Google Search Console:** add a **Domain property** (covers http/https/www/apex in
one). Verification is a DNS TXT record — takes 2 minutes when you have registrar
access, so do it while DNS is already open during a launch. Then Sitemaps → submit.

**Bing Webmaster Tools:** "Import from Google Search Console" — one click, and Bing
feeds ChatGPT search, so it matters more than its traffic share suggests.

## Timeline honesty (set expectations aloud)

- Indexing: 24 hours to ~7 days for a healthy new site
- Ranking movement: weeks
- AI-assistant answers: independent clock entirely (see aeo-measurement)

Say this BEFORE launch or the silence afterward feels like failure.

## Diagnosing "not indexed"

Work the list in order:

1. **Can Google fetch it?** URL Inspection tool → Live Test. 4xx/5xx = fix access.
2. **Is it blocked?** robots.txt, meta noindex, X-Robots-Tag header — all three.
3. **Is it canonical?** Inspection says "Duplicate, Google chose different canonical"
   = fix canonical tags or consolidate the duplicate.
4. **"Crawled — currently not indexed"** = quality verdict, not a bug. The fix is a
   better page (more unique value, internal links to it), not resubmission.
5. **"Discovered — currently not indexed"** = crawl-budget/priority. Internal links
   from strong pages and patience.

Never buy "instant indexing" services and don't hammer the resubmit button — one
submission plus a fixed page is the whole playbook.
