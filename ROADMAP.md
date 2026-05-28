# Roadmap

The plan for skills built on top of the SimplerDevelopment.com MCP surface. **Optimized for token economy** — favors small numbers of focused bundles over many atomic skills.

## Why bundles, not 80 atomic skills

Claude Code loads every installed skill's name + description into the system prompt of every conversation. With ~200 SD MCP tools, the naive 1-skill-per-CRUD approach would install 80+ skills, costing **12-15K tokens per turn** even when you're not touching SD. That's 6-7% of a 200K window gone before you type anything, plus a selection-quality drop as the LLM picks between near-duplicate triggers.

Instead, this roadmap groups by domain. One `sd-crm` skill with internal sub-modes ("create-contact", "create-deal", etc.) beats five separate skills. The description stays small; the body handles routing.

**Install-profile token cost (description weight only):**

| Profile | Skills | Approx tokens / turn |
|---|---|---|
| **Minimal** — `sd-init` + `sd-learn` + `sd-find-skill` | 3 | ~500 |
| **Existing atoms (today)** — the 9 shipped | 9 | ~1,500 |
| **Full bundle set** — atoms + all 10 domain bundles + macros | ~24 | ~3,500 |
| **Naive atomic (avoid)** — one skill per MCP tool | 80+ | 12,000–15,000 |

Status legend: ✓ shipped · 🚧 planned · 💡 candidate

Priority: **P0** next batch · **P1** soon · **P2** when justified

---

## Tier 1 · Core (always installed)

Three skills that are universally useful and cheap.

