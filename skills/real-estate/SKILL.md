---
name: promotiai-real-estate
description: PromotiAI content operator template for Real Estate — listing exposure, buyer/seller leads. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — Real Estate Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `real_estate` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for your
> specific listings/market, then drop this file into your agent's skills directory. Connect an MCP client
> first using the [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your agency/agent name] running listing and lead-gen content on PromotiAI.

**Mission**: Generate, review, and schedule organic content that builds market expertise and captures
buyer/seller leads for [your market/area] — expert, photo/detail-forward, always capturing a lead.

## Who this content is for

- **Audience**: First-time buyers, upgraders, and downsizers researching the market
- **Tone**: expert-trustworthy
- **Voice variants to choose from**:
  - **Market expert** — e.g. "Q1 prices in [your area]: here's what changed."
  - **Lifestyle seller** — e.g. "Wake up to this view. Three bedrooms. Move-in ready."
- **Content instructions**: Highlight neighborhood, photos, and agent expertise. Every post should capture a
  lead — form, DM, or call.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `meta_ads, google_search, linkedin, property_portals` — of
those, **linkedin** is directly usable as an MCP `platform` value for organic posts (market-update,
thought-leadership style). `meta_ads`, `google_search`, and `property_portals` (e.g. listing sites) are
managed outside MCP. Many agents also run organic Facebook/Instagram for listing photos — add those platforms
to your generation loop if your workspace connects them.

## What to track

- **Primary KPI**: qualified leads — target **15/mo**
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "linkedin", tone: "expert", max_chars })` briefed with
   the listing/market-update angle above → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` — recommended on every platform; listing/lifestyle
   photography is the core selling asset in this vertical, mandatory if posting to Instagram
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` around weekend open-house windows
   and weekday market-update slots
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check qualified-lead movement

## Anti-patterns

- Do not schedule Instagram posts without media attached — the publish job fails silently
- Do not publish generated copy without reading it first — pricing/market claims need a human check
- Do not reuse the same copy across all platforms — LinkedIn wants market-expert framing, Instagram wants
  lifestyle framing
- Do not treat `meta_ads` / `google_search` / `property_portals` as MCP-automatable — those live outside
  MCP's scope
