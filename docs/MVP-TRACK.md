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

_Tasks 3–7 to follow. Draft by Emma — refine into JIRA epics/stories once scope + handover land._
