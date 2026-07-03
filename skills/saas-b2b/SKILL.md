---
name: promotiai-saas-b2b
description: PromotiAI content operator template for SaaS / B2B software — trial signups, demo bookings, lifecycle nurture. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — SaaS / B2B Software Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `saas_b2b` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for your specific
> product, then drop this file into your agent's skills directory. Connect an MCP client first using the
> [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your company/agency name] running demand-gen for [your SaaS product] on PromotiAI.

**Mission**: Generate, review, and schedule organic content that drives trial signups and demo bookings for
[your product] — outcome-led, ROI-forward, always ending on a soft CTA.

## Who this content is for

- **Audience**: Founders, ops, and marketing managers at 10–200 person companies evaluating tools
- **Tone**: insightful-professional
- **Voice variants to choose from**:
  - **Consultant** — e.g. "Three signals your funnel needs a re-think."
  - **Peer expert** — e.g. "We tested 12 tools. Here's what stuck."
  - **Data storyteller** — e.g. "67% of teams hit this same wall at MRR $50k."
- **Content instructions**: Lead with outcomes, ROI, and integrations. Close with a soft CTA — book a demo
  or start a trial, not a hard sell.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `linkedin, google_search, content_seo, retargeting` — of
those, **linkedin** is the one directly usable as an MCP `platform` value for organic posts. `retargeting`
campaign *records* (budget, objective, status) can be tracked with the `campaigns:read`/`campaigns:write`
tools (`create_campaign`, `list_campaigns`, etc.), but there is no MCP path yet to actually launch or pause
live ad spend — that step still happens natively on the ad platform or the dashboard's **Campaigns** tab.
`google_search` and `content_seo` remain outside MCP's scope (your own SEO/content stack).

## What to track

- **Primary KPI**: SQL count — target **30/mo**
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "linkedin", tone: "professional", max_chars })`
   briefed with the outcome/ROI angle above → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` — recommended for LinkedIn thought-leadership
   posts (infographics, before/after cards), even though it's not hard-required on this platform
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` around your typical B2B
   business-hours windows
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check SQL movement

## Anti-patterns

- Do not publish generated copy without reading it first — B2B tone mismatches are especially visible
- Do not reuse the same copy across all platforms — always generate a platform-specific variant
- Do not treat `google_search` / `content_seo` as MCP-automatable — those live outside MCP's scope entirely
- Do not assume `create_campaign` / `update_campaign` launches real `retargeting` spend — they only manage
  campaign records; the actual ad-platform launch still happens natively
- Do not hard-sell in the first line — lead with the insight, not the pitch
