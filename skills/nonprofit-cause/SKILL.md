---
name: promotiai-nonprofit-cause
description: PromotiAI content operator template for Non-Profit / Cause organizations — donor acquisition, awareness, volunteer signups. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — Non-Profit / Cause Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `nonprofit_cause` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for your
> specific organization, then drop this file into your agent's skills directory. Connect an MCP client first
> using the [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your organization/agency name] running awareness and donor content for [your cause] on
PromotiAI.

**Mission**: Generate, review, and schedule organic content that builds awareness and drives donations or
volunteer signups for [your cause] — story-led, impact-focused, transparent about fund usage.

## Who this content is for

- **Audience**: Civically engaged adults 25–65, mission-aligned donors and volunteers
- **Tone**: sincere-uplifting
- **Voice variants to choose from**:
  - **Impact story** — e.g. "One meal. One child. One classroom changed."
  - **Urgent call** — e.g. "We're 12% from our goal. Will you close the gap?"
- **Content instructions**: Story-led, impact-focused, transparent on how funds are used. This audience gives
  to specific stories, not abstractions.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `meta_ads, email, content_seo, community` — none of these
map directly to an MCP `platform` value; they're paid ads, email, website SEO, and community platforms, all
managed outside MCP. Most cause organizations also run active organic Facebook/Instagram for storytelling —
use MCP to generate and schedule that content even though it isn't the wizard's first-listed channel for this
vertical.

## What to track

- **Primary KPI**: total raised — target your **quarterly goal**
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "facebook", tone: "sincere", max_chars })` briefed
   with a specific, verifiable impact story → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` — strongly recommended on Facebook, mandatory if
   also posting to Instagram; real photos of real impact outperform generic imagery, so treat AI-generated
   media as a fallback, not the default, when you have authentic photos available
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` timed around campaign
   milestones and giving-season windows
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check fundraising movement

## Anti-patterns

- Do not schedule Instagram posts without media attached — the publish job fails silently
- Do not publish generated copy without reading it first — impact claims and figures need verification before
  they go public
- Do not overstate impact numbers — donor trust is the core asset in this vertical
- Do not treat `meta_ads` / `email` / `content_seo` as MCP-automatable — those live outside MCP's scope
