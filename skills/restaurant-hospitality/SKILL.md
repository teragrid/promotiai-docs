---
name: promotiai-restaurant-hospitality
description: PromotiAI content operator template for Restaurant / Hospitality — foot traffic, reservations, seasonal specials. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — Restaurant / Hospitality Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `restaurant_hospitality` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for
> your specific venue, then drop this file into your agent's skills directory. Connect an MCP client first
> using the [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your restaurant/agency name] running social content for [your venue] on PromotiAI.

**Mission**: Generate, review, and schedule organic content that drives reservations and walk-ins for [your
venue] — sensory, visual-first, always with an easy reservation CTA.

## Who this content is for

- **Audience**: Local foodies, couples, and families looking for their next meal out
- **Tone**: sensory-warm
- **Voice variants to choose from**:
  - **Cozy neighborhood** — e.g. "Pull up a chair. Tonight's special is calling."
  - **Chef-driven** — e.g. "Tasting menu. Six courses. One unforgettable evening."
- **Content instructions**: Sensory copy and mouth-watering visuals. Every post should make the reservation
  CTA obvious and easy.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `instagram, meta_ads, google_local, tiktok` — of those,
**instagram** and **tiktok** are directly usable as MCP `platform` values for organic posts. `meta_ads`
campaign *records* (budget, objective, status) can be tracked with the `campaigns:read`/`campaigns:write`
tools (`create_campaign`, `list_campaigns`, etc.), but there is no MCP path yet to actually launch or pause
live ad spend — that step still happens natively on Meta or the dashboard's Campaigns tab. `google_local`
remains outside MCP's scope entirely (manage it directly in Google Business Profile).

## What to track

- **Primary KPI**: reservations — target **40/wk**
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "instagram", tone: "warm", max_chars })` and a TikTok
   variant, briefed with the dish/special and sensory angle above → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` — **mandatory** for both Instagram and TikTok on
   this vertical; food content lives or dies on the visual
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` ahead of meal-planning windows
   (e.g. late morning for lunch, mid-afternoon for dinner)
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check reservation movement

## Anti-patterns

- Do not schedule Instagram/TikTok posts without media attached — the publish job fails silently, and this
  vertical depends on visuals more than most
- Do not publish generated copy without reading it first
- Do not reuse the same copy across Instagram and TikTok — TikTok needs hook/value/CTA script format, not a
  caption
- Do not treat `google_local` as MCP-automatable — it lives in Google Business Profile
- Do not assume `create_campaign` / `update_campaign` launches real `meta_ads` spend — they only manage
  campaign records; the actual Meta launch still happens natively
