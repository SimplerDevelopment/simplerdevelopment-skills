# Roadmap

A map of every skill that *could* exist on top of the SimplerDevelopment.com MCP surface, what's already shipped, and what's still on the table. Use this to plan the next batch.

**Status legend**

- ✓ shipped (in this repo)
- 🚧 planned / in progress
- 💡 candidate — proposed here, not yet built

**Priority legend**

- **P0** — high impact, build next
- **P1** — clear value, build soon
- **P2** — nice-to-have, build when justified
- **Pmacro** — cross-cutting orchestration skill that composes other skills

**MCP coverage at a glance**

The portal currently exposes **~200 MCP tools** across 25+ feature areas. The 9 shipped skills cover ~40 of those tools (~20%). This roadmap covers the rest.

---

## 1. Shipped skills (recap)

| Skill | MCP tools used | Status |
|---|---|---|
| `sd-init` | `whoami`, `profile_get`, `branding_list_profiles`, `sites_list`, `block_templates_list`, `email_templates_list` | ✓ |
| `sd-create-page` | `posts_create`, `taxonomies_*`, `block_templates_list` | ✓ |
| `sd-create-deck` | `decks_create`, `decks_replace_slides`, `decks_publish_all`, `branding_get_profile` | ✓ |
| `sd-create-email` | `email_campaigns_create`, `email_lists`, `email_templates_list`, `email_segments_*` | ✓ |
| `sd-create-survey` | `surveys_create`, `surveys_update` | ✓ |
| `sd-create-booking-page` | `booking_pages_create`, `booking_pages_update` | ✓ |
| `sd-create-website` | `posts_create` (xN), `nav_create`, `sites_update` | ✓ |
| `sd-build-html-embed` | `posts_upload_html(_zip)`, `decks_upload_html(_zip)` | ✓ |
| `sd-learn` | (none — writes `.sd/learnings.md`) | ✓ |

---

## 2. CRM (largest gap)

