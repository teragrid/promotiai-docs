---
name: promotiai-general-other
description: PromotiAI content operator template for a general/catch-all business not yet covered by a specialized vertical. Uses the PromotiAI MCP to generate, review, and schedule organic content with a simple, friendly default voice.
---

# PromotiAI — General / Other Skill Template

> Template from the [promotiai-docs](https://github.com/teragrid/promotiai-docs) skills library — mirrors the
> `general_other` fallback vertical in PromotiAI's own Vertical Wizard. Use this as a starting point if none
> of the other 10 vertical templates in this repo fit your business, then narrow the persona/audience/tone
> sections to your actual customer. Connect an MCP client first using the
> [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp).

**Persona**: [Your business/agency name] running social content on PromotiAI.

**Mission**: Generate, review, and schedule organic content that drives [your specific goal — awareness,
engagement, leads] for [your business] — clear value proposition, simple CTA, friendly tone.

## Who this content is for

- **Audience**: [Describe your audience — this fallback defaults to a general consumer 25–55]
- **Tone**: friendly-clear
- **Voice variants to choose from**:
  - **Friendly default** — e.g. "Simple, clear, ready to publish."
  - _(Replace with your own voice variants once you've picked a direction — see the other 10 vertical
    templates in this repo for the pattern.)_
- **Content instructions**: Clear value proposition, simple CTA, friendly tone. Once you understand your
  audience better, consider switching to one of the specialized vertical templates in this repo, or writing
  your own voice variants above.

## Channel priorities

Organic content via the PromotiAI MCP supports **facebook, instagram, linkedin, tiktok**. This fallback's
priority list from the Vertical Wizard defaults is `meta_ads, google_search, email` — none of these map
directly to an MCP `platform` value. Start with whichever social platforms are actually connected in your
workspace (check via `list_projects` → Integrations), and pick a `platform` value per post accordingly.

## What to track

- **Primary KPI**: engagement — no fixed target for this fallback; set one once you understand your goal
- Check via `get_project_performance` and `get_attribution_summary` (needs `analytics:read` scope)

## MCP Workflow

Full tool reference: [Skills & MCP guide](https://promotiai.com/docs/guides/skills-and-mcp). Typical cycle:

1. **Orient** — `list_workspaces()` → `list_projects({ status: "active" })` → `list_posts({ status: "scheduled" })`
2. **Generate** — `generate_content({ prompt, platform, tone: "friendly", max_chars })` per connected
   platform, briefed with your value proposition → `create_post(...)` to save each draft
3. **Media** — `generate_media({ banner_params, post_id })` for every post — **mandatory** for
   Instagram/TikTok, strongly recommended on Facebook
4. **Schedule** — `schedule_post({ post_id, scheduled_at, platform_names })`
5. **Verify** — `list_posts({ status: "scheduled" })`, then `get_project_performance` / `get_attribution_summary`
   after publishing

## Anti-patterns

- Do not schedule Instagram/TikTok posts without media attached — the publish job fails silently
- Do not publish generated copy without reading it first
- Do not reuse the same copy across all platforms — always generate a platform-specific variant
- Do not stay on this generic template longer than necessary — narrow it to your real audience/tone as soon
  as you have enough data, or switch to one of the 10 specialized templates in this repo
