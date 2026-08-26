---
name: redirects-and-migrations
description: Use when replacing an existing website, changing domains or URLs, or writing redirect rules — any change where old URLs must keep working.
metadata:
  category: technique
  triggers: redirects, 301, _redirects, site migration, URL change, domain change, redirect map
---

# Redirects & Migrations

## When to Use
- Replacing an old site (site-builder → new build is the classic)
- Any URL structure change
- An audit finds old URLs returning 404

## Build the redirect map BEFORE launch

Inventory every URL the old site ever exposed:

1. `site:olddomain.com` in Google — what's actually indexed
2. Old sitemap.xml / builder page list
3. Search Console top pages report (if there's history)
4. URLs printed on business cards, GBP links, social profiles, email signatures
5. Ask the owner: "any links you've shared for years?"

Map each to its best new equivalent — the page that serves the same intent, or an
anchor on a single-page site. Only map to `/` when nothing closer exists.

## Netlify `_redirects` format

File named `_redirects` in the publish root, one rule per line:

```
/services            /#services        301
/services/           /#services        301
/about-us            /#about           301
/old-contact-page    /#contact         301
```

- Cover trailing-slash variants of every path
- **301** for permanent moves (passes link equity); 302 only for genuinely temporary
- **No catch-all `/* / 301`** — it masks real 404s, breaks the 404 page, and hides
  future broken links from you
- Verify anchors actually exist in the target page before mapping to them

## The rules that prevent equity loss

- **One hop.** old-url → final-url directly. Chains (A→B→C) leak signals and slow
  users; when a target later moves, update the ORIGINAL rule.
- **Redirect at the same protocol+host layer.** http→https and www→apex handled
  globally (host/CDN level), path redirects in `_redirects` — don't stack them into
  chains.
- Keep the map in the repo forever. Redirects are infrastructure, not a launch
  artifact; domains keep earning 404s from old links for years.
- After a domain change (not just a redesign), keep the old domain registered and
  redirecting for **years**, and use Search Console's Change of Address tool.

## Verify

```bash
curl -s -o /dev/null -w "%{http_code} -> %{redirect_url}\n" https://example.com/services
# want: 301 -> https://example.com/#services  (one hop, correct target)
```

Run this for every row of the map. A migration isn't done until the map is verified
live — "we launched" and "old links still work" are separate facts.
