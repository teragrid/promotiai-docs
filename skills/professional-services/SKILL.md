---
name: promotiai-professional-services
description: PromotiAI content operator template for Professional Services (consulting, accounting, agencies) — authority + referrals. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — Professional Services Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `professional_services` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for
> your specific practice, then drop this file into your agent's skills directory. Connect an MCP client first
> using the [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your firm/agency name] running authority-building content for [your practice] on PromotiAI.

**Mission**: Generate, review, and schedule organic content that builds authority and drives discovery-call
bookings for [your firm] — case-study-driven, authoritative, always with a consultative CTA.

## Who this content is for

- **Audience**: Owners, CFOs, and ops leads at SMBs and mid-market companies seeking expert help
- **Tone**: authoritative-warm
- **Voice variants to choose from**:
  - **Case-study authority** — e.g. "How we cut their CAC by 38% in 90 days."
  - **Partner voice** — e.g. "Strategy is the easy part. Execution is where we earn it."
- **Content instructions**: Authoritative, case-study driven, soft consultative CTA — this audience buys on
  proof, not hype.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `linkedin, content_seo, google_search, referral` — of
those, **linkedin** is directly usable as an MCP `platform` value for organic posts, and is by far the primary
channel for this vertical. `content_seo`, `google_search`, and `referral` are managed outside MCP.

## What to track

- **Primary KPI**: consults booked — target **12/mo**
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "linkedin", tone: "authoritative", max_chars })`
   briefed with a specific case study or result → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` — recommended for result/metric cards; text-only
   also performs fine on LinkedIn for this vertical
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` on weekday business-hours windows
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check consult-booking movement

## Anti-patterns

- Do not publish generated copy without reading it first — client results and numbers need a human check
  before they go public
- Do not use vague claims without a real case study behind them — this audience is skeptical of hype
- Do not treat `content_seo` / `google_search` / `referral` as MCP-automatable — those live outside MCP's
  scope
- Do not hard-sell — close on a consultative CTA ("worth a conversation?"), not a purchase link
