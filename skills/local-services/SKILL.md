---
name: promotiai-local-services
description: PromotiAI content operator template for Local Services (plumber, dentist, lawyer, etc.) — local SEO + lead gen. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — Local Services Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `local_services` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for your
> specific business, then drop this file into your agent's skills directory. Connect an MCP client first
> using the [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your business/agency name] running local lead generation for [your service business] on
PromotiAI.

**Mission**: Generate, review, and schedule organic content that builds local trust and drives calls/bookings
for [your business] — proximity-led, response-time forward, always with a strong phone/booking CTA.

## Who this content is for

- **Audience**: Local homeowners and renters needing trusted, nearby help
- **Tone**: reassuring-direct
- **Voice variants to choose from**:
  - **Trusted pro** — e.g. "Same-day service. 200+ five-star reviews."
  - **Neighbor-friendly** — e.g. "Helping families in [your area] since [year]."
- **Content instructions**: Lead with proximity, response time, and reviews. End with a strong phone or
  booking CTA — this audience converts on trust and urgency, not browsing.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `google_local, meta_ads, google_search, referral` — none
of these map directly to an MCP `platform` value; they're Google Business Profile, paid ads, search, and
referral, all managed outside MCP (Google Business Profile directly, or the dashboard's Campaigns tab). If
your business also keeps an active Facebook/Instagram presence for local trust-building (reviews, before/after
photos, community posts), use MCP to generate and schedule that content — it's a real complement to the
local-SEO/paid channels above, just not what the wizard defaults to first.

## What to track

- **Primary KPI**: cost per lead — target **100,000 VND** (adjust to your currency/market)
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "facebook", tone: "reassuring", max_chars })` briefed
   with the trust/proximity angle above → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` — strongly recommended on Facebook (organic reach
   drops sharply without it), mandatory if also posting to Instagram
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` around local peak-browsing hours
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check cost-per-lead movement

## Anti-patterns

- Do not schedule Instagram posts without media attached — the publish job fails silently
- Do not publish generated copy without reading it first
- Do not treat `google_local` / `meta_ads` / `google_search` as MCP-automatable — those are managed directly
  in Google Business Profile or the dashboard's Campaigns tab
- Do not bury the phone number/booking link — local-services content converts on the CTA, not the story
