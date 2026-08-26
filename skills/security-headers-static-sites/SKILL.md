---
name: security-headers-static-sites
description: Use when adding or auditing HTTP security headers on a static marketing site — CSP, HSTS, X-Frame-Options — especially before quoting a "security score" to a client.
metadata:
  category: technique
  triggers: security headers, CSP, HSTS, X-Frame-Options, Content-Security-Policy, securityheaders.com
---

# Security Headers for Static Sites

## When to Use
- Hardening any static marketing site
- Producing a security-score comparison (before/after sells itself)
- Reviewing a `_headers` file

## The six headers (Netlify `_headers` format)

```
/*
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin
  X-Frame-Options: DENY
  Permissions-Policy: camera=(), microphone=(), geolocation=()
  Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self'; img-src 'self' data:; font-src 'self'; connect-src 'self'; form-action 'self'; frame-ancestors 'none'; base-uri 'none'; object-src 'none'; upgrade-insecure-requests
  Strict-Transport-Security: max-age=63072000
```

Adjust CSP for what the site actually loads: Google Fonts needs
`style-src 'self' https://fonts.googleapis.com; font-src 'self' https://fonts.gstatic.com`;
an analytics script needs its origin in `script-src` and `connect-src`. Start strict,
loosen per real console errors — never start with `unsafe-inline` "to be safe."

## ⚠️ The HSTS subdomain trap

`includeSubDomains` and `preload` look like free upgrades. **They are not.**

`includeSubDomains` forces HTTPS on **every** subdomain of the apex — including ones
that aren't websites: remote-desktop endpoints (`rds.`), mail hosts, legacy client
portals, printers exposed for a vendor. If any of those lacks a valid certificate,
adding this directive locks real users out — and `preload` bakes the lock into
browsers for months, effectively irreversibly.

**Rule: never add `includeSubDomains` or `preload` until you have enumerated every
subdomain in the DNS zone and verified each serves valid HTTPS.** For a small business
with an RDP or mail subdomain, plain `max-age` on the web host is the correct
configuration, not a compromise. Do not "fix" it in a later cleanup pass.

## Rules

- Test CSP in a browser with DevTools open before shipping — a too-strict CSP
  silently kills fonts, forms, or analytics
- `frame-ancestors 'none'` (CSP) and `X-Frame-Options: DENY` are belt and suspenders;
  keep both unless the site must be embeddable
- Don't add headers that need server logic (no `Public-Key-Pins` — deprecated;
  no reporting endpoints you won't read)

## Verify

```bash
curl -sI https://example.com/ | grep -iE "strict-transport|content-security|x-frame|x-content-type|referrer-policy|permissions-policy"
```

Count them: "N of 6" is the score. https://securityheaders.com gives the letter grade
clients screenshot. Typical site-builder sites score 2 of 6 — the before/after is a
better sales asset than any slide.