The portal has 25+ CRM tools and zero shipped skills.

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-create-contact` | Add a contact via interview; resolves company; sets custom fields; logs first activity. | `crm_contacts_create/search/update`, `crm_custom_field_values_set`, `crm_activities_create` | **P0** |
| `sd-create-company` | Add a company; optional bulk-add of related contacts. | `crm_companies_create/search/update` | **P0** |
| `sd-create-deal` | Open a deal, place it on the right pipeline + stage, attach contacts and proposals. | `crm_deals_create`, `crm_pipelines_list`, `crm_deal_artifact_link` | **P0** |
| `sd-pipeline-tracker` | Weekly pipeline digest: deals by stage, stalled deals, scoring outliers. | `crm_deals_list`, `crm_pipelines_list`, `crm_scoring_rules_list` | **P1** |
| `sd-deal-move-stage` | Move a deal to a new stage with reason + activity log. | `crm_deals_move_stage`, `crm_activities_create`, `crm_deal_comments_create` | **P1** |
| `sd-crm-import` | Bulk import contacts/companies from CSV or pasted list; dedupe via search-then-create. | `crm_contacts_search/create`, `crm_companies_search/create`, `crm_custom_field_values_set` | **P1** |
| `sd-crm-custom-fields-setup` | Bootstrap a tenant's custom-field schema from a brief. | `crm_custom_fields_create/list/update`, `crm_custom_field_values_set` | **P2** |
| `sd-search-crm` | Natural-language search across contacts, companies, deals with linkbacks. | `crm_contacts_search`, `crm_companies_search`, `crm_deals_list`, `crm_saved_views_list` | **P1** |
| `sd-deal-followup-email` | Compose a followup email from deal context. | `crm_deals_get`, `crm_activities_create`, `email_campaigns_create` | **P1 / Pmacro** |

---

## 3. Company Brain (knowledge layer)

Big surface, especially around notes, relationships, and the review queue. The `sd-brain-*` skills referenced in some skill catalogs are not in this repo yet — listing them here as the canonical roadmap.

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-brain-note` | Capture a structured note (raw or from a template); auto-tags + links to related entities. | `brain_create_note`, `brain_upsert_note_by_url`, `brain_update_note`, `brain_create_note_from_template` | **P0** |
| `sd-brain-meeting` | Record a meeting (attendees, agenda, outcomes); link to deals/contacts/posts. | `brain_create_meeting`, `brain_link_meeting`, `brain_get_meeting` | **P0** |
| `sd-brain-ask` | Natural-language Q&A over the Brain with answer + cited notes. | `brain_search`, `brain_get_note`, `brain_list_notes` | **P0** |
| `sd-brain-dashboard` | Daily/weekly digest: recent notes, tasks due, review queue, saved-search hits. | `brain_dashboard_summary`, `brain_list_tasks`, `brain_list_review_items` | **P1** |
| `sd-brain-template` | Create / update / list note templates for repeated note shapes (standups, retros, 1:1s). | `brain_create_note_template`, `brain_list_note_templates`, `brain_update_note_template` | **P1** |
| `sd-brain-relationships` | Build / query the relationship graph: link note ↔ contact ↔ deal ↔ company; traverse. | `brain_create_relationship`, `brain_list_relationships`, `brain_update_relationship` | **P1** |
| `sd-brain-review-queue` | Walk the LLM-proposed-notes review queue; bulk approve/reject with reason. | `brain_list_review_items`, `brain_approve_review_item`, `brain_reject_review_item` | **P1** |
| `sd-brain-saved-search` | Create / schedule / consume saved searches; route hits to email or kanban. | `brain_create_saved_search`, `brain_list_saved_searches`, `brain_update_saved_search` | **P2** |
| `sd-brain-record-decision` | Capture ADR-style decision records with rationale and reversibility. | `brain_create_note` (with decision template), `brain_create_relationship` | **P0** |
| `sd-brain-define-term` | Glossary entries: term, definition, aliases, owners. Bulk import supported. | `brain_create_note` + a glossary template | **P1** |
| `sd-brain-promote-to-document` | Convert a cluster of related notes into a polished published doc. | `brain_list_notes`, `brain_search`, `posts_create` | **P2 / Pmacro** |
| `sd-brain-kickoff-initiative` | Spin up a project initiative: scope note + tasks + kanban project + members. | `brain_create_note`, `brain_create_task`, `projects_create`, `kanban_create_card` | **P1 / Pmacro** |
| `sd-brain-add-person` | Add a person to the Brain with their roles, expertise, and existing CRM links. | `brain_create_note`, `brain_create_relationship`, `crm_contacts_search/update` | **P2** |
| `sd-brain-find-expert` | Given a topic, surface the people who know it (per Brain links + notes). | `brain_search`, `brain_list_relationships` | **P2** |
| `sd-brain-organize-topics` | Cluster orphan notes into topic groups; reduce review-queue noise. | `brain_list_notes`, `brain_create_relationship`, `brain_bulk_update_notes` | **P2** |
| `sd-brain-create-playbook` / `sd-brain-run-playbook` | Author and execute repeatable "do X every time Y" playbooks. | `brain_create_note_template`, `brain_create_task`, `automations_create` | **P2** |

---

## 4. Store / E-commerce

