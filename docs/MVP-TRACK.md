# MVP Track — Task Breakdown

_Client team's MVP build, running a sprint or two behind the Adobe engineering team.
The Adobe team stands up the full foundation; **this team inherits it and extends** —
so most work is reuse + extend, NOT build-from-zero. **Assets (AEM Assets / DAM) is a
separate track** and out of scope here. Grounded in `TASKS-LIST-EDS.md` (bucket IDs cited)._

**7 MVP tasks:** 1) Onboard · 2) Extend Blocks & Design System · 3) Template & Additional
Blocks · 4) Content Authoring & Migration · 5) Additional Integrations · 6) Update Analytics
& SEO · 7) Test, Perf & Go-Live.

---

## Task 1 — Onboard to Existing Setup

_Goal: every dev can run the inherited project locally, push a branch to preview, and edit
in DA. No net-new build — get access, verify, learn._

### Sub-tasks (from sheet §1.1)
| # | Sub-task | Sheet ID | MVP action |
|---|---|---|---|
| 1 | Dev prerequisites | 1.1.1 | Install Node/npm, Git, AEM CLI, Sidekick extension (each machine) |
| 2 | Repo access | 1.1.2 · 1.1.5 | Get added to their GitHub repo + Code Sync (inherit, don't create) |
| 3 | DA.live access | 1.1.8 | Get org/site permissions on their content source |
| 4 | Local dev running | 1.1.9 | `aem up` against their repo — confirm site runs locally |
| 5 | Preview/live flow | 1.1.4 · 1.1.10 | Confirm branch → `.aem.page` / `.aem.live` works |
| 6 | CI / quality gates | 1.1.6 · 1.1.7 | Learn their PR / lint / branching rules (adopt, don't rewrite) |
| 7 | Orientation | — | Walk their block library, conventions, `docs/` |

### Deliverables (Definition of Done)
- [ ] Every dev can clone, run `aem up`, and see the site locally
- [ ] Each dev can push a branch and see it preview at `.aem.page`
- [ ] Team has DA.live edit access and can open/edit a page
- [ ] Onboarding note in `/docs` (repo URL, DA org/site, conventions, who-to-ask)

### Decisions needed
_Already made by the Adobe team — this task just needs them **confirmed + documented** at handover:_
- **D1** authoring = DA.live · **D4/D5** delivery type + Cloud Manager · **D6** topology (single vs repoless)
- **D9** CDN · **D10** CSP model · **D38** live-preview on/off

> ⚠️ The one genuine gate: are D1/D4/D5/D6/D9/D10 settled + written down, or must the client team
> confirm them at handover? Nail this before onboarding is "done."

### Requirements (inputs to unblock)
- GitHub repo access (write) + Code Sync installed
- DA.live entitlement + org/site permissions
- MVP page list + scope (which pages we're building)
- Handover of Adobe team's conventions / block docs

### Blocks
**None.** Onboarding produces no net-new blocks — block work starts in Task 2/3 (§1.2b, §1.3).

---

## Task 2 — Extend Blocks & Design System

_Goal: reuse the Adobe team's existing block library + design tokens; produce the **gap list**
of what's actually net-new for the MVP. **Reuse > extend (variant) > build-new.** Most of §1.2
(design foundation) is inherited — the MVP work is inventory + mapping + the small gap set._

### Sub-tasks (from sheet §1.2, §1.2b, §1.3)
| # | Sub-task | Sheet ID | MVP action |
|---|---|---|---|
| 1 | Inherit design tokens & base styles | 1.2.1 · 1.2.3 · 1.2.4 · 1.2.6 | Reuse Adobe team's tokens/breakpoints/fonts as-is; confirm they cover MVP designs |
| 2 | Learn block architecture & conventions | 1.2.2 · 1.3.8 | Adopt their naming, DA.live format, `classes_`/`groupName_` conventions |
| 3 | Inventory existing blocks | 1.2b.1 | Survey their library + Block Collection / foundation-kit before building anything |
| 4 | Map MVP components → existing | 1.2b.2 | Per MVP component: **reuse as-is / extend (variant) / build-new** |
| 5 | Extend OOTB / existing blocks | 1.3.2 · 1.3.4 | Add variants/style variations to cover MVP needs (no new block) |
| 6 | Build gap blocks only | 1.2b.5 · 1.3.3 | Build **only** what reuse/variant can't cover (the gap list) |
| 7 | A11y baseline on new/changed blocks | 1.2.5 | WCAG 2.1 AA on anything net-new or modified |

### Deliverables (Definition of Done)
- [ ] **Block inventory** — what exists and is reusable (from their lib + collections)
- [ ] **Reuse/extend/build map** — every MVP component classified with a decision
- [ ] **Gap list** — the definitive "build-new" set (feeds Task 3)
- [ ] Extended variants merged + previewing
- [ ] Net-new gap blocks built, a11y-checked, in the library

### Decisions needed
- **D6** site topology (single vs repoless) — drives shared-lib vs local block model
- **D7** design source / brand-token origin
- **Reuse-vs-build threshold** (§1.2b) — when is a variant enough vs. a new block?
- **Base library** to consume/extend (§1.2b.4) — usually inherit the Adobe team's

### Requirements (inputs to unblock)
- **Component inventory** from business (§1.2b.2) — the MVP component list
- **Template count / page designs** for the MVP pages (§1.2b.3)
- Design system / UI kit access (§1.2.1)
- Handover of Adobe team's block library + conventions (from Task 1)

### Blocks
- **Reuse as-is:** inherited from Adobe team's library (count TBD after inventory)
- **Extend (variant):** MVP components close to existing blocks — style/variant only
- **Build-new (the gap list):** the only true dev scope here — sized after §1.2b.2 mapping

> ⚠️ Can't finalize the block scope until the **MVP component inventory + page designs** land.
> Until then the gap list is an estimate, not a commitment.

---

## Task 3 — Template & Additional Blocks

_Goal: assemble the MVP pages from existing + extended blocks, and stand up the small set of
page templates the MVP needs. Also finish the "build-new" gap blocks carried over from Task 2.
EDS content model = **blocks + DA.live sheets/docs** (no CF — that's the Assets track)._

### Sub-tasks (from sheet §1.3, §1.4)
| # | Sub-task | Sheet ID | MVP action |
|---|---|---|---|
| 1 | Build the gap blocks | 1.3.3 · 1.3.4 | Finish the "build-new" set from Task 2's gap list (only what reuse/variant can't cover) |
| 2 | Implement MVP templates | 1.3.5 | Stand up the N page templates the MVP pages need (reuse their patterns first) |
| 3 | Define EDS content structure | 1.4.1 | Blocks + document model for the MVP page types |
| 4 | Structured content (only if needed) | 1.4.2 | DA JSON-Schema sheets for any list/collection content — skip if plain pages |
| 5 | Feature blocks/utilities | 1.3.7 | Only MVP-required extras (e.g. social/OG meta); defer the rest |
| 6 | Author enablement wiring | 1.4.4 · 1.4.5 | Sidekick roles + DA "Prepare" menu (Preflight on) — inherit their config |

### Deliverables (Definition of Done)
- [ ] Gap blocks built, a11y-checked, in the library
- [ ] MVP page templates working in preview
- [ ] Content model documented (block + sheet structure per MVP page type)
- [ ] Author can assemble an MVP page in DA end-to-end

### Decisions needed
- **D15** structured content: DA JSON-Schema vs AEM CF (per type) — MVP default: **DA sheets**
- **D2/D6/D7** authoring/topology/design (inherited from Adobe team)
- **D34/D35** Preflight + Schedule-Publish posture (inherit)

### Requirements (inputs to unblock)
- Content architecture / page-type definitions (§1.4.1)
- Final MVP template count (§1.3.5) + the gap list from Task 2
- MVP page designs

### Blocks
- **Build-new:** the Task 2 gap set (the core dev here)
- **Templates:** N MVP templates (count TBD from §1.3.5 / designs)

---

## Task 4 — Content Authoring & Migration

_Goal: get the MVP pages' content into DA — authored fresh and/or migrated from legacy.
**Media stays lightweight (DA-referenced images); NO DAM / AEM Assets work** — that's the
separate Assets track that integrates in later._

### Sub-tasks (from sheet §1.4, Track 5)
| # | Sub-task | Sheet ID | MVP action |
|---|---|---|---|
| 1 | Author MVP pages in DA | 1.4.x | Build the MVP pages from templates + blocks in DA |
| 2 | Migrate legacy content (if any) | 5.2 · 5.5 | Bulk import via DA Source API + transform, per MVP page set |
| 3 | Lightweight media | — | Reference images directly in DA media; no Assets/DAM pipeline |
| 4 | Migrate redirect rules | 5.4 | Old→new URL map for the MVP pages (feeds Task 6 SEO) |
| 5 | Content parity check | 5.6 | Reconcile migrated pages vs. source |
| 6 | Content mapping doc | 5.7 | Record source→EDS mapping for the MVP set |

### Deliverables (Definition of Done)
- [ ] All MVP pages authored/migrated and previewing
- [ ] Redirect map for MVP URLs
- [ ] Parity check passed (migrated == source, for migrated pages)
- [ ] Content mapping doc

### Decisions needed
- **Migration approach** — re-platform-first vs transform-first (§Track 5); for a small MVP set, often just **author fresh**
- **D25/D26** migration tooling params (only if bulk-migrating)

### Requirements (inputs to unblock)
- MVP page content (copy + images) from business
- Legacy CMS access + current URL/redirect docs (if migrating)
- Page volumes for the MVP set

### Blocks
**None net-new** — consumes Task 3's blocks/templates. (Authoring, not dev.)

---

## Task 5 — Additional Integrations

_Goal: wire only the integrations the MVP actually needs; reuse the Adobe team's patterns.
One system per ticket. Defer everything not required for MVP scope._

### Sub-tasks (from sheet Track 4)
| # | Sub-task | Sheet ID | MVP action |
|---|---|---|---|
| 1 | Analytics/tag integration | 4.2 | Reuse their `aem-martech`/GTM setup; confirm firing on MVP pages |
| 2 | Consent / CMP gating | 4.4 · 4.10 | Reuse consent-check; ensure no martech pre-consent |
| 3 | Search (only if MVP needs it) | 4.1 | Wire search + facets only if in MVP scope |
| 4 | Forms / CRM (only if MVP needs it) | 4.6 | Connect the 1-2 systems the MVP journeys require |
| 5 | Domain/API integration (if needed) | 4.8 · 4.9 | Consume client APIs only where an MVP page depends on them |

### Deliverables (Definition of Done)
- [ ] Analytics verified firing on all MVP pages (dev + prod)
- [ ] Consent gating confirmed (no tags pre-consent)
- [ ] Each in-scope integration working + SIT-tested on MVP pages
- [ ] Out-of-scope integrations explicitly listed as deferred

### Decisions needed
- **Final MVP integration list** — which systems are in-scope THIS phase (§Track 4)
- **D21** analytics stack · **D19** integration ownership (us vs client) · **D20** search tool (if used)

### Requirements (inputs to unblock)
- Integration endpoints + API docs per system (pre-req)
- Client APIs ready + auth confirmed
- Analytics tracking spec / data-layer standard

### Blocks
Integration blocks/utilities only where required (e.g. search-widget) — reuse existing first.

---

## Task 6 — Update Analytics & SEO

_Goal: apply the analytics data layer and SEO essentials to the MVP pages; inherit the Adobe
team's patterns and the enforced performance bar rather than defining them fresh._

### Sub-tasks (from sheet §1.5, §1.6, §1.8)
| # | Sub-task | Sheet ID | MVP action |
|---|---|---|---|
| 1 | Data layer + tag firing | 1.6.1 · 1.6.2 | Apply their data-layer pattern to MVP page events; verify |
| 2 | RUM / consent gating | 1.6.3 · 1.6.5 | Confirm RUM on; consent-gated firing |
| 3 | Redirects | 1.5.1 | Publish the MVP old→new redirects (from Task 4) |
| 4 | Sitemap · robots · canonical | 1.5.2 · 1.5.3 · 1.5.4 | Ensure MVP pages are covered + canonical 2xx |
| 5 | Structured data / OG meta | 1.5.8 | schema.org + social meta on MVP pages |
| 6 | Metadata + 404 | 1.5.10 · 1.5.9 | Metadata rules applied; 404 page live |
| 7 | Perf gate (inherit) | 1.8.1 · 1.8.4 | Confirm MVP pages pass <100KB pre-LCP + Lighthouse-100 CI gate |

### Deliverables (Definition of Done)
- [ ] Analytics firing + verified on MVP pages
- [ ] Redirects, sitemap, robots, canonicals correct for MVP URLs
- [ ] Structured data + OG meta on MVP pages
- [ ] All MVP pages green on the Lighthouse-100 / <100KB gate

### Decisions needed
- **D21** analytics stack · **D12** perf budget enforced (inherited — should already be a CI gate)

### Requirements (inputs to unblock)
- Analytics tracking spec / data-layer standard
- Metadata rules (business) · current redirect/URL docs

### Blocks
**None net-new** — configuration + meta on existing pages/blocks.

---

## Task 7 — Test, Perf & Go-Live

_Goal: QA the MVP pages, hit the perf bar, and launch using the Adobe team's existing go-live
checklist + plumbing (CDN, DNS). Reuse their runbook; don't invent one._

### Sub-tasks (from sheet §6.1, §6.2)
| # | Sub-task | Sheet ID | MVP action |
|---|---|---|---|
| 1 | Functional + smoke tests | 6.1.1 · 6.1.2 | Test MVP journeys; smoke suite per release |
| 2 | Preflight QA | 6.1.3 | DA-native always-on QA on MVP pages |
| 3 | Accessibility test + fix | 6.1.6 | WCAG 2.1 AA pass on MVP pages |
| 4 | Cross-browser / device | 6.1.7 | Chrome/Edge/Safari + tablet/mobile on MVP pages |
| 5 | Performance testing | 6.1.9 · 6.2.5 | Lighthouse 100 mobile+desktop, pre + post go-live |
| 6 | Bug-fix cycle | 6.1.11 | Burn down MVP defects |
| 7 | Go-live (inherit plumbing) | 6.2.1 · 6.2.3 · 6.2.4 | Prod host in Sidekick, content/design QA on `.aem.live`, CDN already set |
| 8 | Launch ops | 6.2.7 · 6.2.8 · 6.2.9 | Notify Adobe on-call, DNS cutover, rollback plan |

### Deliverables (Definition of Done)
- [ ] MVP pages pass functional + a11y + cross-browser
- [ ] Lighthouse 100 (mobile + desktop) pre and post launch
- [ ] Defects triaged/fixed to launch bar
- [ ] MVP pages live on production domain; rollback plan in hand

### Decisions needed
- **D12** perf target (inherited) · **D28** browser/device coverage % · **D30** rollback/DR (RTO/RPO)
- Who owns UAT (client vs team)

### Requirements (inputs to unblock)
- Test data + client test cases · test devices/infra
- CDN ownership (inherited) · client IT for DNS cutover

### Blocks
**None net-new** — validation + launch of existing pages/blocks.

---

## MVP track — what's inherited vs. net-new (summary)

| From Adobe team (reuse) | Net-new for MVP team |
|---|---|
| Provisioned env, repo, Code Sync, DA.live, preview/live | Onboarding + access |
| Design system / tokens + base block library | Gap blocks + variants |
| Go-live plumbing (CDN, redirects, headers), perf gate, analytics/SEO patterns | MVP templates, content, MVP-scoped integrations, apply analytics/SEO/QA to MVP pages |

**Out of scope for MVP:** Track 2 (AEM Assets / DAM) + Track 3 (bridge) — separate track, integrates later.

_Draft by Emma — refine into JIRA epics/stories once scope + handover land._
