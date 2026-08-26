---
name: local-seo
description: Use when optimizing a business for local search and local AI answers — NAP consistency, Google Business Profile, city landing pages, service areas.
metadata:
  category: technique
  triggers: local SEO, Google Business Profile, GBP, NAP, city pages, near me, service area
---

# Local SEO

## When to Use
- Any business serving a geographic area
- "We don't show up for [service] in [city]"
- Building city or service-area landing pages

## NAP: one truth, everywhere

Name, Address, Phone must be **character-identical** across:
1. The visible site (header/footer/contact)
2. JSON-LD schema
3. llms.txt
4. Google Business Profile
5. Every directory and citation

"Ste A" vs "Suite A" vs "#A" are three different businesses to a matching algorithm.
Pick the format on the Google Business Profile and propagate it. When auditing, get
the GBP values FIRST and treat them as canonical.

## Google Business Profile parity

The GBP and the website must tell the same story: same categories/services, same
hours, same phone. Cross-check as a standard audit step — mismatch is a trust leak in
both Google's local pack and AI answers (engines read the profile AND the site).

- Primary category = the most specific true one
- Every service on the GBP has a matching section or page on the site
- Photos: real premises/team, not stock
- Reviews: respond to all; never fabricate or gate ("only ask happy customers via a
  filter") — that violates FTC rules and platform policy

## City landing pages

For each real target city, one genuine page — not find-and-replace clones:

- Title: `[Service] in [City], [ST] | [Brand]`
- Content that could ONLY be about that city: driving distance, local landmarks,
  county specifics, local client types (e.g., ag operations in Sutter County)
- Its own FAQ (2–3 questions with the city in them)
- Linked from the main nav or services section, in the sitemap, self-canonical
- `areaServed` in schema includes the city

**Threshold rule:** if you can't write 300+ words unique to that city, you don't have
a city page — you have doorway spam. Google penalizes it and AI engines ignore it.
Fold minor towns into a "serving the [region]" section instead.

## Service-area businesses (no storefront)

- Hide the street address on GBP; keep it in schema as `PostalAddress` only if it's a
  real staffed office
- Lean harder on `areaServed` and city pages

## Verify

- Search the exact NAP string in quotes — inconsistencies surface immediately
- Ask an AI assistant: "best [service] in [city]" and "[brand name] [city]" — note
  what it says and where it sources; that's your baseline (see aeo-measurement)
