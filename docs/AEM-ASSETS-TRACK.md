# AEM Assets Track — Task Breakdown

_The DAM workstream, run as its own parallel track (Tracks 2 + 3 in `TASKS-LIST-EDS.md`).
✅ **D13 = Yes — AEM Assets IS the DAM (2026-08-13)**, so this track is in scope. It can run
**independent of the site/MVP build** (tasks 1–4), then **plugs into the live EDS site later**
(tasks 5–7). Bucket IDs cited throughout._

**Standing caveat:** 🟡 **D14 (Dynamic Media) still TBD** — only the DM-specific pieces
(smart crop, DM delivery, DM profiles) are blocked; the core DAM is not.

**7 tasks:** 1) Provision AEM Assets · 2) DAM Structure & Governance · 3) Ingestion &
Processing · 4) Workflows & Lifecycle · 5) Wire the EDS↔Assets Bridge · 6) Asset Delivery via
API · 7) Integrate into the Live Site.

> **Pre-reqs (whole track):** Adobe contract/licensing · Cloud Manager access · data-residency
> region confirmed. **Tasks 1–4 = Track 2 (AEM side). Tasks 5–7 = Track 3 (bridge/integration).**

---

## Task 1 — Provision AEM Assets

_Goal: stand up AEMaaCS (author + publish) with the right access model. Mostly 👤 Human/infra._

### Sub-tasks (from sheet §2.1)
| # | Sub-task | Sheet ID | Notes |
|---|---|---|---|
| 1 | Contract / entitlement review | 2.1.1 | Gate — confirm licensing |
| 2 | Admin Console + Cloud Manager access | 2.1.2 · 2.1.3 | Deployment Manager / Developer roles |
| 3 | Create Program + Environment(s) | 2.1.4 · 2.1.5 | dev / stage / prod |
| 4 | Provision AEMaaCS author + publish | 2.1.6 | ✅ DAM confirmed; add DM tier only if D14=on |
| 5 | CI/CD pipelines (AEM code) | 2.1.7 | + Git repo access |
| 6 | Permission model (two layers!) | 2.1.8–2.1.11 | IMS product profiles ≠ AEM-level groups (common mistake) |
| 7 | Technical accounts / API creds | 2.1.12 | Adobe Developer Console + local dev token |
| 8 | Dispatcher + DA connect env var | 2.1.13 · 2.1.14 | `ADOBE_PROVIDED_CLIENT_ID = darkalley` (enables DA connection) |

### Deliverables (DoD)
- [ ] AEMaaCS author + publish live (dev/stage/prod)
- [ ] Access working at BOTH layers (IMS profiles + AEM groups)
- [ ] CI/CD pipeline green · dispatcher configured
- [ ] `darkalley` env var set (unblocks Track 3 bridge)

### Decisions
- **D4/D5** delivery type + Cloud Manager · **D13 ✅** · **D14** (DM tier only, TBD)

### Requirements (inputs)
- Adobe contract signed · data-residency region · team roster for access

### Blocks
**None** (infra/config, not EDS blocks).

---

## Task 2 — DAM Structure & Governance

_Goal: define how assets are organized, named, tagged, and governed. Heavy on business sign-off._

### Sub-tasks (from sheet §2.2, §2.3.7)
| # | Sub-task | Sheet ID | Notes |
|---|---|---|---|
| 1 | DAM folder structure | 2.2.1 | ⚠️ needs biz sign-off |
| 2 | Asset naming standards | 2.2.2 | ⚠️ enforcement rules |
| 3 | Metadata schemas · profiles · mandatory fields | 2.2.3 | AEM Assets config |
| 4 | Rights mgmt + asset expiry standards | 2.2.4 | governance |
| 5 | Taxonomy & AEM tag-tree build | 2.3.7 | needs taxonomy sign-off |

### Deliverables (DoD)
- [ ] Folder structure + naming standard documented & built
- [ ] Metadata schema/profiles live with mandatory fields enforced
- [ ] Rights + expiry rules configured
- [ ] Tag tree / taxonomy built

### Decisions
- **D13 ✅** · **D25/D26** (metadata/migration params, if migrating assets)

### Requirements (inputs)
- Taxonomy · folder structure · metadata rules (business sign-off)
- Rights/expiry policy from business

### Blocks
**None.**

---

## Task 3 — Ingestion & Processing

_Goal: get assets into the DAM and processed into renditions. (DM pieces gated on D14.)_

### Sub-tasks (from sheet §2.2)
| # | Sub-task | Sheet ID | Notes |
|---|---|---|---|
| 1 | Asset ingestion | 2.2.5 | bulk import + API upload |
| 2 | Processing profiles | 2.2.6 | image/video renditions |
| 3 | Metadata extraction/enrichment | 2.2.7 | workflows |
| 4 | Duplicate + failure handling | 2.2.8 | ⚠️ clean-up rules |
| 5 | Publish/approve for delivery | 2.2.10 | publish tier |
| 6 | Dynamic Media profiles / smart crop | 2.2.9 | 🚫 **BLOCKED on D14** |

### Deliverables (DoD)
- [ ] Assets ingested + processed into renditions
- [ ] Duplicate/failure handling in place
- [ ] Assets published/approved for delivery
- [ ] (DM smart-crop — only if D14 = on)

### Decisions
- **D14** (DM on/off — blocks 2.2.9) · ingestion method · duplicate rules

### Requirements (inputs)
- Asset volumes / sources / file types + max sizes
- Assets staged in shared location (e.g. S3) if bulk-migrating

### Blocks
**None.**

---

## Task 4 — Workflows & Lifecycle

_Goal: approval/publish workflows, lifecycle automation, Creative Cloud tie-ins._