Zero skills currently. The portal has full product, order, customer, discount, gift-cert, and review coverage.

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-create-product` | Add a product with variants, options, inventory, categories, taxonomies. | `store_products_create`, `store_product_options_create`, `store_product_variants_create`, `store_categories_create/list`, `store_products_adjust_inventory` | **P0** |
| `sd-create-store-category` | Hierarchical category bootstrap. | `store_categories_create/list` | **P1** |
| `sd-product-launch` | One macro: product + landing page + email campaign + announcement post. | `store_products_create`, `posts_create`, `email_campaigns_create` | **P0 / Pmacro** |
| `sd-create-discount` | Create a discount (code / automatic / BOGO) with date range and limits. | `store_discounts_create`, `store_discounts_toggle/delete` | **P1** |
| `sd-store-promotion` | Discount + email blast + countdown landing page. | `store_discounts_create`, `email_campaigns_create/schedule`, `posts_create` | **P1 / Pmacro** |
| `sd-issue-gift-certs` | Bulk issue gift certificates (sales / loyalty / refund replacement). | `gift_certificates_issue/list` | **P2** |
| `sd-store-customer-care` | Handle inbound customer messages and order issues from one inbox. | `store_customer_messages_list/reply`, `store_orders_add_note`, `store_orders_update_status` | **P1** |
| `sd-store-reviews-moderate` | Walk pending reviews; auto-approve safe, surface flagged for human review. | `store_reviews_list/moderate` | **P2** |
| `sd-store-orders-report` | Daily/weekly orders + revenue + top-products digest. | `store_orders_list`, `invoices_list`, `store_products_list` | **P1** |
| `sd-product-import` | Bulk import from Shopify CSV / Stripe products / pasted list. | `store_products_create` (xN), `store_categories_list` | **P2** |
| `sd-inventory-restock` | Detect low-stock items; raise PO drafts or update inventory. | `store_products_list/get`, `store_products_adjust_inventory` | **P2** |

---

## 5. Project Management (Kanban + Sprints + Projects)

Surface includes full board / card / sprint / time-tracking primitives.

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-create-project` | Spin up a project with members, default board, labels, artifacts. | `projects_create`, `project_members_set`, `kanban_create_column`, `kanban_labels_create` | **P0** |
| `sd-create-kanban-board` | Initial column + label structure + card templates per board. | `kanban_create_column/update_column`, `kanban_labels_create`, `kanban_card_templates_create` | **P0** |
| `sd-create-card` | Create a card with checklist, assignees, dependencies, time estimate. | `kanban_create_card`, `kanban_checklist_add`, `kanban_card_assign`, `kanban_card_add_blocker` | **P1** |
| `sd-sprint-plan` | Propose a sprint; pull from backlog; balance capacity; create sprint and move cards. | `kanban_propose_sprint`, `sprints_create`, `kanban_move_card`, `kanban_list_board` | **P1** |
| `sd-sprint-retro` | At sprint close: completed vs planned, time logged, carry-over, retro note in Brain. | `sprints_list`, `kanban_list_board`, `brain_create_note` | **P1 / Pmacro** |
| `sd-recurring-tasks` | Set up recurring kanban cards (weekly standup, monthly billing, quarterly review). | `kanban_recurrences_create/list/delete` | **P2** |
| `sd-time-report` | Aggregate logged time per project / client / member for invoicing. | `kanban_card_log_time`, `kanban_list_board`, `invoices_get` | **P1** |
| `sd-card-from-ticket` | Convert a support ticket into a kanban card on the right board. | `tickets_get`, `kanban_create_card`, `kanban_card_artifact_link` | **P1 / Pmacro** |
| `sd-project-artifact-link` | Bulk-link CRM / kanban / proposal artifacts onto a project page. | `projects_artifact_link`, `projects_artifacts_list` | **P2** |
| `sd-card-templates` | Reusable card scaffolds (bug, feature, audit). | `kanban_card_templates_create/list/delete` | **P2** |

---

## 6. Tickets / Customer Support

Tickets are first-class but no skill ships yet.

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-create-ticket` | Open a ticket on behalf of a customer; assign, prioritize. | `tickets_create/update` | **P1** |
| `sd-triage-tickets` | Walk open tickets, classify by topic, route to projects, suggest replies. | `tickets_list/get/update`, `kanban_create_card`, `brain_search` | **P1** |
| `sd-reply-ticket` | Compose a brand-voiced reply using prior thread + brain context. | `tickets_get/reply`, `brain_search` | **P1** |
| `sd-ticket-to-card` | Promote ticket → kanban card on engineering board. | `tickets_get`, `kanban_create_card`, `kanban_card_artifact_link` | **P1 / Pmacro** |
| `sd-ticket-digest` | Weekly support digest: volume, SLA breaches, top issues. | `tickets_list` | **P2** |

---

## 7. Proposals · Contracts · Invoices · Service Catalog

Full sales-to-cash loop is exposed, no skills yet.

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-create-proposal` | Compose a branded proposal with line items from the service catalog. | `proposals_create/update/send`, `service_catalog_list`, `branding_get_profile` | **P0** |
| `sd-create-contract` | Generate a contract from a proposal template; e-sign flow; voidable. | `contracts_create/get/void`, `proposals_get` | **P1** |
| `sd-quote-to-close` | One macro: contact → deal → proposal → contract → invoice. | `crm_contacts_search`, `crm_deals_create`, `proposals_create`, `contracts_create`, `invoices_get` | **P0 / Pmacro** |
| `sd-service-catalog-setup` | Bootstrap a productized-service menu with pricing tiers. | `service_catalog_list`, `service_requests_create` (admin), `store_products_create` | **P1** |
| `sd-service-request-handler` | Inbound service requests → triage → ticket or project. | `service_requests_list/create`, `tickets_create`, `projects_create` | **P2** |
| `sd-invoice-report` | Monthly invoice + revenue digest by client/category. | `invoices_list/get` | **P2** |
| `sd-proposal-templates` | Save winning proposals as templates for reuse. | `proposals_get`, `block_templates_create` | **P2** |

