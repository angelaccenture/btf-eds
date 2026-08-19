# EDS Tasks List — Dev Team, by Work Track (JIRA-ready--Angel and Caitlin to review)

_Dev-team work only, organized into WORK TRACKS so each track can be assigned to a separate
team and managed independently. Within a track, each BUCKET = Epic/Feature; each row =
candidate Story/Sub-task once requirements land._

**Legend:** `⚠️ needs-reqs` = blocked on business/PO input · `(dep: …)` = prerequisite/blocker for JIRA linking.

**Docs:** `docs: tech` = needs a technical spec before build · `docs: biz` = needs a business spec/sign-off. _Don't start a spec-flagged item without the doc._

**Who:** 🤖 **Emma** = I can generate/do it (code, config, scaffolding, blocks, schemas, migration tooling, docs) · 👤 **Human** = infra/credentials/sign-offs/client-owned · 🤝 **Both** = I draft, human decides/reviews (design, architecture, integrations, testing strategy).

**Readiness (RAG):** 🟢 **Green** = dev can start TODAY (foundation; DA.live/EDS already decided) · 🟡 **Yellow** = pending a decision/scope call (has a recommendation) · 🔴 **Red** = blocked on environment, a decision, reqs, or a dependency. _Most items are Red — you can't build blocks/templates/content until the environment exists and gating decisions land._

_The **🔑 Decisions Log is at the BOTTOM** (referenced by the `dec: Dxx` column in each track)._

**Work tracks:**
- **TRACK 1 — EDS Platform & Front-End** (git-driven; no servers)
- **TRACK 2 — AEM Assets (Standard / AEMaaCS)** (author/publish, Cloud Manager, dispatcher)
- **TRACK 3 — EDS ↔ AEM Assets Bridge** (DA.live config; connects Track 1 ↔ Track 2)
- **TRACK 4 — Integrations** (one system per ticket)
- **TRACK 5 — Content Migration** (execution)
- **TRACK 6 — Quality, Testing & Go-Live**
- **TRACK 7 — Platform Security & DevOps (shared)**

> Note: Content Modeling splits by track — EDS uses **blocks + DA.live sheets/docs** (Track 1);
> AEM Assets uses **Content Fragment Models / structured content** (Track 2). They are different work.

═══════════════════════════════════════════════════════════════════════════
# TRACK 1 — EDS Platform & Front-End
> 🔑 **Decisions:** D1–D12 (authoring, UE commitment, delivery type, CM register, topology/repoless, design source, headless, CDN, CSP, protect-preview) · D41 (restricted regions) · D42 (dynamic/large → BYOM) — see Decisions Log (bottom).
> 🔒 **Pre-reqs:** Adobe contract signed · GitHub org + Code Sync app · DA.live org/site created
_Git-driven. Branch-based preview (`.aem.page`) / live (`.aem.live`) + DA.live source. No author/publish/dispatcher servers._

