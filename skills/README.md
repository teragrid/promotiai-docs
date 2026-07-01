# PromotiAI Skill Templates

Eleven persona/vertical skill templates for running [PromotiAI](https://promotiai.com) from an AI agent (Claude, or any
[Model Context Protocol](https://modelcontextprotocol.io) client) instead of the dashboard UI. Each one mirrors a vertical
from PromotiAI's own **Vertical Wizard** (11-industry instant setup), so the audience, tone, voice variants, channel
priorities, and KPI in the template match what PromotiAI itself would pre-populate for that industry.

Start with [Skills & MCP: Automate PromotiAI with AI Agents](https://promotiai.com/docs/guides/skills-and-mcp) to connect
an MCP client and get an API key — these templates assume that step is already done.

## How to use a template

1. Pick the vertical closest to your business below.
2. Copy its folder into your agent's skills directory (e.g. `.github/skills/<name>/SKILL.md` for Claude Code, or your
   client's equivalent skills location).
3. Fill in the `[bracketed placeholders]` — your business name, product, market, and any specific goals.
4. Load the skill in your agent and start with: *"list PromotiAI workspaces"* to confirm the MCP connection, then work
   through the workflow section of the skill.

None of these templates require code — they're plain markdown persona/workflow files. See
[Build a Custom Skill for Your Persona & Market](https://promotiai.com/docs/guides/skills-and-mcp) in the main docs for
the underlying structure if you want to write your own from scratch instead.

## Templates

| Vertical | Best for | Primary KPI |
|---|---|---|
| [E-commerce / DTC](ecommerce-dtc/SKILL.md) | Shopify-style brands, product launches | ROAS |
| [SaaS / B2B Software](saas-b2b/SKILL.md) | Trial signups, demo bookings | SQL count |
| [Local Services](local-services/SKILL.md) | Plumbers, dentists, lawyers — local lead gen | Cost per lead |
| [Restaurant / Hospitality](restaurant-hospitality/SKILL.md) | Foot traffic, reservations, specials | Reservations |
| [Real Estate](real-estate/SKILL.md) | Listing exposure, buyer/seller leads | Qualified leads |
| [Health & Wellness](health-wellness/SKILL.md) | Clinics, coaches, gyms — bookings + trust | Bookings |
| [Education / Online Courses](education-courses/SKILL.md) | Enrollment, webinar signups | Enrollments |
| [Professional Services](professional-services/SKILL.md) | Consulting, accounting, agencies — authority | Consults booked |
| [Creator / Personal Brand](creator-personal-brand/SKILL.md) | Audience growth, sponsorships, drops | Follower growth |
| [Non-Profit / Cause](nonprofit-cause/SKILL.md) | Donor acquisition, awareness, volunteers | Total raised |
| [General / Other](general-other/SKILL.md) | Catch-all — start here if nothing above fits | Engagement (define your own) |

## Contributing

Found a gap, a wrong assumption, or want to add a template for a vertical not listed here? Open a PR — see the
[LICENSE](../LICENSE) for terms.