### Sub-tasks (from sheet §2.4)
| # | Sub-task | Sheet ID | Notes |
|---|---|---|---|
| 1 | Authoring/approval/publish workflows | 2.4.1 | ⚠️ needs workflow definition |
| 2 | Asset lifecycle automation | 2.4.3 | archival, retirement, versioning |
| 3 | Publishing schedule automation | 2.4.4 | — |
| 4 | User group mgmt & permissions | 2.4.5 | — |
| 5 | Adobe Asset Link (CC extension) | 2.4.6 | client IT installs CC extension |
| 6 | Adobe I/O Events | 2.4.7 | asset event triggers |
| 7 | MSM (only if bilingual/multi-site) | 2.4.2 | DA-MSM vs AEM MSM |

### Deliverables (DoD)
- [ ] Approval/publish workflow live
- [ ] Lifecycle automation (archival/versioning) configured
- [ ] Permissions/groups set · CC Asset Link (if in scope)

### Decisions
- **D6/D24** MSM (if multi-site) · workflow definition · **D13 ✅**

### Requirements (inputs)
- Workflow definition (business) · lifecycle/retention policy

### Blocks
**None.**

---

## Task 5 — Wire the EDS ↔ Assets Bridge

_Goal: DA.live-side config that lets EDS consume AEM Assets. No servers — config keys only.
This is the connection layer (Track 3). **Pre-req: Task 1 done + `darkalley` set + assets published.**_

### Sub-tasks (from sheet §3.1–3.7)
| # | Sub-task | Sheet ID | Notes |
|---|---|---|---|
| 1 | Set `aem.repositoryId` in da.live/config | 3.1 | `author-`/`delivery-` prefix sets mode |
| 2 | Origin / basepath config | 3.2 | `aem.assets.prod.origin` · basepath |
| 3 | Delivery options (link / DM / smartcrop) | 3.3 | DM keys only if D14=on |
| 4 | Cloud-Manager technical account | 3.5 | read access to asset folders |
| 5 | AEM Assets Sidekick plugin | 3.6 | `asset-library` block (selector URL, filters, domain map) |
| 6 | Processing profiles for delivery | 3.7 | img 2000×2000 q100 · video MP4 · 20MB limit |

### Deliverables (DoD)
- [ ] `da.live/config` keys set (mode = delivery- for prod)
- [ ] Asset-selector working in Sidekick for authors
- [ ] Technical account has read access to asset folders

### Decisions
- Bridge mode (author- vs delivery-) · **D14** (DM delivery) · **D6/D7/D13 ✅**

### Requirements (inputs)
- Task 1 complete (`darkalley` env var) · assets published/approved

### Blocks
- `asset-library` sidekick block config (🤖 Emma).

---

## Task 6 — Asset Delivery via API

_Goal: EDS/DA renders published assets through the OpenAPI Delivery API — NOT legacy
`/content/dam/` URLs. Decide the delivery model._

### Sub-tasks (from sheet §3.4, §2.3.4)
| # | Sub-task | Sheet ID | Notes |
|---|---|---|---|
| 1 | Verify insert + render via Delivery API | 3.4 | OpenAPI, not `/content/dam/` |
| 2 | Asset-delivery model decision | (D16) | Media Bus copy-in vs keep-in-DAM-CDN |
| 3 | CF Delivery API (only if CF in scope) | 2.3.4 | structured content via OpenAPI |
| 4 | CF overlay (only if publishing CF as HTML) | 3.8 | json2html + Mustache + Config Service |

### Deliverables (DoD)
- [ ] Published asset inserts + renders in a test EDS page via Delivery API
- [ ] Delivery model chosen + configured (Media Bus vs DAM-CDN)
- [ ] LCP/perf verified for asset-heavy pages

### Decisions
- **D16** asset delivery (Media Bus vs keep-in-DAM-CDN) · **D15** DA-vs-CF (if structured content)

### Requirements (inputs)
- Task 5 bridge wired · sample published assets

### Blocks
- CF overlay templates (🤖 Emma) — only if publishing CF as HTML.

---

## Task 7 — Integrate into the Live Site

_Goal: the "integrate later" moment — repoint the already-live EDS site's media from
DA-hosted images to Assets-delivered URLs, verify, and cut over._

### Sub-tasks
| # | Sub-task | Sheet ID | Notes |
|---|---|---|---|
| 1 | Swap DA media → Assets-delivered URLs | (3.4 applied) | On the live MVP/site pages |
| 2 | Regression: rendering + responsive | 6.1.5 | VRT on affected pages |
| 3 | Performance re-check | 6.1.9 · 1.8.1 | Lighthouse-100 / <100KB still holds |
| 4 | External integrations from Assets | 2.4.8 | TMS / CDN, if in scope |
| 5 | Author enablement | — | Authors now pick assets from DAM via Sidekick |

### Deliverables (DoD)
- [ ] Live pages serving assets from the DAM via Delivery API
- [ ] No visual/responsive regressions · perf gate still green
- [ ] Authors trained on asset-selector workflow

### Decisions
- Cutover timing (which pages/waves) · **D9** CDN (delivery)

### Requirements (inputs)
- Live EDS site (MVP/full) already published · Tasks 5–6 complete

### Blocks
**None net-new** — swaps references on existing pages.

---

## AEM Assets track — how it relates to the site build

| Independent of the site (run anytime) | Connection layer | Integrates into the live site |
|---|---|---|
| T1 Provision · T2 Structure · T3 Ingestion · T4 Workflows | T5 Bridge wiring · T6 Delivery API | T7 Swap live media → DAM delivery |

**Only open decision hanging over the track:** 🟡 **D14 (Dynamic Media)** — blocks DM-specific
pieces only (2.2.9 smart-crop, DM delivery keys), not the core DAM.

_Draft by Emma — refine into JIRA epics/stories once business inputs + D14 land._
