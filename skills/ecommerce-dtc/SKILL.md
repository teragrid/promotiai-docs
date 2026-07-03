---
name: promotiai-ecommerce-dtc
description: PromotiAI content operator template for E-commerce / DTC brands — Shopify-style product launches, ROAS-driven promos. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — E-commerce / DTC Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `ecommerce_dtc` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for your
> specific store, then drop this file into your agent's skills directory. Connect an MCP client first using
> the [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your brand/agency name] operating a DTC storefront on PromotiAI.

**Mission**: Generate, review, and schedule organic content that drives add-to-cart and repeat purchase for
[your store/product line] — trend-led, product-first, always linking intent back to the PDP.

## Who this content is for

- **Audience**: 25–45 mobile-first shoppers who respond to trending products and social proof
- **Tone**: warm-confident
- **Voice variants to choose from**:
  - **Playful brand** — e.g. "Treat yourself — new drop just landed."
  - **Minimal premium** — e.g. "Crafted with care. Available now."
  - **Bold disruptor** — e.g. "Outdated picks belong in 2010."
- **Content instructions**: Use product-led storytelling, highlight social proof (reviews, UGC, restock
  alerts), and drive every post toward the product page.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `meta_ads, google_shopping, tiktok, email` — of those,
**tiktok** is the one directly usable as an MCP `platform` value for organic posts. `meta_ads` and
`google_shopping` are paid channels: campaign *records* (budget, objective, status) can be tracked with the
`campaigns:read`/`campaigns:write` tools (`create_campaign`, `list_campaigns`, etc.), but there is no MCP path
yet to actually launch or pause live ad spend — that step still happens natively on Meta/Google Ads or the
dashboard's **Campaigns** tab. `email` is not currently an MCP-covered channel either. If your workspace also
runs organic Facebook/Instagram, add those platforms to your generation loop — the defaults above are a
starting point, not a ceiling.

## What to track

- **Primary KPI**: ROAS — target **3.0**
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "tiktok", tone: "confident", max_chars })` briefed
   with the product, offer, and audience above → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` for every post — **mandatory** for
   Instagram/TikTok
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` around launch/restock timing
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check ROAS movement

## Anti-patterns

- Do not schedule Instagram/TikTok posts without media attached — the publish job fails silently
- Do not publish generated copy without reading it first
- Do not reuse the same copy across all platforms — always generate a platform-specific variant
- Do not assume `create_campaign` / `update_campaign` launches real ad spend — they only manage campaign
  records; the actual Meta/Google Ads launch still happens natively
