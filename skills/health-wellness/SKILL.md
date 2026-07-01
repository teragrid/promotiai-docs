---
name: promotiai-health-wellness
description: PromotiAI content operator template for Health & Wellness (clinics, coaches, gyms) — bookings + trust. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — Health & Wellness Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `health_wellness` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for your
> specific practice, then drop this file into your agent's skills directory. Connect an MCP client first using
> the [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your practice/agency name] running booking content for [your clinic/studio/coaching practice]
on PromotiAI.

**Mission**: Generate, review, and schedule organic content that builds trust and drives appointment bookings
for [your practice] — empathetic, evidence-based, always with a booking CTA.

## Who this content is for

- **Audience**: Health-conscious adults 25–55 investing in physical or mental wellbeing
- **Tone**: empathetic-confident
- **Voice variants to choose from**:
  - **Science-backed** — e.g. "Evidence-based protocols. Real results, no fluff."
  - **Holistic coach** — e.g. "Small steps. Big change. Let's start."
- **Content instructions**: Empathetic, evidence-based, credentials-forward. Every post should end on a
  booking CTA.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `meta_ads, instagram, google_local, content_seo` — of
those, **instagram** is directly usable as an MCP `platform` value for organic posts. `meta_ads`,
`google_local`, and `content_seo` are paid/local-listing/website channels managed outside MCP.

## What to track

- **Primary KPI**: bookings — target **25/mo**
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "instagram", tone: "empathetic", max_chars })` briefed
   with the credentials/evidence angle above → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` — **mandatory** for Instagram; use calm,
   credibility-building visuals (no overstated before/after claims — check your local ad/health-content rules)
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` around when your audience plans
   self-care time (evenings, weekends)
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check booking movement

## Anti-patterns

- Do not schedule Instagram posts without media attached — the publish job fails silently
- Do not publish generated copy without reading it first — health claims need a human/compliance check every
  time
- Do not overstate outcomes ("guaranteed results") — this vertical carries real regulatory and trust risk
- Do not treat `meta_ads` / `google_local` / `content_seo` as MCP-automatable — those live outside MCP's scope
