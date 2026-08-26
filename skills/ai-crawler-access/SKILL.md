---
name: ai-crawler-access
description: Use when checking or fixing whether AI crawlers can reach a site — robots.txt rules, CDN/WAF bot blocking, or a brand invisible to ChatGPT/Perplexity despite good content.
metadata:
  category: technique
  triggers: robots.txt, GPTBot, ClaudeBot, PerplexityBot, bot blocking, crawler access, WAF, Cloudflare bot fight
---

# AI Crawler Access

## When to Use
- Auditing any site for AI visibility (do this FIRST — it's the most common killer)
- A site with good content that never appears in AI answers
- Writing or reviewing robots.txt

## The crawlers that matter

| Crawler | Operator | Feeds |
|---|---|---|
| GPTBot | OpenAI | Model training |
| OAI-SearchBot | OpenAI | ChatGPT search results |
| ChatGPT-User | OpenAI | Live browsing during a chat |
| ClaudeBot / Claude-Web | Anthropic | Claude's knowledge and browsing |
| PerplexityBot | Perplexity | Perplexity answers + citations |
| Google-Extended | Google | Gemini / AI Mode grounding |
| Bingbot | Microsoft | Bing → also feeds ChatGPT search |

Blocking any of these removes you from that engine's answers. That's a business
decision, not a default — for a business that *wants* AI referrals, allow all.

## Reference robots.txt

```
User-agent: *
Allow: /

User-agent: GPTBot
Allow: /

User-agent: OAI-SearchBot
Allow: /

User-agent: ChatGPT-User
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: Claude-Web
Allow: /

User-agent: Google-Extended
Allow: /

Sitemap: https://example.com/sitemap.xml
```

The explicit per-bot Allow blocks are redundant with `*` but serve as documentation
and survive a future `Disallow` added under `*`.

## The hidden blockers (robots.txt is not enough)

Check ALL of these — any one silently overrides a welcoming robots.txt:

1. **`X-Robots-Tag` response header** — `curl -sI URL | grep -i x-robots`
2. **`<meta name="robots">` in the HTML** — grep the served HTML, not the source file
3. **CDN/WAF bot rules** — Cloudflare "Bot Fight Mode" / "AI Scrapers and Crawlers"
   toggle, AWS WAF bot control, Vercel/Netlify firewall rules. These return 403s to
   bots while humans see a perfect site. Test with a spoofed user agent:
   `curl -s -o /dev/null -w "%{http_code}" -A "GPTBot" https://example.com/`
   (A 403 here with a 200 for a normal UA = CDN-level block.)
4. **Rate limiting / JS challenges** — interstitial pages serve the challenge HTML to
   crawlers instead of content.
5. **Geo-blocking** — crawlers come from US datacenter IPs; country blocks catch them.

## Rules

- A robots.txt that blocks ALL AI crawlers on a business site is a **hero finding** in
  any audit — lead with it, quantify it ("invisible to every AI assistant"), fix it
  first.
- After any fix, verify at the **live URL** with both a normal and a bot user agent.
- Never advise cloaking (serving bots different content than humans). It violates
  every engine's policy and gets domains delisted.