---

## 8. Email Marketing (beyond `sd-create-email`)

`sd-create-email` covers campaigns. The rest of the email surface is open.

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-create-list` | Create an email list + initial subscribers + opt-in form. | `email_lists_create`, `email_subscribers_add` | **P1** |
| `sd-create-segment` | Build a smart segment from CRM + behavioral filters. | `email_segments_create/list`, `email_subscribers_list` | **P1** |
| `sd-email-template` | Save / fork / publish reusable campaign templates. | `email_templates_create/list` | **P2** |
| `sd-fork-campaign` | A/B fork a campaign with variant headlines/CTAs. | `email_campaigns_fork/update` | **P2** |
| `sd-email-schedule` | Schedule with timezone-aware send windows. | `email_campaigns_schedule/send` | **P1** |
| `sd-newsletter-recurring` | Auto-drive weekly newsletter from new Brain notes + blog posts. | `brain_list_notes`, `posts_list`, `email_campaigns_create/schedule` | **P1 / Pmacro** |
| `sd-list-cleanup` | Find inactive subscribers / bounces and prune. | `email_subscribers_list/remove/update` | **P2** |

---

## 9. Content (CMS) beyond `sd-create-page`

Pages, taxonomies, CPTs, block templates.

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-edit-page` | Edit / restructure an existing page with surgical block updates. | `posts_get/update`, `posts_list_revisions` | **P0** |
| `sd-fork-page` | Fork a high-performing page as a template for variants. | `posts_fork` | **P2** |
| `sd-create-cpt` | Define a custom post type with fields, code, templates. | `post_types_create/update`, `post_types_fields_create/list`, `post_types_update_template/code` | **P1** |
| `sd-cpt-bulk-author` | Given a CPT (e.g. case-study), bulk-author N posts from a brief or KB. | `posts_create` (xN), `post_types_get`, `crm_custom_field_values_set` | **P1** |
| `sd-create-block-template` | Save a winning block pattern as a reusable template. | `block_templates_create/publish/update` | **P1** |
| `sd-fork-block-template` | Fork-and-customize an existing template per tenant. | `block_templates_fork/get` | **P2** |
| `sd-taxonomy-bootstrap` | Bootstrap category/tag tree for a new site. | `taxonomies_create_category/create_tag/list`, `posts_set_taxonomies` | **P2** |
| `sd-page-audit` | Audit existing pages for SEO, brand voice, broken blocks. | `posts_list/get`, `branding_audit` | **P2** |

---

## 10. Decks beyond `sd-create-deck`

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-edit-deck` | Edit individual slides; reorder; restructure without rebuilding. | `decks_get`, `decks_add_slide`, `decks_replace_slides`, `decks_publish_slide` | **P0** |
| `sd-fork-deck` | Fork a winning deck as a template for sales teams. | `decks_fork` | **P1** |
| `sd-deck-from-brain` | Generate a quarterly-review or capabilities deck from Brain notes + CRM. | `brain_search`, `crm_deals_list`, `decks_create/replace_slides` | **P1 / Pmacro** |
| `sd-deck-html-upload` | Drop a Figma export / hi-fi HTML straight into a deck. | `decks_upload_html/_zip` | ✓ via sd-build-html-embed |

---

## 11. Surveys beyond `sd-create-survey`

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-edit-survey` | Edit existing surveys: add fields, rewire branching, change scoring. | `surveys_get/update` | **P1** |
| `sd-survey-responses-report` | Pull responses, score, route hot leads to CRM. | `surveys_list_responses`, `crm_contacts_create/update`, `crm_deals_create` | **P1 / Pmacro** |
| `sd-fork-survey` | Fork a survey to A/B copy or branching changes. | `surveys_fork` | **P2** |

