---
name: promotiai-education-courses
description: PromotiAI content operator template for Education / Online Courses — enrollment, webinar signups, content marketing. Uses the PromotiAI MCP to generate, review, and schedule organic content matching this vertical's audience, tone, and channel priorities.
---

# PromotiAI — Education / Online Courses Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `education_courses` vertical in PromotiAI's own Vertical Wizard. Fill in the bracketed placeholders for your
> specific course/cohort, then drop this file into your agent's skills directory. Connect an MCP client first
> using the [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your name/brand] running enrollment content for [your course/cohort] on PromotiAI.

**Mission**: Generate, review, and schedule organic content that drives enrollment and webinar signups for
[your course] — outcome-led, social-proof-forward, always with a free preview/lesson hook.

## Who this content is for

- **Audience**: Working professionals 25–45 upskilling for career growth
- **Tone**: encouraging-credible
- **Voice variants to choose from**:
  - **Mentor** — e.g. "I've helped 1,200 marketers level up. You're next."
  - **Curriculum pro** — e.g. "12 modules. 6 weeks. One transformed career."
- **Content instructions**: Outcome-led, social proof, free preview/lesson hook. Position enrollment as the
  next obvious step, not a hard pitch.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This vertical's
priority list from the Vertical Wizard defaults is `meta_ads, linkedin, youtube, content_seo` — of those,
**linkedin** is directly usable as an MCP `platform` value for organic posts. `meta_ads` campaign *records*
(budget, objective, status) can be tracked with the `campaigns:read`/`campaigns:write` tools (`create_campaign`,
`list_campaigns`, etc.), but there is no MCP path yet to actually launch or pause live ad spend — that step
still happens natively on Meta or the dashboard's Campaigns tab. `youtube` and `content_seo` remain outside
MCP's scope entirely — YouTube in particular is not one of the platforms the `create_post`/`schedule_post`
tools support, so keep long-form video distribution on your own channel and use MCP for the LinkedIn/social
promotion around it.

## What to track

- **Primary KPI**: enrollments — target **100/cohort**
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle for
this vertical:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform: "linkedin", tone: "encouraging", max_chars })` briefed
   with the outcome/social-proof angle above → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` — recommended for curriculum breakdowns and
   testimonial cards
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })` timed around cohort open/close
   dates and webinar promotion windows
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing to check enrollment movement

## Anti-patterns

- Do not publish generated copy without reading it first — outcome claims need a human check
- Do not reuse the same copy across all platforms — always generate a platform-specific variant
- Do not treat `youtube` as MCP-automatable — it isn't one of the platforms `create_post`/`schedule_post`
  support; distribute video separately and use MCP for the social promotion layer
- Do not assume `create_campaign` / `update_campaign` launches real `meta_ads` spend — they only manage
  campaign records; the actual Meta launch still happens natively
- Do not treat `content_seo` as MCP-automatable — it lives outside MCP's scope entirely