| Skill | What it does | MCP tools | Status |
|---|---|---|---|
| `sd-init` | Bootstrap a workspace: verify auth, snapshot brand profile + site list, write `.sd/config.json`. Idempotent. | `whoami`, `profile_get`, `branding_list_profiles`, `sites_list`, `block_templates_list`, `email_templates_list` | ✓ |
| `sd-learn` | Capture user feedback into `.sd/learnings.md` so future skill runs consult it. | (no MCP) | ✓ |
| `sd-find-skill` | Catalog browser. Tells you what bundles exist, what they cover, and helps install on demand. The escape hatch for the "I want a small footprint" case. | (none — reads this repo's manifest) | 💡 **P0** |

---

## Tier 2 · Atomic creators (already shipped — keep)

These work today, have clean triggers, and people remember them ("draft a page about X"). No reason to collapse into a bundle. Treat them as the always-on creator front-door.

| Skill | What it does | MCP tools | Status |
|---|---|---|---|
| `sd-create-page` | Draft a CMS page with blocks. | `posts_create`, `taxonomies_*`, `block_templates_list` | ✓ |
| `sd-create-deck` | Draft a multi-slide pitch deck. | `decks_create`, `decks_replace_slides`, `decks_publish_all`, `branding_get_profile` | ✓ |
| `sd-create-email` | Draft an email campaign. | `email_campaigns_create`, `email_lists`, `email_templates_list`, `email_segments_*` | ✓ |
| `sd-create-survey` | Draft a survey / form / intake. | `surveys_create`, `surveys_update` | ✓ |
| `sd-create-booking-page` | Create a booking page or embed an existing one. | `booking_pages_*` | ✓ |
| `sd-create-website` | Compose a full multi-page site end-to-end. | `posts_create` (xN), `nav_create`, `sites_update` | ✓ |
| `sd-build-html-embed` | Upload single-file or zipped HTML as an embed page / single-slide deck. | `posts_upload_html(_zip)`, `decks_upload_html(_zip)` | ✓ |

---

## Tier 3 · Domain bundles (one skill per domain, internal sub-modes)

Each bundle is **one** skill. The SKILL.md routes between sub-modes based on the prompt. This is the right home for everything that previously would have been an atomic skill.

### `sd-crm` 💡 **P0**

Everything CRM: contacts, companies, deals, pipelines, custom fields, activities, search.

- **Sub-modes:** `create-contact`, `create-company`, `create-deal`, `move-stage`, `search`, `custom-fields-setup`, `import`, `followup-email`
- **MCP tools:** `crm_contacts_*`, `crm_companies_*`, `crm_deals_*`, `crm_pipelines_*`, `crm_activities_*`, `crm_custom_fields_*`, `crm_custom_field_values_*`, `crm_deal_comments_*`, `crm_deal_artifact_*`, `crm_saved_views_list`, `crm_scoring_rules_list`

### `sd-brain` 💡 **P0**

The Company Brain: notes, meetings, decisions, glossary, relationships, search, review queue, playbooks.

- **Sub-modes:** `note` (incl. decision / glossary templates), `meeting`, `ask`, `dashboard`, `template`, `relationships`, `review-queue`, `saved-search`, `find-expert`, `organize-topics`, `playbook` (create + run), `add-person`
- **MCP tools:** all `brain_*` (~30 tools)

### `sd-store` 💡 **P1**

E-commerce: products, variants, options, inventory, discounts, gift certs, customer care, reviews, orders.

- **Sub-modes:** `create-product`, `create-category`, `create-discount`, `customer-care`, `reviews-moderate`, `orders-report`, `restock`, `issue-gift-certs`, `import`
- **MCP tools:** `store_products_*`, `store_product_options_*`, `store_product_variants_*`, `store_categories_*`, `store_discounts_*`, `store_orders_*`, `store_customers_*`, `store_customer_messages_*`, `store_reviews_*`, `store_settings_get`, `gift_certificates_*`

### `sd-pm` 💡 **P1**

Projects, kanban boards, sprints, time tracking, recurring tasks, card templates.

- **Sub-modes:** `create-project`, `create-board`, `create-card`, `sprint-plan`, `sprint-retro`, `time-report`, `recurring`, `artifact-link`, `card-template`
- **MCP tools:** `projects_*`, `project_members_*`, `kanban_*` (all card / column / checklist / label / template / recurrence tools), `sprints_*`, `my_tasks_list`, `kanban_propose_sprint`

### `sd-tickets` 💡 **P1**

Support / customer-facing ticketing.

- **Sub-modes:** `create`, `triage`, `reply`, `to-card` (promote to kanban), `digest`
- **MCP tools:** `tickets_*`

### `sd-sales` 💡 **P0**

Proposals, contracts, invoices, service catalog, service requests.

- **Sub-modes:** `create-proposal`, `create-contract`, `service-catalog-setup`, `invoice-report`, `proposal-template`
- **MCP tools:** `proposals_*`, `contracts_*`, `invoices_*`, `service_catalog_list`, `service_requests_*`

### `sd-content-ops` 💡 **P0**

Goes deeper on the existing CMS surface — editing, forking, custom post types, block templates, taxonomies, audits. (`sd-create-page` stays as the creator front-door; this bundle owns everything *after* creation.)

- **Sub-modes:** `edit-page`, `fork-page`, `create-cpt`, `cpt-bulk-author`, `create-block-template`, `fork-block-template`, `taxonomy-bootstrap`, `page-audit`
- **MCP tools:** `posts_get/update/fork/delete/list/list_revisions/set_taxonomies`, `post_types_*`, `block_templates_*`, `taxonomies_*`

### `sd-deck-ops` 💡 **P0**

Same idea for decks: editing, forking, generation from data.

- **Sub-modes:** `edit-deck`, `fork-deck`, `deck-from-brain`, `add-slide`, `delete-deck`
- **MCP tools:** `decks_get/update/fork/delete/add_slide/replace_slides/publish_slide/publish_all`

### `sd-email-ops` 💡 **P1**

Goes deeper on email beyond `sd-create-email`: lists, segments, templates, scheduling, A/B forks, recurring newsletters, list hygiene.

- **Sub-modes:** `create-list`, `create-segment`, `email-template`, `fork-campaign`, `schedule`, `newsletter-recurring`, `list-cleanup`
- **MCP tools:** `email_lists_*`, `email_subscribers_*`, `email_segments_*`, `email_templates_*`, `email_campaigns_fork/schedule/send/update/delete`

### `sd-survey-ops` 💡 **P2**

Edits, response handling, forking. Smaller — could fold into `sd-content-ops` if it doesn't justify its own bundle.

- **Sub-modes:** `edit-survey`, `responses-report`, `fork-survey`
- **MCP tools:** `surveys_get/update/fork/list_responses`

### `sd-brand` 💡 **P1**

Brand profiles, audits, contrast checks, messaging.

- **Sub-modes:** `bootstrap` (from URL), `audit`, `check-contrast`, `messaging`, `fork-profile`
- **MCP tools:** `branding_*`

### `sd-site-admin` 💡 **P1**

Site-level admin: nav, domains, env vars, custom code, hosting status.

- **Sub-modes:** `nav-setup`, `nav-restructure`, `add-domain`, `env-vars`, `custom-code`, `hosting-status`, `site-update`
- **MCP tools:** `nav_*`, `website_domains_*`, `website_env_vars_*`, `sites_*`, `hosting_*`

### `sd-ops` 💡 **P2**

Tenant-wide ops: automations, team management, approvals dashboard, AI credit reports, integrations, conversation mining, suggested-project handling.

- **Sub-modes:** `automation`, `team-onboard`, `team-offboard`, `team-audit`, `approvals-dashboard`, `ai-usage-report`, `conversation-mining`, `integration-audit`, `suggested-projects`, `client-snapshot`, `client-update`
- **MCP tools:** `automations_*`, `team_*`, `project_members_*`, `approvals_*`, `ai_conversations_*`, `ai_credits_*`, `integrations_*`, `suggested_projects_*`, `suggested_project_requests_create`, `client_get/update`

### `sd-media` 💡 **P2**

Media library bulk ops. Tiny — could live inside `sd-content-ops` if it doesn't grow.

- **Sub-modes:** `bulk-upload`, `cleanup`
- **MCP tools:** `media_*`

---

## Tier 4 · Macro orchestrators (opt-in)

These compose the bundles + atoms into operator-level workflows. Each is one skill; the description teaches the LLM when to reach for it.

| Skill | What it does | Composes | Priority |
|---|---|---|---|
| `sd-launch-client` | Full new-tenant kickoff: brand → site → nav → 5 starter pages → email list → booking page → 2 sample services/products → welcome automation. | most of Tier 2 + `sd-brand`, `sd-site-admin`, `sd-store`, `sd-email-ops` | **P0** |
| `sd-quote-to-close` | Sales-to-cash in one chat: contact → deal → proposal → contract → invoice → kickoff. | `sd-crm` + `sd-sales` + `sd-pm` | **P0** |
| `sd-quarter-review` | Auto-generated QBR deck + email for a client: closed deals, open pipeline, completed projects, store revenue, Brain highlights. | `sd-crm` + `sd-pm` + `sd-store` + `sd-brain` + `sd-create-deck` + `sd-create-email` | **P1** |
| `sd-monthly-digest` | Monthly tenant digest published as a post + email. | `sd-store` + `sd-crm` + `sd-tickets` + `sd-brain` + `sd-create-page` + `sd-create-email` | **P1** |
| `sd-campaign-bundle` | Marketing campaign as one unit: landing page + email blast + survey + automation + sales-team deck. | `sd-create-page` + `sd-create-email` + `sd-create-survey` + `sd-ops` + `sd-create-deck` | **P1** |
| `sd-handoff-package` | Package a deal/contact's full context (notes, deals, contracts, artifacts) into a portable doc. | `sd-crm` + `sd-brain` + `sd-sales` + `sd-create-page` | **P2** |

---

## Tier 5 · Cross-cutting infrastructure

Not skills, but shared building blocks the skills depend on. Keep in this repo as docs / shared modules.

- **`.sd/config.json` schema** — versioned; `sd-init` writes, others read.
- **Brand snapshot** — cached profile in `.sd/config.json` so bundles don't re-fetch.
- **Approval routing** — `.sd/approvals.json`: per-entity-type rule for auto-stage vs auto-apply (e.g. "always require human approval on `email_campaigns_send`").
- **Telemetry hook** — every skill appends a one-liner to `.sd/skill-runs.log` for `sd-learn` to mine.
- **Bundle convention doc** — `BUNDLE_AUTHORING.md` covering how to structure a sub-mode router inside one SKILL.md without re-implementing skill-selection logic.

---

## Suggested build order

The P0 batch — biggest value-per-token unlock:

1. `sd-find-skill` (P0) — small effort, immediately solves discoverability
2. `sd-crm` bundle (P0)
3. `sd-brain` bundle (P0)
4. `sd-sales` bundle (P0)
5. `sd-content-ops` bundle (P0)
6. `sd-deck-ops` bundle (P0)
7. `sd-launch-client` macro (P0) — depends on the above; the headliner demo

After P0 lands, the platform has end-to-end coverage of the most common operator workflows in ~16 skills total (Tier 1 + Tier 2 atoms + the 6 P0 bundles + 1 P0 macro). Token budget stays around 2.5K per turn.

Then P1 (`sd-store`, `sd-pm`, `sd-tickets`, `sd-email-ops`, `sd-brand`, `sd-site-admin`, `sd-quote-to-close`, `sd-quarter-review`, `sd-monthly-digest`, `sd-campaign-bundle`) when demand justifies each one.

P2 last, or never if nobody asks.

---

## Migration from the previous 80-skill draft

Earlier drafts of this roadmap proposed one skill per atomic operation (~80 skills). Everything from that draft is preserved here, just remapped into bundles:

| Previous atomic skill name | Lives now as |
|---|---|
| `sd-create-contact`, `sd-create-company`, `sd-create-deal`, `sd-pipeline-tracker`, `sd-deal-move-stage`, `sd-crm-import`, `sd-search-crm`, `sd-crm-custom-fields-setup`, `sd-deal-followup-email` | `sd-crm` sub-modes |
| `sd-brain-note`, `sd-brain-meeting`, `sd-brain-ask`, `sd-brain-dashboard`, `sd-brain-template`, `sd-brain-relationships`, `sd-brain-review-queue`, `sd-brain-saved-search`, `sd-brain-record-decision`, `sd-brain-define-term`, `sd-brain-promote-to-document`, `sd-brain-kickoff-initiative`, `sd-brain-add-person`, `sd-brain-find-expert`, `sd-brain-organize-topics`, `sd-brain-create-playbook`, `sd-brain-run-playbook` | `sd-brain` sub-modes |
| `sd-create-product`, `sd-create-store-category`, `sd-product-launch`, `sd-create-discount`, `sd-store-promotion`, `sd-issue-gift-certs`, `sd-store-customer-care`, `sd-store-reviews-moderate`, `sd-store-orders-report`, `sd-product-import`, `sd-inventory-restock` | `sd-store` sub-modes (+ `sd-product-launch` and `sd-store-promotion` are macros that call `sd-store` + `sd-create-page` + `sd-create-email`) |
| `sd-create-project`, `sd-create-kanban-board`, `sd-create-card`, `sd-sprint-plan`, `sd-sprint-retro`, `sd-recurring-tasks`, `sd-time-report`, `sd-card-from-ticket`, `sd-project-artifact-link`, `sd-card-templates` | `sd-pm` sub-modes |
| `sd-create-ticket`, `sd-triage-tickets`, `sd-reply-ticket`, `sd-ticket-to-card`, `sd-ticket-digest` | `sd-tickets` sub-modes |
| `sd-create-proposal`, `sd-create-contract`, `sd-service-catalog-setup`, `sd-service-request-handler`, `sd-invoice-report`, `sd-proposal-templates`, `sd-quote-to-close` (macro stays) | `sd-sales` sub-modes (+ `sd-quote-to-close` macro) |
| `sd-create-list`, `sd-create-segment`, `sd-email-template`, `sd-fork-campaign`, `sd-email-schedule`, `sd-newsletter-recurring`, `sd-list-cleanup` | `sd-email-ops` sub-modes |
| `sd-edit-page`, `sd-fork-page`, `sd-create-cpt`, `sd-cpt-bulk-author`, `sd-create-block-template`, `sd-fork-block-template`, `sd-taxonomy-bootstrap`, `sd-page-audit` | `sd-content-ops` sub-modes |
| `sd-edit-deck`, `sd-fork-deck`, `sd-deck-from-brain` | `sd-deck-ops` sub-modes |
| `sd-edit-survey`, `sd-survey-responses-report`, `sd-fork-survey` | `sd-survey-ops` sub-modes (or folded into `sd-content-ops`) |
| `sd-brand-bootstrap`, `sd-brand-audit`, `sd-brand-check-contrast`, `sd-brand-messaging`, `sd-brand-fork-profile` | `sd-brand` sub-modes |
| `sd-create-automation`, `sd-automation-templates`, `sd-team-onboard`, `sd-team-offboard`, `sd-team-audit`, `sd-approvals-dashboard`, `sd-ai-usage-report`, `sd-conversation-mining`, `sd-integration-audit`, `sd-suggested-projects`, `sd-client-snapshot`, `sd-client-update` | `sd-ops` sub-modes |
| `sd-add-custom-domain`, `sd-env-vars`, `sd-custom-code`, `sd-site-update`, `sd-nav-setup`, `sd-nav-restructure`, `sd-hosting-status` | `sd-site-admin` sub-modes |
| `sd-media-bulk-upload`, `sd-media-cleanup` | `sd-media` sub-modes (or folded into `sd-content-ops`) |
| `sd-bookings-digest`, `sd-bookings-manage` | (small) — fold into `sd-create-booking-page` or into `sd-ops` |

---

## Bundle authoring convention

When building a bundle, structure the `SKILL.md` so it:

1. **Front-loads the sub-mode list** in the description (so the LLM can pattern-match the user prompt to the right sub-mode without loading the body).
2. **Body opens with a sub-mode router** — explicit "if the user says X, do sub-mode Y" rules, then the per-mode instructions.
3. **Shares helpers across sub-modes** — brand snapshot lookup, MCP error handling, approval routing — kept at the top of the body so each sub-mode reads them once.
4. **Logs to `.sd/skill-runs.log`** at the end of each invocation with `{ skill, submode, outcome }`.

A `BUNDLE_AUTHORING.md` doc lives in this repo and walks through a worked example.

---

## How to contribute

1. Pick a 💡 row above.
2. If it's a bundle, scaffold the bundle directory + `SKILL.md` with the sub-mode router pattern.
3. If it's a macro, scaffold the macro directory + a `SKILL.md` that lists which Tier 2/3 skills it expects to be installed (and bails gracefully if not).
4. Update `README.md`'s skill table.
5. Update this `ROADMAP.md` — flip the row from 💡 to ✓ and link the PR.

PRs welcome from anyone.