---

## 12. Bookings beyond `sd-create-booking-page`

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-bookings-digest` | Daily bookings digest with conflicts and prep notes. | `bookings_list/get`, `brain_create_note` | **P1** |
| `sd-bookings-manage` | Cancel / reschedule / update bookings with notification. | `bookings_cancel/update`, `crm_activities_create` | **P2** |

---

## 13. Branding

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-brand-bootstrap` | Generate a brand profile from a URL or pasted brief; color + font sampling. | `branding_create_profile/update_profile` | **P0** |
| `sd-brand-audit` | Audit brand consistency across pages, decks, emails; surface drift. | `branding_audit`, `posts_list`, `decks_list`, `email_campaigns_list` | **P1** |
| `sd-brand-check-contrast` | Run accessibility contrast checks against brand profile colors. | `branding_check_contrast` | **P2** |
| `sd-brand-messaging` | Author / update brand messaging (tone, taglines, value props). | `branding_update_messaging`, `branding_get_messaging` | **P1** |
| `sd-brand-fork-profile` | Fork a brand profile for sub-brands or campaigns. | `branding_create_profile`, `branding_get_profile` | **P2** |

---

## 14. Automations

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-create-automation` | Author a trigger → conditions → actions workflow with NL → spec → review. | `automations_create/update/list/toggle/delete` | **P1** |
| `sd-automation-templates` | Library of common automations (welcome flow, abandoned cart, lead-routing, etc.). | `automations_create` | **P1** |

---

## 15. Site administration (Domains · Env Vars · Custom Code)

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-add-custom-domain` | Add a domain with DNS verification walkthrough. | `website_domains_add/list/remove` | **P1** |
| `sd-env-vars` | Batch set/list/delete env vars per site (analytics IDs, API keys). | `website_env_vars_set/list/delete` | **P1** |
| `sd-custom-code` | Inject site-wide custom HTML/CSS/JS (marketing pixels, A11y widgets). | `sites_update_custom_code`, `sites_get_custom_code`, `sites_publish_custom_code` | **P2** |
| `sd-site-update` | Rename a site, swap default website, change agency white-label colors. | `sites_update`, `client_update` | **P2** |

---

## 16. Site navigation

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-nav-setup` | Build a multi-level top-nav for a new site from page list. | `nav_create/publish_all`, `posts_list` | **P1** |
| `sd-nav-restructure` | Bulk reorg of existing nav: drag tree changes via prompt. | `nav_list/update/publish` | **P2** |

---

## 17. Media

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-media-bulk-upload` | Upload a folder / URL list with auto-tag and category. | `media_register/upload_from_url`, `media_list` | **P1** |
| `sd-media-cleanup` | Find unreferenced media; archive or delete. | `media_list/delete`, `posts_list` | **P2** |

---

## 18. Team & access

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-team-onboard` | Invite a teammate + set role + add to projects + grant MCP token. | `team_invite/update_role`, `project_members_set` | **P1** |
| `sd-team-offboard` | Revoke roles + remove from projects + audit attribution. | `team_remove_member`, `project_members_remove`, `kanban_card_assignees_list` | **P1** |
| `sd-team-audit` | List members, last activity, scope of access. | `team_list_members`, `ai_conversations_list` | **P2** |

---

## 19. Approvals

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-approvals-dashboard` | Walk pending approvals, batch approve safe ones, route risky to human. | `approvals_list/get/approve/reject` | **P1** |
| `sd-approvals-policy` | Set per-entity-type approval policies (auto-approve / always review). | `approvals_list` + portal API extension | **P2** |

---

## 20. AI / Conversations / Credits

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-ai-usage-report` | Monthly AI credits ledger digest by user / feature; cost attribution. | `ai_credits_balance/ledger` | **P1** |
| `sd-conversation-mining` | Pull AI conversations for the period; extract decisions/action items into Brain. | `ai_conversations_list/get`, `brain_create_note`, `brain_create_task` | **P1 / Pmacro** |
| `sd-credit-low-alert` | Trigger when balance falls below a threshold. | `ai_credits_balance` | **P2** |

---

## 21. Integrations

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-integration-audit` | List all integrations, revoke stale ones, surface scope drift. | `integrations_list/revoke` | **P2** |