## 1.1 — EDS Environments & DevOps Foundation

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 1.1.1 | Dev prerequisites | Node.js + npm · Git · GitHub account · AEM CLI global · Sidekick extension | 🟢 | 🤝 Both | — |
| 1.1.2 | EDS project scaffolding | GitHub repo from `adobe/aem-boilerplate` | 🟢 | 🤖 Emma | — |
| 1.1.3 | Front-end build step _(only if heavy deps)_ | Bundle step for heavy deps (e.g. esbuild for Lit) — EDS is buildless by default; NOT a generic build pipeline (Sitecore/SPA assumption; only real if bundling a dep). | 🟡 | 🤖 Emma | if heavy deps used |
| 1.1.4 | Branch-based preview/live flow | Configure preview (`.aem.page`) / live (`.aem.live`) | 🟡 | 🤝 Both | dep: Code Sync + DA.live org/site live |
| 1.1.5 | Code Sync app | Install GitHub ↔ AEM Code Sync on repo | 🟢 | 🤝 Both | — |
| 1.1.6 | CI for code | Lint/test on PR + branching strategy + guardrails | 🟢 | 🤖 Emma | — |
| 1.1.7 | Code quality metrics gate | — | 🟢 | 🤖 Emma | — |
| 1.1.8 | DA.live content source setup | Create org/site content source | 🟡 | 🤝 Both | dep: DA.live entitlement/access (pre-req) |
| 1.1.9 | Local dev environment | aem-cli / `aem up` | 🟢 | 🤖 Emma | docs: tech |
| 1.1.10 | Live-preview wiring | `?dapreview` IIFE in scripts.js + CORS for `*.preview.da.live` | 🟢 | 🤖 Emma | dec: D38 |
| 1.1.11 | Config Service migration | query.yaml · sitemap.yaml · headers.json · access.json · sidekick.json (replaces .helix/*) | 🟡 | 🤖 Emma | docs: tech |
| 1.1.12 | Register EDS site in Cloud Manager (if chosen) | one-click site create + connect external Git (BYO Git) | 🟡 | 👤 Human | dec: D4, D5 |
| 1.1.13 | EDS Config Pipeline (Cloud Manager) | traffic filters · origin selectors · redirects · domain mappings · SSL  ⚠️ (GA for AEM-backed; Beta for standalone Edge) | 🔴 | 👤 Human | dec: D4, D5 · docs: tech |
| 1.1.14 | Custom HTTP headers | CORS / security response headers | 🟡 | 🤖 Emma | dec: D10 |
| 1.1.15 | Repoless setup (if multi-site) | Config Service schemas (content/folders/robots/cdn/headers/metadata/access/sidekick/index/sitemap); provision extra sites via Admin API (no repo each); drop fstab.yaml/paths.json from git in API mode | 🟡 | 🤝 Both | dec: D6, D9, D25, D26 · docs: tech |
| 1.1.16 | CDN setup | Adobe-managed (`cdn.yaml` via Config Pipeline) OR BYO (origin `main--site--org.aem.live` + `X-Forwarded-Host` + `X-Push-Invalidation`) | 🟡 | 🤝 Both | dec: D4, D5, D9 · docs: tech |
| 1.1.17 | Push invalidation setup + test | Per BYO CDN (Akamai/Cloudflare/Fastly) | 🟡 | 🤝 Both | dec: D9 |
| 1.1.18 | Placeholders | Spreadsheet-driven UI copy | 🟢 | 🤖 Emma | — |

_(dep: Git repo + Code Sync + DA.live org/site)_

## 1.2 — Design System & FED Foundation

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 1.2.1 | Extract brand tokens → EDS CSS custom properties | From UI Kit / design system | 🔴 | 🤖 Emma | reqs: design system · dec: D7 · docs: tech |
| 1.2.2 | EDS block architecture design | library, reuse candidates, naming, DA.live format | 🔴 | 🤖 Emma | dec: D6, D7 · docs: tech |
| 1.2.3 | Multi-brand reusable architecture + theme-based styling | (CSS vars / block classes / theme tokens) | 🔴 | 🤝 Both | dec: D7, D6 · docs: tech |
| 1.2.4 | Responsive breakpoints baseline | — | 🔴 | 🤝 Both | — |
| 1.2.5 | Accessibility-compliant baseline for blocks | (WCAG 2.1 AA) | 🔴 | 🤖 Emma | — |
| 1.2.6 | Font loading strategy | — | 🔴 | 🤝 Both | — |


## 1.2b — Block & Template Inventory / Reuse Mapping
> 🌐 **Global-first:** survey what ALREADY exists before building anything. Reuse > variant > build-new.
> 🔑 **Decision:** which existing library is the base (Block Collection / da-block-collection / our foundation-kit libs / client's existing)? · reuse vs. build threshold?

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 1.2b.1 | Inventory existing blocks | Survey Block Collection + da-block-collection + our foundation-kit/repoless libs + client's existing blocks | 🟢 | 🤖 Emma | — |
| 1.2b.2 | Map required blocks vs. existing | Per component in the inventory: **reuse as-is / extend (variant) / build new** — decide the split | 🔴 | 🤝 Both | reqs: component inventory (biz) · dec: D6 · docs: biz |
| 1.2b.3 | Template inventory & needs | List templates the sites need; map to existing template patterns vs. new | 🔴 | 🤝 Both | reqs: template count · dec: D6 · docs: biz |
| 1.2b.4 | Reuse source decision | Pick the base library to consume/extend (libs-provider / Block Collection / client) | 🟡 | 🤝 Both | dec: D6 |
| 1.2b.5 | Gap list → feeds 1.3 | Output = the "build-new" set that becomes Block Dev (1.3) scope | 🔴 | 🤖 Emma | dep: 1.2b.2/1.2b.3 |

_Emma accelerates: I can run the inventory (Block Collection search, scan repos/libs), do first-pass reuse-vs-build mapping, and draft the gap list — human confirms the calls against real designs._

## 1.3 — Block / Component Development

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 1.3.1 | Map legacy templates/renderings → reusable EDS blocks | — | 🔴 | 🤖 Emma | dep: discovery+design complete · reqs: component inventory · dec: D6 |
| 1.3.2 | Reuse + extend OOTB EDS/Franklin blocks | — | 🔴 | 🤖 Emma | — |
| 1.3.3 | Build custom blocks | (only where reuse/variation can't cover)  ⚠️ needs-reqs (component list + complexity) | 🔴 | 🤖 Emma | reqs:component list + complexity · dec: D6, D7 |
| 1.3.4 | Block style variations / variants | — | 🔴 | 🤖 Emma | dec: D6, D7 |
| 1.3.5 | Implement N reusable templates  ⚠️ needs-reqs | (template count) | 🔴 | 🤖 Emma | reqs:template count · dec: D6, D7 |
| 1.3.6 | Block library governance + versioning | (shared-libs / provider model) | 🔴 | 🤖 Emma | dec: D6, D7 · docs: biz |
| 1.3.7 | Feature blocks/utilities as needed | RSS feed (index/spreadsheet-driven) · Open Graph / social-sharing meta · page-deletion/unpublish process | 🔴 | 🤖 Emma | — |
| 1.3.8 | Block-authoring conventions | model docs before UE models · `classes_` prefix → CSS classes · `groupName_` field grouping · infer props from context · never override max-cells linter | 🔴 | 🤖 Emma | dec: D2, D6, D7 · docs: tech |


## 1.4 — EDS Content Modeling & Authoring
> 🔑 **Decision:** Authoring method (DA / UE / EW) · Structured content: **DA JSON-Schema vs AEM CF** (per content type) · Approval workflow needed (Request Publish)?
_EDS content model = blocks + DA.live sheets/docs (NOT CF Models — that's Track 2)._

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 1.4.1 | Define EDS content structure | (blocks + document model)  ⚠️ needs-reqs (content architecture) | 🔴 | 🤝 Both | reqs:content architecture · docs: biz |
| 1.4.2 | DA-native structured content (WITHOUT AEM CF): design JSON Schema in Schema Editor (`/.da/forms/schemas/`) · set `editor.path`→`da.live/form#` · fetch JSON in blocks · `helix-query.yaml` index · delivered via da-sc worker  ⚠️ needs-reqs (decide: DA vs AEM CF | see Parking Lot) | 🔴 | 🤖 Emma | reqs:decide: DA vs AEM CF — see Parking Lot · dec: D15, D13, D25, D26 · docs: tech |
| 1.4.3 | Universal Editor enablement + component-level UE integration | (component-models/definitions/filters.json) | 🔴 | 🤝 Both | dec: D2, D6, D7, D19 · docs: tech |
| 1.4.4 | Author authentication via Sidekick + roles/permissions | — | 🔴 | 🤝 Both | docs: tech |
| 1.4.5 | DA "Prepare" menu config | Preflight (QA, always-on) · Schedule Publish (feature-flag row) | 🔴 | 🤝 Both | dec: D34, D35 |
| 1.4.6 | Request Publish approval workflow (EA) | Adobe Eng onboarding · plugin + Inbox app · `publish-workflow-config` | 🔴 | 🤝 Both | dec: D18 · docs: biz |
| 1.4.7 | Send-to-Adobe-Target (EA) | Developer Console Target API · `adobe-target` sheet · prepare-menu row | 🔴 | 🤝 Both | dec: D23 |
| 1.4.8 | Media Library enablement | write access to `/.da/media-library` · bulk index for pre-Feb-2026 content | 🔴 | 🤝 Both | dec: D36 |
| 1.4.9 | Author sandbox / training environment | — | 🔴 | 🤝 Both | docs: tech |

> _NOTE: DA-native apps (bulk-operations · content-tree/Traverse · snapshots · translation-projects · version history) are OOTB — author enablement, NOT dev build_

## 1.5 — SEO / Technical Web Standards

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 1.5.1 | Redirects | Legacy URL mapping (old→new) + high-impact backlinks | 🔴 | 🤖 Emma | dep: current redirect rules/URL docs |
| 1.5.2 | Sitemap generation | Auto + discoverable from robots.txt | 🔴 | 🤖 Emma | — |
| 1.5.3 | robots.txt | (allow crawlers; noindex where needed) | 🔴 | 🤖 Emma | — |
| 1.5.4 | Canonical URLs | (rel=canonical; verify 2xx) | 🔴 | 🤖 Emma | — |
| 1.5.5 | hreflang for multilingual  ⚠️ | (if multi-locale) | 🟡 | 🤝 Both | — |
| 1.5.6 | i18n strings | `placeholders.xlsx` per language + `fetchPlaceholders('language')` (no hardcoded strings) | 🟡 | 🤖 Emma | — |
| 1.5.7 | Regional query index with fallback to language index | Link rewriting; per-language sitemaps | 🟡 | 🤝 Both | dec: D24 (if multi-locale) |
| 1.5.8 | Structured data | schema.org + Open Graph / social meta | 🔴 | 🤖 Emma | — |
| 1.5.9 | 404 page + post-launch 404 monitoring | — | 🔴 | 🤖 Emma | — |
| 1.5.10 | Metadata rules | (technical) | 🔴 | 🤖 Emma | docs: biz |


## 1.6 — Analytics & Telemetry (front-end)

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 1.6.1 | Frontend Data Layer for analytics  ⚠️ needs-reqs | (tracking spec / data-layer standard) | 🔴 | 🤖 Emma | reqs:tracking spec / data-layer standard · dec: D21 · docs: tech |
| 1.6.2 | Implement analytics tags + verify firing | (dev/prod) | 🔴 | 🤖 Emma | dec: D21 |
| 1.6.3 | RUM | (Real User Monitoring) instrumentation | 🔴 | 🤖 Emma | — |
| 1.6.4 | Operational Telemetry | (OpTel) instrumentation (before/after perf) | 🔴 | 🤝 Both | dec: D12 |
| 1.6.5 | Consent-gated tag firing | Cookie consent integration | 🔴 | 🤝 Both | dec: D21 |


## 1.8 — Performance Engineering (EDS hard rules — enforce as PR gate)
> 🔑 **Decision:** Adopt Adobe's perf budget as an enforced constraint? · CSP posture (nonce) for RUM/OpTel?

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 1.8.1 | Pre-LCP payload budget **< 100KB | (enforced) | 🔴 | 🤖 Emma | dec: D12 |
| 1.8.2 | E-L-D three-phase loading | (eager / lazy / delayed); hide body until eager done | 🔴 | 🤖 Emma | dec: D12 |
| 1.8.3 | Delay third-party scripts ≥ 3s after LCP; avoid preloads/redirects/CDN script injection | — | 🔴 | 🤖 Emma | dec: D9, D12 · docs: tech |
| 1.8.4 | Lighthouse 100 gate wired into CI | (test every PR via PageSpeed Insights) | 🔴 | 🤖 Emma | dec: D12 |
| 1.8.5 | RUM/OpTel config | `AEM_OPTEL_DISABLED` / `AEM_OPTEL_NONCE` (CSP nonce) via Cloud Manager | 🟡 | 🤖 Emma | dec: D4, D5, D10 |
| 1.8.6 | Font fallback / `size-adjust` to eliminate CLS | (Helix Font Fallback tool) | 🔴 | 🤖 Emma | dec: D12 |


## 1.7 — Experimentation / A-B Testing (EDS native)

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 1.7.1 | Conditional import of exp plugin in scripts.js | (on `daexperiment` param) | 🔴 | 🤖 Emma | dec: D23 |
| 1.7.2 | `sidekick.js` to manage exp import + fire `experimentation` event | — | 🔴 | 🤖 Emma | dec: D23 |
| 1.7.3 | Register in `sidekick.json` (id | experimentation, dev/preview only) | 🔴 | 🤖 Emma | dec: D23 |
| 1.7.4 | Author-facing | run tests from Sidekick UI (enablement) | 🔴 | 🤝 Both | docs: tech |


═══════════════════════════════════════════════════════════════════════════
# TRACK 2 — AEM Assets (Standard / AEMaaCS)
> 🔑 **GATING decision:** ✅ **AEM Assets IS the DAM (D13 = Yes, 2026-08-13)** → Tracks 2 & 3 are IN scope. · **Dynamic Media** yes/no? → 🟡 **TBD (D14)** · **CF** in scope (vs DA structured content)? · **Asset delivery: Media Bus (copy in) vs keep-in-DAM-CDN (rewrite at decoration)?**
> 🔒 **Track pre-reqs:** Adobe contract/licensing · Cloud Manager access · data-residency region confirmed
_Traditional Cloud Service infra. ✅ AEM Assets IS the DAM (D13 = Yes) → this track is active. Ref: docs.da.live/administrators/guides/setup-aem-assets_

## 2.1 — AEM Assets Environments & DevOps Foundation
_Follows Adobe AEMaaCS onboarding journey. NOTE: IMS product profiles ≠ AEM-level groups —
two SEPARATE permission layers (common mistake). Sequence matters (program → environment)._

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 2.1.1 | Contract review | Confirm entitlements/licensing | 🔴 | 👤 Human | gate: Adobe contract |
| 2.1.2 | Admin Console access | sys-admin verifies profile | 🔴 | 👤 Human | — |
| 2.1.3 | Cloud Manager product-profile assignment | (Deployment Manager / Developer roles) | 🟡 | 👤 Human | dec: D4, D5 |
| 2.1.4 | Cloud Manager | create PROGRAM | 🟡 | 👤 Human | dec: D4, D5 |
| 2.1.5 | Cloud Manager | create ENVIRONMENT(s) (dev / stage / prod) | 🟡 | 👤 Human | dec: D4, D5 |
| 2.1.6 | AEMaaCS provisioning | Author + publish instance ✅ (DAM confirmed, D13) · add Dynamic Media only if D14=on | 🔴 | 👤 Human | dec: D13 ✅, D14 (DM tier only) · docs: tech |
| 2.1.7 | Cloud Manager CI/CD pipelines | (AEM code) + Git repo access | 🟡 | 👤 Human | dec: D4, D5 |
| 2.1.8 | IMS users + IMS user groups | (Admin Console) | 🔴 | 👤 Human | docs: tech |
| 2.1.9 | AEM product profiles: `AEM Users` (read-only/Contributors) vs `AEM Administrators` (full) | assign team | 🔴 | 👤 Human | docs: tech |
| 2.1.10 | AEM-level groups & permissions (SEPARATE from IMS product profiles | granular ACLs) | 🔴 | 👤 Human | docs: tech |
| 2.1.11 | SSO / IMS wiring | — | 🔴 | 👤 Human | docs: tech |
| 2.1.12 | IMS technical accounts / API + service credentials | (Adobe Developer Console) · local dev token | 🔴 | 👤 Human | docs: tech |
| 2.1.13 | Dispatcher configuration | — | 🔴 | 👤 Human | docs: tech |
| 2.1.14 | Env var `ADOBE_PROVIDED_CLIENT_ID = darkalley` | (enables DA.live connection; ~10–20 min restart) | 🔴 | 👤 Human | — |

_(dep: Adobe contract signed; Cloud Manager access)_

## 2.2 — DAM / Asset Pipeline
> 🔑 **Decision:** **Dynamic Media** on/off? 🟡 **TBD (D14)** · Ingestion methods (bulk/API/agency)? · Duplicate-handling + clean-up rules?

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 2.2.1 | DAM folder structure | (technical build)  ⚠️ needs-reqs | 🔴 | 🤝 Both | reqs pending · dec: D13 · docs: biz |
| 2.2.2 | Asset naming standards | (technical enforcement)  ⚠️ needs-reqs | 🔴 | 🤝 Both | reqs pending · dec: D13 · docs: biz |
| 2.2.3 | Metadata schemas · metadata profiles · mandatory metadata fields | (AEM Assets config)  ⚠️ needs-reqs | 🔴 | 🤖 Emma | reqs pending · dec: D13, D25, D26 · docs: biz |
| 2.2.4 | Rights management standards · asset expiry standards | (technical config)  ⚠️ needs-reqs | 🔴 | 🤝 Both | reqs pending · dec: D13 · docs: biz |
| 2.2.5 | Asset ingestion | bulk import · API-based upload | 🔴 | 🤝 Both | dec: D13 |
| 2.2.6 | Processing profiles | (image/video) · rendition generation | 🔴 | 🤝 Both | docs: tech |
| 2.2.7 | Metadata extraction | metadata enrichment workflows | 🔴 | 🤝 Both | — |
| 2.2.8 | Duplicate asset handling | ⚠️ · processing failure handling | 🔴 | 🤝 Both | dec: D13 |
| 2.2.9 | Dynamic Media profiles · smart crop · asset distribution ⚠️ | (if in scope) — 🚫 **BLOCKED on D14 (DM decision pending)** | 🟡 | 🤝 Both | dec: D14 ⏳, D13 ✅ |
| 2.2.10 | Publish/approve assets for delivery | (publish tier, or approved→delivery for DM) | 🔴 | 🤝 Both | — |


## 2.3 — Structured Content (Content Fragments)
_AEM-Assets-side structured content. Only if AEM Assets is the structured-content store._

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 2.3.1 | Content Fragment Models (+ up to N fragments)  ⚠️ needs-reqs (CF count; dep | content-architecture workshops) | 🔴 | 🤝 Both | reqs:CF count; dep: content-architecture workshops · dec: D13, D15 · docs: tech |
| 2.3.2 | Experience Fragments ⚠️ | (if in scope) | 🟡 | 🤝 Both | — |
| 2.3.3 | CF permissions | CF translation · CF publishing | 🔴 | 🤝 Both | dec: D13, D15 |
| 2.3.4 | CF Delivery API | (OpenAPI) exposure | 🔴 | 🤝 Both | dec: D13, D15 · docs: tech |
| 2.3.5 | CF Feature Flag enablement | (Cloud Manager toggle) | 🟡 | 🤝 Both | dec: D13, D15, D4, D5 |
| 2.3.6 | Search facets · asset collections | (AEM Assets) | 🔴 | 🤝 Both | dec: D20, D13 |
| 2.3.7 | Taxonomy & AEM tag tree build | Technical build | 🔴 | 🤝 Both | reqs: taxonomy sign-off · docs: biz |


## 2.4 — Asset Workflows & Lifecycle (Standard)
_AEM workflow-engine features — NOT EDS._

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 2.4.1 | Authoring / approval / publishing workflows | (config)  ⚠️ needs-reqs (workflow definition) | 🔴 | 🤝 Both | reqs:workflow definition · docs: biz |
| 2.4.2 | Multi-Site Management setup ⚠️ (if bilingual/MSM in scope) | decide DA-MSM (base+satellite, EA) vs AEM MSM | 🟡 | 🤝 Both | dec: D6, D24 · docs: tech |
| 2.4.3 | Asset lifecycle automation | (archival, retirement, versioning) | 🔴 | 🤝 Both | dec: D13 |
| 2.4.4 | Publishing schedule automation | — | 🔴 | 🤝 Both | — |
| 2.4.5 | User group management & permissions | — | 🔴 | 🤝 Both | — |
| 2.4.6 | Adobe Asset Link (Creative Cloud app extension) 🎯 dep | client IT installs CC extension | 🔴 | 👤 Human | dec: D13 · docs: tech |
| 2.4.7 | Adobe I/O Events | (asset event triggers) | 🔴 | 🤝 Both | dec: D13 · docs: tech |
| 2.4.8 | External system integrations from Assets | (TMS / CDN / etc.) | 🔴 | 🤝 Both | dec: D9, D19 · docs: tech |
| 2.4.9 | Creative Service Workflow ⚠️ | (if in scope) | 🟡 | 🤝 Both | docs: biz |


═══════════════════════════════════════════════════════════════════════════
# TRACK 3 — EDS ↔ AEM Assets Bridge
> 🔑 **Decision:** ✅ Bridge IS in scope (AEM Assets = DAM, D13). · Author mode vs Delivery mode (`author-`/`delivery-` repo prefix)? · Dynamic Media delivery on/off? 🟡 **TBD (D14)**
> 🔒 **Pre-reqs:** Track 2 provisioned · `ADOBE_PROVIDED_CLIENT_ID=darkalley` set · assets published/approved
_DA.live-side wiring that lets EDS consume AEM Assets. No servers — config keys only.
Ref: docs.da.live/administrators/guides/setup-aem-assets_

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 3.1 | Set `aem.repositoryId` in da.live/config | (prefix `author-`/`delivery-` sets mode) | 🔴 | 🤝 Both | docs: tech |
| 3.2 | Optional | `aem.assets.prod.origin` · `aem.assets.prod.basepath` (default `/adobe/assets`) | 🔴 | 🤝 Both | — |
| 3.3 | Optional | `aem.assets.image.type=link` · `aem.asset.dm.delivery=on` · `aem.asset.smartcrop.select=on` · `aem.asset.mime.renditions` | 🔴 | 🤝 Both | — |
| 3.4 | Verify EDS/DA inserts + renders published assets via Delivery API (OpenAPI) | NOT legacy /content/dam/ URLs | 🔴 | 🤝 Both | dec: D13 · docs: tech |
| 3.5 | Cloud-Manager technical account | read access to asset folders (map cloud config to `/conf/<site>`) | 🔴 | 👤 Human | dec: D13 |
| 3.6 | AEM Assets Sidekick plugin | `asset-library` block in sidekick config (asset-selector URL, filters, domain mapping) | 🔴 | 🤖 Emma | dec: D6, D7, D13 · docs: tech |
| 3.7 | Processing profiles | (img 2000×2000 q100 · video MP4) + 20MB limit; reprocess | 🔴 | 🤝 Both | docs: tech |
| 3.8 | Content Fragment overlay (if publishing CF as HTML) | json2html + Mustache templates + Config Service | 🟡 | 🤖 Emma | dec: D13, D15, D6, D7, D25, D26 · docs: tech |

_(dep: Track 2 provisioning + `darkalley` env var set)_

═══════════════════════════════════════════════════════════════════════════
# TRACK 4 — Integrations
> 🔑 **Decision:** Final integration list + which are in-scope this phase? · Search tool (Coveo/Typesense/other)? · Analytics stack? · Are backend APIs owned by us or client?
> 🔒 **Pre-reqs:** Integration endpoints + API docs available · client APIs ready & (un)authenticated confirmed
_One system per ticket. ⚠️ needs-reqs: exact integration list from business._

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 4.1 | Search integration | (e.g. Coveo / Typesense) + facets + indexing/crawl config | 🔴 | 🤝 Both | dec: D20, D19 · docs: tech |
| 4.2 | Analytics/tag integration | `aem-martech` (Adobe WebSDK/Analytics/Tags/ACDL) or `aem-gtm-martech` (GA4+GTM) plugin; phased loading | 🔴 | 🤝 Both | dec: D21, D19 · docs: tech |
| 4.3 | Adobe Target | WebSDK (recommended) vs at.js; per-page `Target: on` metadata | 🔴 | 🤝 Both | dec: D23 |
| 4.4 | CMP consent gating | `consent-check.js`/`consented.js`, map categories (e.g. OneTrust C0004), no martech pre-consent | 🔴 | 🤝 Both | dec: D21 |
| 4.5 | Translation / TMS integration | ⚠️ | 🔴 | 🤝 Both | dec: D19 · docs: tech |
| 4.6 | CRM / marketing | (e.g. Salesforce, Floodlight, Tealium) | 🔴 | 🤝 Both | — |
| 4.7 | Chat / voice | (e.g. Online Chat, Invoca, Verint) | 🔴 | 🤝 Both | — |
| 4.8 | Domain systems (e.g. EHR/Provider Finder; SAP/Billing/Payments) | consume via API | 🔴 | 🤝 Both | — |
| 4.9 | API Gateway/BFF · API management · async message queue | — | 🔴 | 🤝 Both | dep: client APIs ready + documented · dec: D22 · docs: tech |
| 4.10 | Cookie consent / CMP integration (e.g. OneTrust) | feeds consent-gated tag firing (Track 1.6) | 🔴 | 🤝 Both | dec: D21, D19 · docs: tech |
| 4.11 | Native mobile app content consumption | (CF API) + integration support | 🔴 | 🤝 Both | dec: D13, D15, D19 |


═══════════════════════════════════════════════════════════════════════════
# TRACK 5 — Content Migration (execution)
> 🔑 **Decision:** Migration approach — **re-platform-first vs transform-first**? · EMA/AI-accelerated vs manual? · Which sites in which wave?
> 🔒 **Pre-reqs:** Legacy CMS access · content+assets in shared location (e.g. S3) · page/asset volumes confirmed · redirect rules/URL docs

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 5.1 | EMA configured & run | (migration accelerator) | 🔴 | 🤖 Emma | dec: D25, D26 |
| 5.2 | Bulk migration tooling | DA Source API + `crawl()`/update-tree (import, transform via DOMParser, POST back) | 🔴 | 🤖 Emma | dec: D25, D26 · docs: tech |
| 5.3 | Content overlays / BYOM for dynamic/large content (13k+ pages, no manual authoring) | external markup service → EDS-semantic HTML; register overlay + markup URL via Admin API; return real 200/404 (NOTE: folder-mapping is DEPRECATED — use overlays) | 🔴 | 🤖 Emma | dec: D25, D26 · docs: tech |
| 5.4 | Migrate legacy redirect rules | (feeds Track 1.5 redirects) | 🔴 | 🤝 Both | — |
| 5.5 | Content migration execution | (per site/wave)  ⚠️ needs-reqs (page/asset volumes) | 🔴 | 🤝 Both | reqs:page/asset volumes · dec: D13, D25, D26 · docs: tech |
| 5.6 | Content parity / migration validation | (reconcile migrated vs. source) | 🔴 | 🤝 Both | dec: D25, D26 · docs: biz |
| 5.7 | Content mapping document | (technical) | 🔴 | 🤖 Emma | docs: biz |
| 5.8 | Migration report | — | 🔴 | 🤖 Emma | dec: D25, D26 · docs: tech |


═══════════════════════════════════════════════════════════════════════════
# TRACK 6 — Quality, Testing & Go-Live
> 🔑 **Decision:** Browser/device matrix + coverage %? · Perf target (Lighthouse 100?) · Who owns UAT (us/client)? · Rollback + DR targets (RTO/RPO)?
> 🔒 **Pre-reqs:** Test data + client test cases · test infra/devices · CDN ownership · client IT for DNS cutover

## 6.1 — Testing & QA (dev-side)
> 🔑 **Approach:** test by ROI (high failure-impact + low test-cost) — backend logic, reusable libs, critical journeys (login/checkout/forms), integrations. Deprioritize cosmetic/content-heavy UI tests (fragile).

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 6.1.1 | Functional testing | — | 🔴 | 🤝 Both | — |
| 6.1.2 | Sanity test suite | (smoke tests per release) | 🔴 | 🤖 Emma | — |
| 6.1.3 | Preflight QA (DA-native, always-on | config in Track 1.4) | 🔴 | 🤖 Emma | dec: D34 |
| 6.1.4 | Automation testing | (e.g. Selenium; AI-assisted scripts) | 🔴 | 🤖 Emma | — |
| 6.1.5 | Visual Regression Testing | (VRT) | 🔴 | 🤝 Both | — |
| 6.1.6 | Accessibility testing + remediation loop | — | 🔴 | 🤝 Both | — |
| 6.1.7 | Cross-browser / device testing | (Chrome/Edge/Safari + Tablet/iPad/iPhone/Android)  ⚠️ needs-reqs (coverage %) | 🔴 | 🤝 Both | reqs:coverage % · dec: D28 · docs: biz |
| 6.1.8 | SIT | (System Integration Testing) | 🔴 | 🤝 Both | dec: D19 |
| 6.1.9 | Performance testing | Lighthouse 100 target + load/stress at scale | 🔴 | 🤝 Both | dec: D12 |
| 6.1.10 | Regression cycles | — | 🔴 | 🤝 Both | — |
| 6.1.11 | Bug fixing | — | 🔴 | 🤝 Both | — |

_(dep: test data + client-provided test cases + infra/devices)_

## 6.2 — Go-Live / Launch (technical)
_Follows Adobe official go-live checklist (see master doc)._

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 6.2.1 | CDN configuration → point to aem.live | (main); test staging incl. www/APEX redirects | 🔴 | 🤝 Both | dec: D9 · docs: tech |
| 6.2.2 | Push invalidation configured + tested | — | 🟡 | 🤝 Both | dec: D9 |
| 6.2.3 | Production host added to Sidekick config + verify author access from prod domain | — | 🔴 | 🤝 Both | docs: tech |
| 6.2.4 | Content & design QA on .aem.live | — | 🔴 | 🤝 Both | — |
| 6.2.5 | Lighthouse 100 | (mobile + desktop) pre + post go-live | 🔴 | 🤖 Emma | dec: D12 |
| 6.2.6 | Favicon added | — | 🔴 | 🤖 Emma | — |
| 6.2.7 | Notify Adobe engineering on-call | (aemgolives@adobe.com) | 🔴 | 👤 Human | — |
| 6.2.8 | DNS cutover runbook + freeze window | — | 🔴 | 👤 Human | dep: client IT Ops · docs: tech |
| 6.2.9 | Rollback plan | (+ RTO/RPO targets) | 🔴 | 🤝 Both | dec: D30 · docs: tech |
| 6.2.10 | Disaster recovery approach | DA auto-versioning · `/.trash` restore · re-import from aem.live/aem.page (ref: docs.da.live/administrators/reference/disaster-recovery) | 🔴 | 🤝 Both | dec: D30 · docs: tech |
| 6.2.11 | Google Search Console monitoring post-launch | — | 🔴 | 🤝 Both | — |


═══════════════════════════════════════════════════════════════════════════
# TRACK 7 — Platform Security & DevOps (shared across tracks)
> 🔑 **Decision:** SIEM destination? · Secrets manager + rotation policy? · Pen-test required + who runs it?
> 🔒 **Pre-reqs:** Security standards (SAST/DAST/ingress/egress) from client · SIEM endpoint

| ID | Item | Description | RAG | Who | Dep / Decision |
|---|------|-------------|:--:|:--:|---|
| 7.1 | SAST scan setup + integrate into CI  [EDS + AEM] | — | 🔴 | 🤝 Both | dec: D33 |
| 7.2 | DAST scan setup | — | 🔴 | 🤝 Both | dec: D33 |
| 7.3 | Ingress controls | Egress controls | 🔴 | 🤝 Both | — |
| 7.4 | Security hardening | — | 🔴 | 🤝 Both | — |
| 7.5 | Secret configurations + | ⚠️ secrets rotation policy | 🔴 | 🤝 Both | dec: D32 |
| 7.6 | Log forwarding → SIEM | — | 🔴 | 👤 Human | dec: D31 |
| 7.7 | CSP | nonce model (`nonce="aem"` on trusted scripts + `strict-dynamic`; EDS v5+); meta tag → HTTP headers once regression-free  [EDS] | 🔴 | 🤝 Both | dec: D10 · docs: tech |
| 7.8 | Site/preview auth | Token-based protection of preview/live (`secrets.json` + `access/site.json`); CDN forwards Authorization | 🔴 | 🤝 Both | dec: D9, D11, D32 · docs: tech |
| 7.9 | Author auth | role mappings (`access/admin.json` author/publish) + IdP admin consent (Azure/Google/Adobe)  [EDS] | 🔴 | 🤝 Both | dec: D21 · docs: tech |
| 7.10 | IMS technical accounts / API credentials  [AEM] | — | 🔴 | 👤 Human | docs: tech |
| 7.11 | RBAC / product profile + role mapping  [AEM] | — | 🔴 | 👤 Human | docs: tech |
| 7.12 | Monitoring & alerting | — | 🔴 | 🤝 Both | — |
| 7.13 | Audit logging | application log forwarding · access log monitoring | 🔴 | 🤝 Both | dec: D31 |
| 7.14 | Capacity planning | (technical inputs) | 🔴 | 🤝 Both | — |


═══════════════════════════════════════════════════════════════════════════
## REQUIREMENTS NEEDED FROM BUSINESS (inputs — not decisions)
_These are **inputs/sign-offs** the business must provide to unblock tasks (shown as `reqs:` in the tables).
Decisions live in the **Decisions Log** (bottom) — not repeated here._

| Requirement (input) | Unblocks |
|---|---|
| Component inventory + complexity split (Simple/Medium/Complex) | 1.3 (block dev) |
| Template count · CF model count · brand/theme count | 1.3 · 2.3 |
| Page & asset migration volumes | Track 5 (migration) |
| Taxonomy · folder structure · metadata rules (sign-off) | 1.5 · 2.2 · 2.3 |
| Analytics tracking spec / data-layer standard | 1.6.1 |
| Integration endpoints + API docs (per system) | Track 4 |
| Current redirect rules / URL structure docs | 1.5.1 |
| Design system / brand tokens | 1.2.1 |

> Scope/approach **decisions** live in the **Decisions Log** at the bottom (D13, D14, D15, D18, D19, D21, D23, D24).
> ✅ **Resolved: D13 — AEM Assets IS the DAM (2026-08-13)**, so Tracks 2 & 3 are in scope.
> Still open: Dynamic Media? (D14) · Content Hub? · structured-content DA-vs-CF? (D15) · MSM? · Target/Experimentation? · Request Publish? · integration list? · analytics stack?

═══════════════════════════════════════════════════════════════════════════
# 🔑 DECISIONS LOG — answer BEFORE starting each track
_Single place for architects + business to resolve open decisions. Each is repeated inline in
its track. **⛔ = gating** (blocks a whole track). **💡 Emma's Rec** = our default recommendation
(client can override). Fill Decision + Date as they land._

### DT-A — Authoring & Editing
_How authors create/edit/approve content. Drives Track 1 (+2 if UE)._
_Related DA.live-feature decisions living in other tracks: **D23** (Send-to-Adobe-Target, DT-E)._

| # | Decision | Options | Gating? | Track | 💡 Emma's Rec (why) | Decision | Date |
|---|----------|---------|:---:|:---:|---|---|---|
| D1 | **Authoring method** | DA.live / Universal Editor / Experience Workspace | ⛔ | 1 | **DA.live** — fastest, no AEM instance, fits our foundation-kit; UE only if in-context WYSIWYG is a hard requirement | | |
| D2 | **UE commitment** — UE needs AEMaaCS + AEM Site + xwalk | UE vs document/DA | ⛔ | 1,2 | **Document/DA** unless client already owns AEMaaCS + wants in-context editing (UE = big infra + xwalk cost) | | |
| D3 | **Content source** | DA.live / SharePoint / Google Drive | ⛔ | 1 | **DA.live** — purpose-built, versioning, apps, no O365/Drive licensing friction | ✅ **DA.live** | |
| D18 | **Approval workflow?** _(DA.live feature)_ | Request Publish (EA) / none | | 1 | **Request Publish** if governance/regulated (pharma/finance); none for small trusted author teams. _Also a DA.live feature — belongs with D34–D40; pairs with D37 Snapshots/Reviews_ | | |
| D34 | **Preflight (pre-live checklist)** | On / off · default vs custom checks | | 1 | **On** — always-on QA gate (SEO titles/desc, H1, broken/unpublished refs, placeholder text, a11y); customize checks per client. Cheap, catches launch-blockers | | |
| D35 | **Schedule Publish** | On / off | | 1 | **On** if authors need future-dated publishing (campaigns); off for always-manual sites | | |
| D36 | **Media Library** | On / off | | 1 | **On** — central asset browse/insert + usage/alt-text; note pre-Feb-2026 content needs a bulk index | | |
| D37 | **Snapshots / Reviews (content staging)** | On / off | | 1 | **On** if coordinated/time-sensitive launches or review-before-publish needed; pairs with D18 | | |
| D38 | **Live Preview** | On / off | | 1 | **On** — real-time in-context preview; small dev task (`?dapreview` IIFE + CORS). Big author QoL win | | |
| D39 | **Quick Edit** | On / off | | 1 | **On** — in-context visual edit on aem.page; low lift via Sidekick/Author Kit | | |
| D40 | **Authoring Library setup** | Blocks/templates/icons/placeholders | | 1 | **Yes** — build the DA Library so authors self-serve blocks/templates; core to the self-service model | | |

### DT-B — Platform, Topology & Delivery
_Where/how EDS runs and is delivered. Drives Track 1 & 7._

| # | Decision | Options | Gating? | Track | 💡 Emma's Rec (why) | Decision | Date |
|---|----------|---------|:---:|:---:|---|---|---|
| D4 | **EDS delivery type** | with-AEM-env (proxy) vs standalone Edge | ⛔ | 1 | **Standalone Edge** for pure EDS; with-AEM-env only if reusing an existing AEM environment | | |
| D5 | **Register in Cloud Manager?** | Yes / No | | 1 | **Yes** — unlocks Adobe support/SLA + managed CDN; low cost, high safety net for enterprise | | |
| D6 | **Site topology** | Single vs multi-brand / **repoless** | ⛔ | 1 | **Repoless** if >1 site/brand (Adobe-native libs model; only 1st site needs a repo); single otherwise | | |
| D9 | **CDN** | Adobe-managed Fastly vs BYO | ⛔ | 1,7 | **Adobe-managed Fastly** (in-license, zero setup). BYO only if client mandates — and NOT CloudFront/CF-Free (no purge) | | |
| D41 | **Restricted regions** (e.g. China) | in-region HTML/media + China-native CDN vs standard | | 1 | **Standard** unless serving China/restricted markets → then in-region + Alicloud/Tencent/Baidu CDN | | |
| D42 | **Dynamic/large content** | BYOM content-overlays vs authored in DA | | 1,5 | **Authored in DA** for normal volumes; **BYOM overlays** for large/dynamic sets (13k+ pages) — folder-mapping is deprecated | | |

### DT-C — Performance & Security posture
_Non-functional guardrails. Drives Track 1 & 7._

| # | Decision | Options | Gating? | Track | 💡 Emma's Rec (why) | Decision | Date |
|---|----------|---------|:---:|:---:|---|---|---|
| D10 | **CSP enforcement** | meta → HTTP headers (nonce, v5+) | | 1,7 | **Yes, nonce model** — start meta in prod, move to headers once regression-free; enterprise expects a CSP | | |
| D11 | **Protect preview/live?** | site token auth / open | | 7 | **Protect preview** (token auth) for pre-launch; live open unless intranet/gated content | | |
| D12 | **Perf budget enforced?** | <100KB pre-LCP + CI gate / advisory | | 1 | **Enforce** — Lighthouse-100 CI gate + <100KB pre-LCP; it's EDS's whole value prop, don't let it erode | | |

### DT-D — Assets & Content Modeling
_DAM + how structured content is stored/delivered. Drives Track 2 & 3 — ✅ **D13 = Yes (gate satisfied 2026-08-13)**, both tracks unblocked._

| # | Decision | Options | Gating? | Track | 💡 Emma's Rec (why) | Decision | Date |
|---|----------|---------|:---:|:---:|---|---|---|
| D13 | **⛔ Is AEM Assets the DAM?** | Yes (Tracks 2+3) / No | ⛔ | 2,3 | **No** for most — use DA media / existing DAM. Only Yes if client already runs AEM Assets or needs its governance | ✅ **Yes** — AEM Assets IS the DAM. Tracks 2 & 3 in scope. | 2026-08-13 |
| D14 | **Dynamic Media? / Content Hub?** | DM on/off · Content Hub in/out | | 2,3 | **DM off** by default (EDS native opt is fast; on only for smart-crop/advanced). **Content Hub: out** unless client asks | 🟡 **DM: TBD** — client undecided; DM-only tasks stay blocked (2.2.9). Content Hub: out unless asked. | |
| D15 | **Structured content** | DA JSON-Schema vs AEM CF | | 1,2 | **DA JSON-Schema** — no AEM dependency, EDS-native. AEM CF only if AEM Assets already the store | | |
| D16 | **Asset delivery** | Media Bus vs keep-in-DAM-CDN | | 2,3 | **Media Bus (copy-in)** — same-origin, better LCP; only rewrite-in-place if migration volume forbids copy | | |
| D17 | **Bridge mode** | author- vs delivery- prefix | | 3 | **delivery-** (published assets) for prod; author- only for pre-publish preview workflows | | |
| D24 | **Multi-site manager** | DA-MSM vs AEM MSM | | 2 | **DA-MSM** if on DA/repoless; AEM MSM only if already AEMaaCS-based | | |

### DT-E — Design & Front-End approach
_Design system + advanced FE capabilities. Drives Track 1 (+4 for A-B)._

| # | Decision | Options | Gating? | Track | 💡 Emma's Rec (why) | Decision | Date |
|---|----------|---------|:---:|:---:|---|---|---|
| D7 | **Design system source** | Figma / existing / new | | 1 | **Figma → EDS tokens** if a design system exists; else extract from current site during discovery | | |
| D8 | **AEM Headless** | data-heavy only / not used | | 1,4 | **Not used** unless genuinely data-heavy views exist (keep it simple; EDS blocks + JSON cover most) | | |
| D23 | **Personalization / A-B?** | Target · Experimentation | | 1,4 | **Experimentation on** (EDS-native, low lift); Target only if client owns it + wants deep personalization. _Target = DA.live "Send to Adobe Target" (Prepare menu) feature — see DT-A D34–D40; needs adobe-target config sheet_ | | |

### DT-F — Integrations
_Which external systems + who owns the APIs. Drives Track 4._

| # | Decision | Options | Gating? | Track | 💡 Emma's Rec (why) | Decision | Date |
|---|----------|---------|:---:|:---:|---|---|---|
| D19 | **Integration list** | final list + phase scope | ⛔ | 4 | **Lock a phase-1 subset** — defer non-critical integrations to later waves to protect go-live | | |
| D20 | **Search tool** | Coveo / Typesense / other | | 4 | **Reuse client's existing** search if any; else Typesense (lightweight) for new | | |
| D21 | **Analytics stack** | Adobe / GA4+GTM / other | | 4 | **Match client's existing** stack; use the matching aem-martech / aem-gtm-martech plugin | | |
| D22 | **API ownership** | client-owned vs we build | | 4 | **Client-owned APIs** — we consume, don't build backend (keeps scope + risk down) | | |

### DT-G — Migration
_How content moves off legacy. Drives Track 5._

| # | Decision | Options | Gating? | Track | 💡 Emma's Rec (why) | Decision | Date |
|---|----------|---------|:---:|:---:|---|---|---|
| D25 | **Migration approach** | re-platform-first vs transform-first | ⛔ | 5 | **Re-platform-first** — fastest off legacy, transform after landing (lower risk, quicker value) | | |
| D26 | **Migration tooling** | EMA/AI vs manual | | 5 | **EMA/AI-accelerated** for bulk; manual only for high-touch hero pages | | |
| D27 | **Wave grouping** | site→wave mapping | | 5 | **Pilot lowest-risk site first**, then batch by shared templates/brand | | |

### DT-H — Quality & Launch
_Testing scope + launch/rollback. Drives Track 6._

| # | Decision | Options | Gating? | Track | 💡 Emma's Rec (why) | Decision | Date |
|---|----------|---------|:---:|:---:|---|---|---|
| D28 | **Browser/device matrix** | targets + coverage % | | 6 | **Chrome 100% + Edge/Safari 30% + responsive** (matches Adobe/analytics reality; adjust to client analytics) | | |
| D29 | **UAT owner** | us vs client | | 6 | **Client owns UAT** (they own acceptance); we support + fix. Keeps sign-off with the business | | |
| D30 | **Rollback / DR targets** | RTO / RPO | | 6 | **Lean on EDS built-ins** (versioning, /.trash, re-import) + a documented cutover freeze + rollback | | |

### DT-I — Security & Ops (run)
_Logging, secrets, pen-test ownership. Drives Track 7._

| # | Decision | Options | Gating? | Track | 💡 Emma's Rec (why) | Decision | Date |
|---|----------|---------|:---:|:---:|---|---|---|
| D31 | **SIEM destination** | endpoint | | 7 | **Client's existing SIEM** — forward logs there; don't stand up new tooling | | |
| D32 | **Secrets mgmt + rotation** | manager + policy | | 7 | **Config Service secrets** + client's rotation policy; never in git | | |
| D33 | **Pen test** | required? + who | | 7 | **Client/3rd-party pen-tests** prod (Adobe allows anytime); we remediate. SAST/DAST ≠ pen test | | |
