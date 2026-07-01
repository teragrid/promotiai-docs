---
name: promotiai-creator-personal-brand
description: PromotiAI content operator template for Creator / Personal Brand — audience growth, sponsorships, product drops. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — Creator / Personal Brand Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `creator_personal_brand` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for
> your specific channel, then drop this file into your agent's skills directory. Connect an MCP client first
> using the [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your name/brand] running audience-growth content on PromotiAI.

**Mission**: Generate, review, and schedule organic content that grows an engaged audience and drives product
drops/sponsorship interest for [your brand] — first-person, behind-the-scenes, always teasing what's next.

## Who this content is for

- **Audience**: Engaged niche audience, 18–40, following for the person as much as the content
- **Tone**: authentic-energetic
- **Voice variants to choose from**:
  - **Authentic storyteller** — e.g. "Real talk: here's what year 1 actually cost me."
  - **High-energy** — e.g. "Drop incoming. You're going to want this one."
- **Content instructions**: First-person voice, behind-the-scenes framing, drop teasers. This audience wants
  to feel like an insider, not a customer.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `instagram, tiktok, youtube, email` — of those,
**instagram** and **tiktok** are directly usable as MCP `platform` values for organic posts. `youtube` is not
one of the platforms `create_post`/`schedule_post` support, and `email` is not currently an MCP-covered
channel — keep long-form video and newsletter distribution on your own tools and use MCP for the
Instagram/TikTok layer.

## What to track

- **Primary KPI**: follower growth — target **+5%/mo**
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "tiktok", tone: "energetic", max_chars })` and an
   Instagram variant, briefed with the first-person/behind-the-scenes angle above → `create_post(...)` to
   save each draft
3. **Media** — `generate_media({ banner_params, post_id })` — **mandatory** for both Instagram and TikTok;
   this vertical is visual-first by definition
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` around your audience's known
   peak-engagement windows
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check follower-growth movement

## Anti-patterns

- Do not schedule Instagram/TikTok posts without media attached — the publish job fails silently
- Do not publish generated copy without reading it first — voice authenticity is the whole value proposition
  here, and AI phrasing that doesn't sound like you will be noticed
- Do not reuse the same copy across Instagram and TikTok — TikTok needs hook/value/CTA script format
- Do not treat `youtube` / `email` as MCP-automatable — those live outside MCP's scope