---

## 22. Hosting

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-hosting-status` | Hosting plan summary per site; usage and limits. | `hosting_list/get` | **P2** |

---

## 23. Client (whole-tenant) operations

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-client-snapshot` | Whole-tenant snapshot: brand, sites, lists, pipelines, products, projects — for audits or duplication. | `client_get`, `branding_list_profiles`, `sites_list`, `email_lists`, `crm_pipelines_list`, `store_products_list`, `projects_list` | **P1** |
| `sd-client-update` | Update client-level settings (timezone, white-label, agency name). | `client_update` | **P2** |

---

## 24. Suggested Projects

| Proposed skill | What it does | MCP tools | Priority |
|---|---|---|---|
| `sd-suggested-projects` | Surface AI-suggested projects; promote to real projects with kickoff. | `suggested_projects_list`, `suggested_project_requests_create`, `projects_create` | **P2 / Pmacro** |

---

## 25. Macro / orchestration skills

These compose multiple sibling skills into one operator-level workflow.

| Proposed skill | What it does | Composes | Priority |
|---|---|---|---|
| `sd-launch-client` | Full new-tenant kickoff: brand → site → nav → 5 starter pages → email list → booking page → 2 sample services/products → welcome automation. | most of the `sd-create-*` family | **P0 / Pmacro** |
| `sd-quarter-review` | Auto-generated QBR for a client: deals closed, deals open, completed projects, store revenue, key Brain decisions. Output is a deck + email. | `crm_*`, `projects_*`, `store_orders_list`, `brain_*`, `decks_create` | **P1 / Pmacro** |
| `sd-monthly-digest` | Monthly tenant digest: orders, leads, completed tickets, brain highlights → email + post. | `store_orders_list`, `crm_*`, `tickets_list`, `brain_*`, `email_campaigns_create` | **P1 / Pmacro** |
| `sd-campaign-bundle` | Marketing campaign as one unit: landing page + email blast + survey + automation + deck for sales team. | `posts_create`, `email_campaigns_create`, `surveys_create`, `automations_create`, `decks_create` | **P1 / Pmacro** |
| `sd-handoff-package` | Package a deal/contact's full context (notes, deals, contracts, artifacts) into a portable doc for handoff. | `crm_*`, `brain_*`, `contracts_get`, `posts_create` | **P2 / Pmacro** |

---

## 26. Cross-cutting infrastructure

Not skills exactly, but supporting building blocks the skills will need.

- **`.sd/config.json` schema versioning** — bump as new skills add fields.
- **Brand profile snapshot** — keep brand colors / fonts / tone close at hand to reduce per-call MCP fetches.
- **Approval routing config** — `.sd/approvals.json` so each skill knows which writes auto-stage vs auto-apply.
- **Telemetry hook** — every skill emits a one-line tracelog to `.sd/skill-runs.log` for `sd-learn` to mine.
- **Skill-versioning convention** — bump `version:` in each `SKILL.md` frontmatter so the portal can compatibility-check.

---

## 27. Suggested build order

Next batch (~5 skills, biggest gap-fill / unlocks the most):

1. `sd-create-contact` (P0)
2. `sd-create-deal` + `sd-create-company` (P0)
3. `sd-brain-note` + `sd-brain-meeting` (P0)
4. `sd-create-product` (P0)
5. `sd-create-project` + `sd-create-kanban-board` (P0)
6. `sd-create-proposal` (P0)
7. `sd-edit-page` and `sd-edit-deck` (P0 — closes the round-trip on existing creators)

Macro on the horizon:

- `sd-launch-client` — the headliner. Once the P0 set lands, this becomes feasible and is the most impressive demo of the SD stack.
- `sd-quote-to-close` — full sales-to-cash flow in one chat.
- `sd-quarter-review` — auto-generated QBR is a great upsell.

---

## How to contribute a skill

1. Pick a row marked 💡 above.
2. Open a draft PR adding a new directory `<skill-name>/SKILL.md` following the existing skill format (frontmatter + body).
3. Wire the SKILL.md so it references the MCP tools listed in the table.
4. Add a row to `README.md`'s skill table.
5. Update this `ROADMAP.md` — flip the row from 💡 to ✓ and link the PR.

PRs welcome from anyone — internal team or external contributors.
