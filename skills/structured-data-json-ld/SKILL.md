---
name: structured-data-json-ld
description: Use when adding or auditing JSON-LD structured data — LocalBusiness, Service, FAQPage, Organization schema — or when page text and schema disagree.
metadata:
  category: technique
  triggers: JSON-LD, schema.org, structured data, LocalBusiness, FAQPage, rich results
---

# Structured Data (JSON-LD)

## When to Use
- Adding schema to any page
- Auditing existing schema (most common defect: placeholder or stale values)
- After any change to phone, address, hours, or services

## Core types for a service business

One `<script type="application/ld+json">` block in `<head>`, using `@graph` to hold
multiple entities:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "AccountingService",
      "@id": "https://example.com/#business",
      "name": "Example Accounting",
      "url": "https://example.com/",
      "telephone": "+1-555-555-5555",
      "email": "hello@example.com",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "123 Main St Ste A",
        "addressLocality": "Yuba City",
        "addressRegion": "CA",
        "postalCode": "95991",
        "addressCountry": "US"
      },
      "openingHoursSpecification": [{
        "@type": "OpeningHoursSpecification",
        "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday"],
        "opens": "09:00",
        "closes": "17:00"
      }],
      "areaServed": ["Yuba City", "Marysville", "Sutter County"]
    },
    {
      "@type": "FAQPage",
      "mainEntity": [{
        "@type": "Question",
        "name": "How much does tax preparation cost?",
        "acceptedAnswer": { "@type": "Answer", "text": "…exact text from the visible FAQ…" }
      }]
    }
  ]
}
```

Pick the most specific business type that's true (`AccountingService`, `Plumber`,
`LegalService`, `Restaurant`…); fall back to `LocalBusiness` only when nothing
specific fits.

## Rules

- **Parity is the law.** Every value in the schema must appear in the visible page and
  match exactly — phone, address, hours, FAQ answers. Schema describing content that
  isn't on the page violates Google's guidelines and erodes AI-engine trust. When you
  update one, update both in the same commit.
- **Real values only.** `[PHONE]` placeholders shipping to production is the single
  most common schema defect. Grep for `[` before every deploy.
- **Phone format:** E.164-ish with country code (`+1-530-555-1234`).
- **One FAQPage per site** (on the page where the FAQ visibly lives), not repeated on
  every page.
- **Never mark up** invented reviews (`aggregateRating` requires real, on-site
  reviews), fake credentials, or regulated titles the client hasn't confirmed.
- **areaServed** should list the real service area — it's a strong local-AEO signal.

## Verify

```bash
# schema parses and contains real values
curl -s https://example.com/ | sed -n '/application\/ld+json/,/<\/script>/p'
```

Then run the live URL through https://validator.schema.org/ and Google's Rich Results
Test. Confirm zero errors and that the phone/address shown match the page footer.
