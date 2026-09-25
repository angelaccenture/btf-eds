# Role-Based Enablement Plan: AEM Edge Delivery Services with Experience Workspace

**Status:** Reviewed 2026-09-25 against the live aem.live docs. Changes from the original draft, and the questions still open for the Adobe TAM, are listed at the end.

**Links:** aem.live links were checked on 2026-09-25. Links for AEM Assets, Experience League, video hubs, and webinars were not carried over from the original Word document; copy them from there (marked _link: see original_).

## Read this first: three things that clear up most of the confusion

1. **Experience Workspace (EW) is Document Authoring (DA), upgraded.** Adobe: *"This is an upgrade, not a migration… Nothing you've built in DA breaks."* EW adds a visual editor and an AI Assistant. Some Adobe pages still say "Document Authoring"; for this client, read DA as EW. See [Document Authoring is now Experience Workspace](https://www.aem.live/docs/ew/da-is-ew).
2. **AEM Sites with the Universal Editor is a different authoring model.** Material about authoring inside AEM as a Cloud Service (Universal Editor, AEM Sites as the content source, AEM site templates) doesn't apply to this client. Adobe: EW *"replaces traditional AEM authoring for new projects"*. See [About Experience Workspace](https://www.aem.live/docs/ew/about).
3. **Permissions come from two places.** EW content access (read/write) is set with Adobe Admin Console groups plus the EW config sheet. Preview and publish permissions come from Edge Delivery Services, not EW. See [EW permissions](https://www.aem.live/docs/ew/administering/permissions) and [Security](https://www.aem.live/docs/security).

**Personas**
- **Business:** Content Author · Content Reviewer/Approver · Publisher · CMS Administrator · Content Manager
- **Technical:** Front-End Developer/Engineer · Platform Administrator/DevOps · Architect/Technical Lead
- **DAM:** DAM User · DAM Librarian · DAM Administrator

---

## Part A: Business enablement path

| Role | Primary responsibility | Suggested effort |
|---|---|---|
| Content Author | Creates, edits, and maintains web content in Experience Workspace. | 6-8 hours |
| Content Reviewer / Approver | Reviews and approves content before it moves to publishing. | 3-4 hours |
| Publisher | Controls when and where approved content goes live. | 3 hours |
| CMS Administrator | Administers and operates the authoring environment: site and authoring configuration, the authoring library, permissions in Experience Workspace and Edge Delivery, publishing processes, and operational governance. | 8-12 hours |
| Content Manager | Owns content governance, standards, workflow, and lifecycle. | 6-8 hours |

### Foundation for all business personas

- [About Experience Workspace](https://www.aem.live/docs/ew/about): what EW is and what it can do.
- [Document Authoring is now Experience Workspace](https://www.aem.live/docs/ew/da-is-ew): why some material still says "DA".
- [Orientation](https://www.aem.live/docs/ew/orientation): a tour of the workspace.
- Live EDS demo by Angel Andreas.

The platform architecture overview moved to the technical track; it's too technical for a business audience.

### Content Author

**Role:** Drafts, edits, and maintains web content in Experience Workspace.

**Learning objectives**
- Understand the EDS authoring model: pages made of sections, blocks, media, and metadata.
- Navigate Experience Workspace.
- Use sections, blocks, media, and metadata.
- Use the Assistant and Live Preview.
- Preview content and submit it for review.

**Documentation**
- [Authoring with Experience Workspace](https://www.aem.live/docs/ew/authoring): authoring, media, publishing, snapshots, and versions.
- [Authoring pages](https://www.aem.live/docs/ew/authoring/editing-docs) · [Adding media](https://www.aem.live/docs/ew/authoring/adding-media) · [Live Preview](https://www.aem.live/docs/ew/authoring/live-preview) · [Assistant panel](https://www.aem.live/docs/ew/authoring/assistant)

**Tutorials and videos**
- Experience Workspace, AEM Authoring & EDS: recorded authoring demonstration (_link: see original_). Check that it shows the current EW editor.

**Hands-on lab**
1. Edit text and media on an assigned page.
2. Insert an approved image from AEM Assets using the asset picker.
3. Add or rearrange an approved block.
4. Validate metadata and accessibility fields.
5. Preview, then submit for review with [Request Publish](https://www.aem.live/docs/ew/administering/request-publish).

**Suggested effort:** 6-8 hours

### Content Reviewer / Approver

**Role:** Reviews quality, compliance, and readiness before publication.

**Learning objectives**
- Understand approval gates.
- Review content, assets, metadata, links, and accessibility.
- Use versions, snapshots, and the approval workflow.
- Communicate approval decisions.

**Documentation**
- [Authoring with Experience Workspace](https://www.aem.live/docs/ew/authoring)
- [Request Publish](https://www.aem.live/docs/ew/administering/request-publish): EW's approval workflow.
- [Preflight](https://www.aem.live/docs/ew/administering/preflight) · [Version history](https://www.aem.live/docs/ew/authoring/version-history) · [Snapshots](https://www.aem.live/docs/ew/authoring/snapshots)

**Hands-on lab**
1. Review a draft against the content checklist and run Preflight.
2. Request and verify corrections.
3. Approve and hand off to the publisher.

**Suggested effort:** 3-4 hours

### Publisher

**Role:** Controls the release of approved content.

**Learning objectives**
- Understand preview and live destinations.
- Verify approval evidence.
- Validate approved content before release.
- Follow release and remediation procedures, including scheduled publishing and unpublishing.

**Documentation**
- [Publishing content](https://www.aem.live/docs/ew/authoring/publishing): preview, publish, and unpublish.
- [Request Publish](https://www.aem.live/docs/ew/administering/request-publish) · [Schedule Publish](https://www.aem.live/docs/ew/administering/schedule-publish) · [Preflight](https://www.aem.live/docs/ew/administering/preflight)

**Hands-on lab**
1. Publish to preview.
2. Complete pre-release validation with Preflight.
3. Publish using the client's procedure.
4. Verify the live page and rehearse remediation (unpublish or restore a version).

**Suggested effort:** 3 hours

### CMS Administrator

**Role:** Administers and operates the authoring environment: site and authoring configuration, the authoring library, permissions, publishing processes, and operational governance.

**Learning objectives**
- Understand EDS and Experience Workspace setup.
- Manage the authoring library and site configuration.
- Coordinate access: EW read/write permissions and Edge Delivery preview/publish roles.
- Support governance and troubleshooting.

**Documentation**
- [About Experience Workspace](https://www.aem.live/docs/ew/about): prerequisites and configuration concepts.
- [Administering Experience Workspace](https://www.aem.live/docs/ew/administering) · [Configs](https://www.aem.live/docs/ew/administering/configs) · [Permissions](https://www.aem.live/docs/ew/administering/permissions)
- [Set up library](https://www.aem.live/docs/ew/administering/set-up-library) · [Multi-Site Manager](https://www.aem.live/docs/ew/administering/multi-site-manager) (if the client runs more than one site)

**Tutorials**
- [Getting Started – Developer Tutorial](https://www.aem.live/developer/tutorial): project setup with Document Authoring (EW) as the content source.

**Hands-on lab**
1. Validate prerequisites and access.
2. Review a non-production site and its authoring library.
3. Map personas to least-privilege access, in two parts: EW read/write in the config sheet, and preview/publish roles in Edge Delivery.
4. Test preview and publishing permissions with representative accounts.

**Suggested effort:** 8-12 hours

### Content Manager

**Role:** Owns content governance, standards, workflow, and lifecycle.

**Learning objectives**
- Define standards and ownership.
- Establish intake, review, approval, publication, and maintenance processes.
- Align platform roles to responsibilities.
- Measure readiness and adoption gaps.

**Documentation**
- [About Experience Workspace](https://www.aem.live/docs/ew/about) · [Authoring with Experience Workspace](https://www.aem.live/docs/ew/authoring)
- [Request Publish](https://www.aem.live/docs/ew/administering/request-publish): the approval workflow to build governance around.

**Hands-on lab**
1. Map the lifecycle from intake to retirement.
2. Define a RACI and a quality checklist.
3. Run one page through the complete process.

**Suggested effort:** 6-8 hours

### Business webinars and recorded sessions (optional)

Confirm these with the TAM; they may predate Experience Workspace (_links: see original_).
- Optimizing Content Delivery: Unlocking the Power of Edge Services
- Getting Started with AEM Authoring and Edge Delivery
- Experience Manager Edge Delivery Services Overview

---

## Part B: Technical enablement path

| Role | Role focus |
|---|---|
| Front-End Developer / Engineer | Build and maintain the EDS front end: project structure, sections, blocks, widgets, metadata-driven behaviour, integrations, and performance. |
| Platform Administrator / DevOps | Administer, provision, and govern the Adobe platform: product entitlements, user provisioning, product profiles, user groups, and access through the Adobe Admin Console. Configure and operate the EW and EDS environment. |
| Architect / Technical Lead | Own architectural decisions across content structure, block and template strategy, integrations, security, CDN/WAF, performance, and technical governance. |

### Foundation for all technical personas

- [AEM.live documentation hub](https://www.aem.live/docs/)
- [Architecture](https://www.aem.live/docs/architecture): layers, content and code sources, preview, publishing, CDN delivery, and push invalidation.
- [About Experience Workspace](https://www.aem.live/docs/ew/about) · [Document Authoring is now Experience Workspace](https://www.aem.live/docs/ew/da-is-ew)

**Scope guardrail:** use resources for Edge Delivery Services and Experience Workspace. Skip material for AEM Sites with the Universal Editor.

### Front-End Developer / Engineer

**Learning objectives**
- Understand the EDS project anatomy and development workflow.
- Build blocks that align with the authoring model and the client's standards.
- Tell content-oriented blocks apart from application-like widgets.
- Use spreadsheets and JSON where they fit.
- Apply development collaboration, performance, and operational telemetry guidance.

**Documentation**
- [Getting Started – Developer Tutorial](https://www.aem.live/developer/tutorial) · [Developing for Experience Workspace](https://www.aem.live/docs/ew/developing)
- [The Anatomy of a Project](https://www.aem.live/developer/anatomy-of-a-project) · [Markup, Sections, Blocks, and Auto Blocking](https://www.aem.live/developer/markup-sections-blocks) · [Exploring blocks](https://www.aem.live/docs/exploring-blocks)
- [Spreadsheets and JSON](https://www.aem.live/developer/spreadsheets) · [Web performance](https://www.aem.live/developer/keeping-it-100) · [Development collaboration and good practices](https://www.aem.live/docs/dev-collab-and-good-practices)
- [Security](https://www.aem.live/docs/security) · [EW configs](https://www.aem.live/docs/ew/administering/configs)

**Tutorials and videos**
- Edge Delivery Services Video Hub (_link: see original_). Confirm with the TAM which videos are current.

**Practical validation**
1. Create or clone a non-production EDS project.
2. Build one client-relevant block with an explicit content model.
3. Apply CSS and JavaScript while validating authoring behaviour in EW.
4. Implement one spreadsheet/JSON or widget scenario, only if required.
5. Run performance checks and document deviations from the client's standards.

**Completion evidence:** a working demonstration, documented decisions, and follow-up actions for the implementation.

### Platform Administrator / DevOps

**Learning objectives**
- Understand EDS architecture and operational responsibilities.
- Configure Experience Workspace organization and site settings.
- Support library configuration, access controls, and governance.
- Connect Experience Workspace to AEM Assets.
- Understand CDN options, push invalidation, and security guidance.
- Prepare a repeatable go-live and operational-readiness checklist.

**Documentation**
- [Architecture](https://www.aem.live/docs/architecture) · [Security](https://www.aem.live/docs/security) · [FAQ](https://www.aem.live/docs/faq)
- [EW configs](https://www.aem.live/docs/ew/administering/configs) · [EW permissions](https://www.aem.live/docs/ew/administering/permissions) · [Set up AEM Assets](https://www.aem.live/docs/ew/administering/set-up-aem-assets)
- [Go-live checklist](https://www.aem.live/docs/go-live-checklist) · [Picking the right CDN](https://www.aem.live/docs/cdn-guide) · [BYO CDN setup](https://www.aem.live/docs/byo-cdn-setup) · [Adobe Managed CDN](https://www.aem.live/docs/byo-cdn-adobe-managed)

**Tutorials**
- [Getting Started – Developer Tutorial](https://www.aem.live/developer/tutorial), or [Import EDS projects into Experience Workspace](https://www.aem.live/docs/ew/administering/import) for an existing project.

**Practical validation**
1. Configure a non-production organization or site setting.
2. Validate library and permission design against least-privilege expectations.
3. Connect a non-production site to AEM Assets and confirm authors can insert assets.
4. Document the selected CDN model and invalidation flow.
5. Review security and rate/volume-limit considerations.
6. Create a go-live checklist with owners, validation evidence, and escalation paths.

**Completion evidence:** a working demonstration, documented decisions, and follow-up actions for the implementation.

### Architect / Technical Lead

**Learning objectives**
- Explain the complete EDS publishing and delivery architecture.
- Define decision principles for blocks, widgets, content models, the library, and templates.
- Evaluate integration and micro-frontend patterns against EDS constraints.
- Define security, CDN, invalidation, and performance strategies.
- Establish architecture governance and implementation guardrails.

**Documentation**
- [Architecture](https://www.aem.live/docs/architecture) · [About Experience Workspace](https://www.aem.live/docs/ew/about)
- [Exploring blocks](https://www.aem.live/docs/exploring-blocks) · [Security](https://www.aem.live/docs/security) · [EW configs](https://www.aem.live/docs/ew/administering/configs)
- [Building integrations](https://www.aem.live/developer/integrations) · [Go-live checklist](https://www.aem.live/docs/go-live-checklist) · [Indexing](https://www.aem.live/developer/indexing) · [Web performance](https://www.aem.live/developer/keeping-it-100)

### Technical webinars and recorded sessions

Confirm these with the TAM (_links: see original_).
- Optimizing Content Delivery: Unlocking the Power of Edge Services
- Getting Started with AEM Authoring and Edge Delivery
- Experience Manager Edge Delivery Services Overview

---

## Part C: AEM Assets (DAM) enablement path

| Role | Primary responsibility | Core capabilities | Recommended AEM experience |
|---|---|---|---|
| DAM User | Searches for and reuses approved assets in day-to-day work. | Browse, search, filter, preview, download, share, use approved renditions. | Assets view and/or Content Hub, per the client's access design. |
| DAM Librarian | Organizes, tags, curates, and maintains the asset library. | Metadata quality, taxonomy, collections, lifecycle, review, governance, reporting. | Assets view plus Admin view where stewardship tasks require it. |
| DAM Administrator | Manages DAM configuration, permissions, metadata structures, and operational controls. | User groups, permissions, schemas, profiles, workflows, integrations, monitoring. | Admin view and Adobe Admin Console; Assets view configuration as applicable. |

### How the DAM connects to web authoring

Experience Workspace authors insert images through an **AEM Assets picker** inside the editor. Setup needs AEM as a Cloud Service with a publish instance or Dynamic Media, a Cloud Manager environment setting, and EW site configuration. See [Set up AEM Assets](https://www.aem.live/docs/ew/administering/set-up-aem-assets). That page doesn't mention Content Hub as a source; see the TAM questions below.

### Foundation for all DAM personas

_Links: see original._
- AEM Assets as a Cloud Service overview: core DAM capabilities, ingestion options, asset management, and persona-based experiences.
- AEM Assets videos and tutorials: tutorial hub for Assets view and Admin view workflows.
- Best practices for getting started with AEM Assets: content strategy, folder structure, metadata, taxonomy, permissions, and governance.
- Governance best practices for AEM Assets: policies, roles, standards, workflows, and lifecycle governance.
- Search and discovery tutorial: search and filter concepts across Assets view and Admin view.
- Premium Learning: Manage and Deliver Digital Assets Using AEM (foundational course).
- Webinar: From Content Chaos to Content Reuse: How Marketing Teams Move Faster with AEM Assets.

### DAM User

**Role:** Searches for and reuses approved digital assets in day-to-day work.

**Learning objectives**
- Understand the purpose of AEM Assets and the approved-asset lifecycle.
- Navigate the assigned asset experience.
- Search by keyword, metadata, path, file type, and filters.
- Check details, versions, renditions, rights, and usage guidance before download.
- Download or share the correct approved rendition without creating duplicates.

**Documentation and tutorials** (_links: see original_)
- Content Hub overview: the Assets view walkthrough, plus browse, search, preview, and download tutorials.
- Search and discovery: keyword search, filters, saved searches, and refining results.

**Hands-on lab**
1. Locate an approved asset using keyword search and metadata filters.
2. Inspect metadata, rights, status, renditions, and version information.
3. Download the approved rendition and record the intended use.
4. Show what to do when an asset is missing, expired, restricted, or duplicated.

**Premium Learning and webinars:** AEM Assets Content Hub: Intelligent Discovery and Governed Distribution for Enterprises (webinar).

**Suggested effort:** 3-4 hours

### DAM Librarian

**Role:** Organizes, tags, curates, and maintains assets in the library.

**Learning objectives**
- Apply the client's metadata, taxonomy, naming, and folder standards consistently.
- Curate assets, collections, and search experiences for discovery and reuse.
- Maintain asset quality across ingestion, review, approval, expiry, archival, and deletion.
- Identify duplicates, incomplete metadata, rights risks, and governance exceptions.
- Partner with administrators on schemas, permissions, workflows, and controlled-vocabulary changes.

**Documentation and tutorials** (_links: see original_)
- Metadata best practices for AEM Assets.
- Taxonomy and tagging best practices.
- Governance best practices for AEM Assets.
- AEM Assets videos and tutorials: metadata, collections, tasks, asset management, and Admin view workflows.
- Executive guide to success with AEM Assets: librarian responsibilities, and how governance drives value.

**Hands-on lab**
1. Ingest or select a sample asset and complete all mandatory metadata.
2. Apply approved tags from the client's taxonomy and validate search discovery.
3. Place the asset in an approved collection or folder and route it through review.
4. Resolve a simulated duplicate, expired-rights, or incomplete-metadata exception.
5. Produce a short stewardship report of quality gaps and recommended corrections.

**Premium Learning and webinars**
- Metadata, taxonomy, and governance (Premium Learning, high priority): stewardship, discovery, rights, lifecycle, and quality standards for the client.
- Taxonomy & Structure: AEM's Secret to Scalable Asset Management (webinar).
- AEM Assets Content Hub: Intelligent Discovery and Governed Distribution for Enterprises (webinar).
- AEM Assets user fundamentals (Premium Learning, high priority): shared with DAM User.
- Workflows, integrations, and automation (Premium Learning, medium priority, advanced): optional next step.

**Suggested effort:** 8-12 hours

### DAM Administrator

**Role:** Manages DAM configuration, permissions, metadata structures, and operational controls.

**Learning objectives**
- Understand how the Adobe Admin Console, AEM user groups, product profiles, and repository permissions relate.
- Configure and govern metadata schemas, metadata profiles, taxonomy, and search facets.
- Apply group-based, least-privilege access to folders and DAM capabilities.
- Support asset workflows, processing profiles, lifecycle controls, and integrations, including the Experience Workspace connection.
- Monitor configuration health, troubleshoot access and processing issues, and maintain operational documentation.

**Documentation and tutorials**
- [Set up AEM Assets for Experience Workspace](https://www.aem.live/docs/ew/administering/set-up-aem-assets)
- _Links: see original:_ AEM Assets as a Cloud Service overview · User group and permission best practices · Baseline permissions tutorial · Metadata best practices · Taxonomy management tutorial · AEM Assets videos and tutorials (Admin view playlists).

**Hands-on lab**
1. Map DAM User, DAM Librarian, and DAM Administrator to the client's groups and least-privilege permissions.
2. Configure or review a metadata schema and profile in non-production.
3. Validate taxonomy visibility, search facets, and mandatory-field behaviour.
4. Test upload, processing, review, download, and access boundaries with representative accounts.
5. Confirm authors can insert an approved asset from Experience Workspace.
6. Document one troubleshooting scenario and the evidence support needs for escalation.

**Webinars**
- Taxonomy & Structure: AEM's Secret to Scalable Asset Management.
- The Right Access for the Right Teams: Designing Smarter Roles and Workflows in AEM Assets.

**Suggested effort:** 12-16 hours

### Cross-role webinars and coaching (optional)

Catalog titles, schedules, seats, language, and entitlement change, so confirm availability in the client's learning portal before assigning.
- Content Hub vs. Brand Portal: most relevant to librarians and administrators making platform decisions.
- Developing Reports and ROI Metrics for AEM Assets: useful for reporting on program value.

---

## Changes from the original draft

**Removed (AEM Sites with the Universal Editor, or outdated):**
- Site Templates (classic AEM Sites) · Create an AEM Site · Methods to Author Content in AEM · Set Up AEM Sites as a Content Source · EDS and Universal Editor Developer Tutorial · Authoring with AEM Sites for EDS · Create an AEM Site for EDS
- AEM Sites and Edge Delivery Services (Architect). Add it back only if EW versus the Universal Editor is still being decided.
- Document Authoring Videos and Document Workflows: DA-era material that likely shows the pre-EW editor. Replaced with Experience Workspace pages; EW's approval workflow is Request Publish.

**Changed:**
- Edge Delivery Services Overview moved from the business foundation to the technical track.
- Role wording changed from "AEM Sites" to Experience Workspace (Content Author, CMS Administrator).
- The stray "Getting Started – Developer Tutorial" line (between CMS Administrator and Content Manager) moved to the Front-End Developer, CMS Administrator, and Platform Admin paths.
- The CMS Administrator access lab is split into EW read/write and Edge Delivery preview/publish.

**Added:** EW pages for publishing, Request Publish, Schedule Publish, Preflight, snapshots, version history, Live Preview, and the Assistant; the AEM Assets connection for Content Author, Platform Admin, and DAM Administrator.

**Client name** removed throughout; replaced with "the client".

## Open questions for the Adobe TAM

1. Are there current **Experience Workspace videos** to replace the Document Authoring videos?
2. Which **webinars and video-hub** sessions reflect Experience Workspace, not the older editor?
3. Does the EW asset picker work with **Content Hub**, or only AEM Assets (publish or Dynamic Media)? The DAM User path recommends Content Hub.
4. Are **Request Publish** and **Schedule Publish** generally available for this client, or still early access?
