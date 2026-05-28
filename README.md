# SimplerDevelopment Skills

Claude Code [skills](https://docs.claude.com/en/docs/claude-code/skills) for working with the [SimplerDevelopment.com](https://simplerdevelopment.com) portal via its MCP server. These skills let Claude draft pages, decks, emails, surveys, booking pages, and full websites against your SimplerDevelopment tenant — all human-in-the-loop with approval URLs before anything goes live.

## Install

Clone into your Claude Code skills directory:

```bash
cd ~/.claude/skills
git clone https://github.com/SimplerDevelopment/simplerdevelopment-skills.git sd
ln -s sd/sd-* .
ln -s sd/CLIENT_QUICKSTART.md .
ln -s sd/SD_DESIGN_PRINCIPLES.md .
```

Or copy the directories directly into `~/.claude/skills/`.

## Prerequisites

1. A SimplerDevelopment.com portal account with an active MCP API key
2. The SimplerDevelopment MCP server connected to Claude Code (see `CLIENT_QUICKSTART.md`)
3. Run `/sd-init` once per workspace to bootstrap `.sd/config.json` (default brand profile, default site, brand snapshot)

## Skills

| Skill | What it does |
|---|---|
| **sd-init** | One-shot bootstrap. Verifies auth, snapshots brand profile + site list, writes `.sd/config.json` so sibling skills don't re-discover tenant on every run. Idempotent — re-run to refresh. |
| **sd-create-page** | Draft a CMS page (blog post, landing page, marketing page). Applies brand profile, reuses existing block templates, returns approval URL. |
| **sd-create-deck** | Draft a multi-slide V2 pitch deck (sales / investor / capabilities). Inherits brand theme. Returns approval URL. |
| **sd-create-email** | Draft an email campaign (announcement / newsletter / nurture). Approval records "ready" stamp; send is a separate explicit action. |
| **sd-create-survey** | Draft a survey / form / intake questionnaire with branching logic, scoring, and recommendation engines. |
| **sd-create-booking-page** | Create a booking page (Calendly-style) or embed an existing one into a CMS page, deck, or email. |
| **sd-create-website** | Compose a multi-page website end-to-end: sitemap, pages via sub-skills, top-nav, booking widget on contact, qualifier survey on funnel page. |
| **sd-build-html-embed** | Author a self-contained HTML experience (single file or multi-file zipped bundle up to 50 MB), upload as an `html-embed` page or single-slide deck. |
| **sd-learn** | Capture user feedback into `.sd/learnings.md` so future runs of sibling `sd-create-*` skills consult it before authoring. |

## Supporting docs

- **`CLIENT_QUICKSTART.md`** — end-to-end onboarding: install MCP, connect Claude, run `sd-init`, author your first page.
- **`SD_DESIGN_PRINCIPLES.md`** — the design / voice / brand patterns these skills follow when authoring content.

## How they work together

```
sd-init  ──┐
           ├──► .sd/config.json  ◄──┐
           │                         │
           ▼                         │
  sd-create-page                     │
  sd-create-deck       ──► approval URL ──► you approve in portal ──► live
  sd-create-email                    ▲
  sd-create-survey                   │
  sd-create-booking-page             │
  sd-create-website  ────────────────┘
           │
           ▼
       sd-learn  ──►  .sd/learnings.md  ──► fed back into next run
```

Every write is staged behind an approval URL — Claude never publishes content without you clicking approve.

## License

MIT. Use them, fork them, send PRs.

## Links

- Portal: https://simplerdevelopment.com
- Org: https://github.com/SimplerDevelopment
- Claude Code skills docs: https://docs.claude.com/en/docs/claude-code/skills
