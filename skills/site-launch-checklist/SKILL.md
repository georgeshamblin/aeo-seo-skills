---
name: site-launch-checklist
description: Use when taking a website live — DNS cutover, removing staging blocks, go/no-go verification — or when a launched site mysteriously gets no traffic.
metadata:
  category: discipline
  triggers: launch, go live, DNS cutover, noindex, staging, domain flip, propagation
---

# Site Launch Checklist

## When to Use
- Any go-live, no matter how small
- "We launched last week and nothing's happening" (usually trap #1 below)

This is a **discipline skill**: run every gate in order. The failure modes here are
silent — the site looks perfect while being invisible, or the website works while
the client's email is down. No step is skippable because "it's probably fine."

## Trap #1: the double noindex

Staging blocks indexing in **two places**. Both must be removed at launch:

1. `<meta name="robots" content="noindex, nofollow">` in every HTML page
2. `X-Robots-Tag: noindex` in `_headers` (or server config)

Remove only the meta tags and the site launches looking perfect while the header
keeps every crawler out — and nobody notices for weeks, because pages render fine.

```bash
curl -sI https://example.com/ | grep -i x-robots     # must return nothing
curl -s https://example.com/ | grep -i noindex        # must return nothing
```

## Trap #2: DNS records that aren't the website

Before touching a zone, inventory what ELSE lives on the domain:

- **MX records** — the business's email. Change nameservers carelessly and email
  stops. (Email-security services like Barracuda make this non-obvious: the MX
  points somewhere you don't recognize. That's normal. Don't "clean it up.")
- **Service subdomains** — remote desktop (`rds.`), client portals, VPN, printers.
  Clients log in through these. Same failure mode.

**The safe cutover:** nameservers stay where they are. Change ONLY the apex A record
and the `www` CNAME to the new host. Screenshot the zone before and after. Lower TTL
an hour ahead if you can.

Say the risk out loud before the client touches anything. Naming the downside before
touching production is what makes you the consultant they keep.

## Go/no-go gates (in order)

1. New site deployed and verified on its temporary URL (hosting URL)
2. Placeholders gone: `grep -r "\[" *.html` returns nothing suspicious
3. Redirect map in place (see redirects-and-migrations)
4. Both noindex blocks removed, verified on the temp URL
5. DNS: apex A + www CNAME only; MX and service subdomains untouched
6. Post-flip verify: `dig +short domain.com`, then the full curl battery — 200, no
   noindex, headers present, canonical right, forms work
7. **Send a test email to the client's domain address** — proves mail survived
8. Submit sitemap in Search Console + Bing (see sitemaps-and-indexing)
9. Old builder subscription cancelled — the SITE PLAN only, never the domain
   registration, never anything hosting a service subdomain

## After

- Propagation runs minutes to hours; some resolvers serve the old IP for a while.
  Tell the client in advance or the last five minutes feel like a failure.
- Baseline re-scan for AI visibility in ~1 week (see aeo-measurement)
- "We launched" and "we launched and verified" are different sentences. Only say the
  second one when the gates are green.
