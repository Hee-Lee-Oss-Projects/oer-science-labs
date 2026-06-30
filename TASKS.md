# TASKS — oer-science-labs (open, low-cost, safety-reviewed science experiment guides)

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## How these tasks map to Elyos

Each task below becomes an Elyos **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- `id` — stable slug ID, e.g. `oer-science-labs-arch-001`.
- `title` — the task title from the table.
- `project` — `"oer-science-labs"`.
- `type` — one of `code | research | writing | data | design-spec | maintenance` (the "Type" column).
- `lane` — `"donated"` for all tasks here (no escrow/API spend). A `funded` task would additionally
  require `fundedBudgetUsd` (per the schema's `if/then` rule).
- `priority` — `high | medium | low`.
- `domain` — array, e.g. `["education","science","safety","software","accessibility","translation"]`.
- `riskTier` — `low | medium | high` (the "Risk" column). Guide-content + safety tasks are **medium**.
- `urgent` — boolean (default `false`; this is curriculum content, not live response).
- `deliverable` — `pr | dataset | document | translation` (the "Deliverable" column).
- `tokenEstimate` — `small | medium | large` (the "Size" column).
- `status` — `open | in-progress | review | delivered | done` (all start `open`).
- `context`, `objective`, `acceptanceCriteria[]`, `output` — task narrative + checkable criteria.
- `resources[]` — source/reference URLs or repo paths.
- `requestor` — partner/requestor (**TO BE SECURED**; use `"TBD"` until a partner is named).
- `verifiedNeed` — **`false` until a named partner confirms need in writing** (honest default).
- `outputLicense` — `"MIT"` for code, `"CC-BY-4.0"` for content/guides/translations.

**Reviewer column legend:** `maintainer` (code review), `science` (science/curriculum-accuracy
reviewer), `safety` (credentialed safety reviewer, distinct from author), `dry-run` (second educator
who physically reproduces the guide), `a11y` (accessibility reviewer), `translation+safety`
(competent speaker paired with safety-accuracy re-check), `steward` (last-mile/partner/field-testing).

**Content review rule (all guide tasks, medium risk):** dual review with **no self-approval** —
`authoredBy`, `scienceReviewedBy`, and `safetyApprovedBy` must be **distinct people**. The safety
approver must meet the credential bar (qualified science teacher with lab-safety training, school/lab
safety officer, occupational-safety/industrial-hygiene professional, or equivalent). Each guide is
**physically dry-run/reproduced by a second educator** before publish. Every approval writes a
**PR-tied, append-only review-log entry** (PR #, commit SHA, `contentVersion`, the three named roles,
sources checked, **exclusion-check result**, dry-run result, any divergence decision) — the auditable
record the Definition of Shipped checks against.

**Sequencing rule (M0):** the **content-format ADR (arch-001) lands before** the guide schema
(`data-003`) is finalized, and the **hazard-taxonomy + hard-exclusion-list ADR (arch-002) lands
before** the first guide (`content-006`) is authored. Until those ADRs land the schema is provisional
and format-agnostic. Dependencies below reflect this.

---

## Milestone M0 — Foundation & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| oer-science-labs-arch-001 | ADRs: **content format (decide first)**, static-site + SW tooling, hosting, content-version manifest/hard-invalidation, PDF/print | design-spec | small | low | document | — | maintainer |
| oer-science-labs-arch-002 | Hazard taxonomy + safety-review rubric + **hard exclusion list** (CI-encodable) | design-spec | medium | medium | document | — | maintainer, safety |
| oer-science-labs-data-003 | Experiment-guide content schema + provenance/review-log format | data | medium | low | dataset | arch-001, arch-002 | maintainer, science, safety |
| oer-science-labs-code-004 | Repo scaffold + CI: schema-validation, **exclusion-list**, **cost-ceiling**, readability, no-telemetry audit (CSP `connect-src 'none'` + runtime interception E2E) | code | medium | low | pr | data-003 | maintainer |
| oer-science-labs-code-005 | Static site skeleton: installable/offline shell + per-guide printable output | code | medium | low | pr | arch-001 | maintainer, a11y |
| oer-science-labs-content-006 | Sample guide (e.g. density tower / red-cabbage pH indicator), source-cited, dual-reviewed, dry-run | writing | small | medium | document | data-003, arch-002 | science, safety, dry-run |

**Acceptance criteria — key tasks**

- **oer-science-labs-arch-002 (hazard taxonomy + hard exclusion list):**
  - Defines hazard **classes** (chemical, fire/heat, sharp, electrical, biological, projectile,
    pressure, allergen/ingestion, environmental, photosensitivity/sensory), **severity levels**,
    required **PPE**, **minimum age/supervision**, and **disposal classes**.
  - Publishes a **hard exclusion list** of barred activity classes (concentrated/strong acids & bases
    beyond household-dilution norms; toxic/asphyxiant/corrosive gas generation; explosives/energetics/
    pyrotechnics/thermite; flame + volatile-fuel demos; mains/high-voltage/high-current; high-pressure
    vessels; ionizing radiation; pathogen culture; controlled/regulated substances; ingestion of
    non-food chemicals; vertebrate-animal or human-subject harm) — represented so CI can enforce it.
  - Includes the **safety-review rubric** a credentialed reviewer applies, and a change process
    (governance-ratified) for amending the exclusion list.
- **oer-science-labs-data-003 (content schema):**
  - Captures discipline, grade bands, `minAge`, `supervision`, setting, time, group size, `materials[]`
    (item/quantity/cost/substitutions/hazardFlags), `estTotalCost` + ceiling flag, procedure with
    inline safety callouts, science + misconceptions, assessment/extensions, `curriculumAlignments[]`
    (framework/code/link/rationale — **codes/links, not restricted full text**), the full `safety`
    block (hazards/PPE/allergens-ingestion/disposal/photosensitivity-sensory/prohibited-substitutions/
    firstAidRef/exclusionCheck), `readingLevel`, `sources[]`, the three review roles, `reviewLogRef`,
    `lastReviewed`, lang, license, `contentVersion`, `integrityHash`, `hardInvalidate`.
  - Follows the content-format ADR (arch-001), which lands first; schema is provisional until then.
  - Build-time validation rejects a guide missing required citation/safety fields, a guide where
    `safetyApprovedBy` or `scienceReviewedBy` equals `authoredBy` (no self-approval), and a guide that
    trips the hard exclusion list.
- **oer-science-labs-code-004 (CI gates):**
  - CI fails on lint/type/unit/schema errors, on any **exclusion-list** hit, on a guide over its
    **cost ceiling**, on a **readability** miss for the grade band, and on offline E2E failure.
  - No-telemetry/no-PII via defense in depth: static tracker/PII audit **plus** a runtime network-
    interception E2E that fails on any unexpected outbound request; CSP `connect-src 'none'` asserted.
    A static grep alone does not pass.
- **oer-science-labs-content-006 (sample guide):**
  - Every claim/material/step is traceable to a cited open/PD/CC source with retrieval date + license;
    no verbatim copying of copyrighted text; only open/PD/CC media.
  - Carries a complete, accurate safety block (hazards, PPE, `minAge`, supervision, allergens/
    ingestion, disposal, prohibited substitutions) and **passes the exclusion check**.
  - Runnable within the cost ceiling using listed substitutions and **no special lab equipment**.
  - Science-reviewed for accuracy + misconceptions and **credentialed-safety-approved** by reviewers
    **distinct from the author**, and **dry-run/reproduced by a second educator**; a PR-tied review-log
    entry is written.

**Definition of Done (M0):** Repo + MIT/CC-BY licensing in place; content-format ADR recorded before
the schema is finalized; hazard taxonomy + safety rubric + hard exclusion list recorded before the
first guide; CI enforces schema-validation + exclusion-list + cost-ceiling + readability +
no-telemetry; static offline/printable shell loads after first visit; **one sample guide** renders
from the schema, fully cited, dual-reviewed, exclusion-checked, and dry-run; telemetry/PII audit green.

---

## Milestone M1 — Safety framework hardening & first guide set

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| oer-science-labs-content-007 | First guide set: ≥ 8 guides across ≥ 2 disciplines × ≥ 2 grade bands, dual-reviewed + dry-run | writing | large | medium | document | content-006 | science, safety, dry-run |
| oer-science-labs-code-008 | Browse/filter UI (discipline, grade band, cost, materials, hazard level) — offline | code | large | low | pr | code-005 | maintainer, a11y |
| oer-science-labs-code-009 | Cost-ceiling + readability gates wired into CI + authoring tooling | code | medium | low | pr | code-004 | maintainer |
| oer-science-labs-a11y-010 | WCAG 2.2 AA hardening + manual assistive-tech audit | code | medium | low | pr | code-008 | a11y |
| oer-science-labs-ops-011 | Incident-report channel + triage process (no required PII) + hard-invalidation wiring | code | medium | medium | pr | code-005 | maintainer, steward, safety |

**Acceptance criteria — key tasks**

- **oer-science-labs-content-007 (first guide set):**
  - ≥ 8 guides spanning ≥ 2 disciplines and ≥ 2 grade bands; each within cost ceiling, runnable
    without lab equipment, fully cited, dual-reviewed (science + credentialed safety), and **dry-run by
    a second educator**; each passes the exclusion check with the result recorded in the review log.
- **oer-science-labs-a11y-010 (AA hardening):**
  - Automated axe/pa11y pass with 0 critical issues across browse, guide, and print views.
  - Documented manual audit across the support matrix (NVDA+Firefox/Win, JAWS+Chrome/Win,
    VoiceOver+Safari/macOS·iOS, TalkBack+Chrome/Android, keyboard-only per desktop), signed off by the
    qualified a11y reviewer; printable output is readable and offline.
- **oer-science-labs-ops-011 (incident channel):**
  - A public report channel accepts safety reports/near-misses **without requiring personal data**;
    triage targets 72h; a confirmed safety issue triggers **hard-invalidation** (purge + force refresh)
    of the implicated guide via the content-version manifest; incidental PII is minimized, never
    committed.

**Definition of Done (M1):** ≥ 8 guides across ≥ 2 disciplines × ≥ 2 grade bands, each dual-reviewed +
dry-run; cost-ceiling + readability enforced in CI; accessible (AA, manual AT) offline browse + print;
incident-report + triage + hard-invalidation operational.

---

## Milestone M2 — Curriculum alignment & i18n

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| oer-science-labs-data-012 | Curriculum crosswalk model + code-level mapping to ≥ 2 frameworks (license-clean) | data | medium | medium | dataset | data-003, content-007 | maintainer, science |
| oer-science-labs-content-013 | Alignment review: validate guide↔standard mappings + written rationale | research | medium | medium | document | data-012 | science |
| oer-science-labs-code-014 | i18n framework: catalogs, units (metric/imperial), ICU pluralization, locale formatting, completeness check, safe fallback | code | medium | low | pr | code-008 | maintainer, a11y |
| oer-science-labs-l10n-015 | First non-English UI localization (provisional; partner may override) | writing | medium | medium | translation | code-014 | translation+safety |
| oer-science-labs-l10n-016 | Localize ≥ 1 guide (safety terms accuracy-reviewed) | writing | medium | medium | translation | l10n-015, content-007 | translation+safety, science, safety |

**Acceptance criteria — key tasks**

- **oer-science-labs-data-012 (curriculum crosswalk):**
  - Maps guides to ≥ 2 frameworks (e.g. NGSS + 1 national/regional) by **standard code + link + our
    own rationale**; does **not** embed restricted full standard text; each framework's license is
    verified and recorded; the structure is additive for future frameworks.
- **oer-science-labs-l10n-016 (localized guide):**
  - Translation is **accuracy-reviewed for safety meaning**, not only fluency, against the source guide
    and official safety terminology in that language where available; units/formatting localized;
    `contentLicense` = CC-BY-4.0; source attribution preserved.

**Definition of Done (M2):** Code-level crosswalk to ≥ 2 frameworks with alignment review and
license-clean handling; i18n framework with build-time completeness check; ≥ 1 non-English locale
complete for UI + ≥ 1 guide; safe fallback verified; localized safety terms accuracy-reviewed.

---

## Milestone M3 — Scale, partner adoption & classroom validation

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| oer-science-labs-partner-017 | Secure named partner (need, disciplines, grade bands, languages, field-testing) | research | medium | medium | document | — | maintainer, steward |
| oer-science-labs-content-018 | Scale to ≥ 30 reviewed guides across ≥ 3 disciplines × ≥ 3 grade bands | writing | large | medium | document | content-007 | science, safety, dry-run |
| oer-science-labs-l10n-019 | Reach ≥ 2 fully localized languages (UI + key guides) | writing | large | medium | translation | l10n-016 | translation+safety, safety |
| oer-science-labs-steward-020 | Classroom field-testing of ≥ 5 guides with a partner; incorporate feedback | research | medium | medium | document | partner-017, content-018 | steward, safety |
| oer-science-labs-code-021 | Production deployment + versioned cache/update + non-endorsement disclaimer | code | medium | low | pr | a11y-010, code-014 | maintainer, steward |
| oer-science-labs-ops-022 | Outcomes-tracking process + annual/event-driven safety re-review cadence | maintenance | small | low | document | partner-017 | maintainer, steward, safety |

**Acceptance criteria — key tasks**

- **oer-science-labs-partner-017 (secure partner):**
  - A named partner (school/district, teacher association, or OER/education nonprofit) confirms the
    need in writing (letter of support or MOU) and names priority disciplines, grade bands, languages,
    and material-availability constraints; ideally commits to classroom field-testing.
  - On success, `verifiedNeed` flips to `true` and `requestor` is set to the named org across tasks.
- **oer-science-labs-steward-020 (classroom field-testing):**
  - ≥ 5 guides run in real classrooms under the stated supervision; educator feedback (usefulness,
    safety, cost, timing) collected **without student PII**; issues fixed or guides revised; any safety
    concern routed through the incident/triage + hard-invalidation path.
- **oer-science-labs-ops-022 (outcomes + freshness):**
  - Documented privacy-preserving outcomes process (educator/partner self-report; no telemetry) over a
    rolling 12-month window counting distinct educators/class groups; **zero-harm-incident** tracking
    via the incident channel; re-review cadence defined (**annual + after any incident or guidance
    change**) with staleness flagging.

**Definition of Done (M3):** ≥ 30 reviewed guides across ≥ 3 disciplines × ≥ 3 grade bands; ≥ 2
frameworks mapped; ≥ 2 languages; **named partner endorsement/adoption on file** (verifiedNeed = true);
≥ 5 guides field-tested in real classrooms with feedback incorporated; production build deployed with
safe versioned update + non-endorsement disclaimer; outcomes tracking + safety re-review cadence
operational. This satisfies the project-level *Definition of Shipped (partner-validated)*.

**Decision point (so a finished library isn't stranded):** if no partner is secured by **6 months
after the M3 production build is ready**, the steward + Elyos governance declare **"Publicly Shipped
(generic public good)"** — criteria (1)–(5) met, deployed and distributed via educator/OER channels,
outcomes tracked by best-effort self-report. A later partner endorsement upgrades the status rather
than re-opening launch.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| oer-science-labs-content-023 | Easy-read / low-literacy guide variants | writing | medium | medium | document | a11y + science + safety review |
| oer-science-labs-content-024 | Pictograph/icon set for materials, hazards & PPE (license-clean) | design-spec | medium | low | document | Open/PD/CC assets only |
| oer-science-labs-content-025 | Outdoor / field-science guides (weather, ecology, astronomy-by-eye) | writing | large | medium | document | Environmental + sun/heat safety |
| oer-science-labs-feat-026 | Materials-availability presets per region (advisory, no PII) | code | medium | low | pr | User picks region; no tracking |
| oer-science-labs-feat-027 | "Teacher pack" bundle export (multi-guide printable + materials list) | code | medium | low | pr | Client-side only |
| oer-science-labs-data-028 | Additional curriculum frameworks added to crosswalk | data | medium | medium | dataset | License-verified per framework |
| oer-science-labs-ops-029 | Annual safety + curriculum re-validation pass | maintenance | medium | medium | document | Recurring; staleness flags |
| oer-science-labs-sec-030 | Dependency/supply-chain audit + SRI hardening | maintenance | small | low | pr | Recurring |

---

## Example task JSON

Complete, schema-valid Task JSON for the first M0 task. `verifiedNeed` is `false` and `requestor` is
`"TBD"` because **no partner is secured yet** (honest default per the plan). Lane is `donated`, so no
`fundedBudgetUsd` is required.

```json
{
  "id": "oer-science-labs-arch-001",
  "title": "ADRs: content format (decide first), static-site + SW tooling, hosting, content-version manifest, PDF/print",
  "project": "oer-science-labs",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["education", "science", "software"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "small",
  "status": "open",
  "context": "oer-science-labs is an open library of no-/low-cost, curriculum-aligned, safety-reviewed science experiment guides for under-resourced classrooms, homeschoolers, and informal educators. This task records the foundational architecture decisions. The content-format ADR must be decided FIRST because the guide schema and content precaching both depend on it; the hazard-taxonomy/hard-exclusion-list ADR is a separate task (arch-002) that must land before any guide is authored.",
  "objective": "Produce Architecture Decision Records selecting the content format (JSON vs MDX), the static-site generator + service-worker tooling, the hosting target, the content-version manifest / hard-invalidation mechanism for safety corrections, and the PDF/print approach — sequenced so the content-format decision is made before the schema is finalized.",
  "acceptanceCriteria": [
    "Content-format ADR (JSON vs MDX) is recorded and explicitly marked as a prerequisite for the guide schema (data-003)",
    "ADRs cover static-site generator + service-worker tooling, precache budget/eviction, and hosting target (static, no app server)",
    "An ADR specifies the content-version manifest (per-guide version + integrity hash + hardInvalidate flag) and how a corrected/withdrawn guide is purged and force-refreshed (non-dismissible)",
    "An ADR specifies the client-side PDF/print approach for per-guide printable output (no server round-trip)",
    "Each ADR states context, options considered, decision, and consequences; decisions are consistent with MIT code / CC-BY-4.0 content and zero-telemetry constraints"
  ],
  "resources": [
    "C:\\code\\elyos\\planning\\projects\\oer-science-labs\\PLAN.md",
    "C:\\code\\elyos\\docs\\good-deed-definition.md",
    "C:\\code\\elyos\\packages\\schema\\src\\schemas.ts"
  ],
  "output": "A pull request adding the foundational ADR documents (content format decided first, site/SW tooling, hosting, content-version manifest/hard-invalidation, PDF/print) for oer-science-labs.",
  "requestor": "TBD",
  "verifiedNeed": false,
  "outputLicense": "MIT"
}
```

---

## Generated task index

> Auto-generated by Elyos task-decomposition on 2026-06-29. Seed: `oer-science-labs-arch-001` (committed). All other task files generated from the backlog above.

| File | ID | Title | Type | Deliverable | Risk | Status |
| --- | --- | --- | --- | --- | --- | --- |
| tasks/oer-science-labs-arch-001.json | oer-science-labs-arch-001 | ADRs: content format (decide first), static-site + SW tooling, hosting, content-version manifest, PDF/print | design-spec | document | low | open |
| tasks/oer-science-labs-arch-002.json | oer-science-labs-arch-002 | Hazard taxonomy + safety-review rubric + hard exclusion list (CI-encodable) | design-spec | document | medium | open |
| tasks/oer-science-labs-data-003.json | oer-science-labs-data-003 | Experiment-guide content schema + provenance/review-log format | data | dataset | low | open |
| tasks/oer-science-labs-code-004.json | oer-science-labs-code-004 | Repo scaffold + CI: schema-validation, exclusion-list, cost-ceiling, readability, no-telemetry audit | code | pr | low | open |
| tasks/oer-science-labs-code-005.json | oer-science-labs-code-005 | Static site skeleton: installable/offline shell + per-guide printable output | code | pr | low | open |
| tasks/oer-science-labs-content-006.json | oer-science-labs-content-006 | Sample guide (e.g. density tower / red-cabbage pH indicator): source-cited, dual-reviewed, dry-run | writing | document | medium | open |
| tasks/oer-science-labs-content-007.json | oer-science-labs-content-007 | First guide set: ≥ 8 guides across ≥ 2 disciplines × ≥ 2 grade bands, dual-reviewed + dry-run | writing | document | medium | open |
| tasks/oer-science-labs-code-008.json | oer-science-labs-code-008 | Browse/filter UI (discipline, grade band, cost, materials, hazard level) — offline | code | pr | low | open |
| tasks/oer-science-labs-code-009.json | oer-science-labs-code-009 | Cost-ceiling + readability gates wired into CI + authoring tooling | code | pr | low | open |
| tasks/oer-science-labs-a11y-010.json | oer-science-labs-a11y-010 | WCAG 2.2 AA hardening + manual assistive-tech audit | code | pr | low | open |
| tasks/oer-science-labs-ops-011.json | oer-science-labs-ops-011 | Incident-report channel + triage process (no required PII) + hard-invalidation wiring | code | pr | medium | open |
| tasks/oer-science-labs-data-012.json | oer-science-labs-data-012 | Curriculum crosswalk model + code-level mapping to ≥ 2 frameworks (license-clean) | data | dataset | medium | open |
| tasks/oer-science-labs-content-013.json | oer-science-labs-content-013 | Alignment review: validate guide↔standard mappings + written rationale | research | document | medium | open |
| tasks/oer-science-labs-code-014.json | oer-science-labs-code-014 | i18n framework: catalogs, units, ICU pluralization, locale formatting, completeness check, safe fallback | code | pr | low | open |
| tasks/oer-science-labs-l10n-015.json | oer-science-labs-l10n-015 | First non-English UI localization (provisional; partner may override locale choice) | writing | translation | medium | open |
| tasks/oer-science-labs-l10n-016.json | oer-science-labs-l10n-016 | Localize ≥ 1 guide (safety terms accuracy-reviewed) | writing | translation | medium | open |
| tasks/oer-science-labs-partner-017.json | oer-science-labs-partner-017 | Secure named partner (need, disciplines, grade bands, languages, field-testing) | research | document | medium | open |
| tasks/oer-science-labs-content-018.json | oer-science-labs-content-018 | Scale to ≥ 30 reviewed guides across ≥ 3 disciplines × ≥ 3 grade bands | writing | document | medium | open |
| tasks/oer-science-labs-l10n-019.json | oer-science-labs-l10n-019 | Reach ≥ 2 fully localized languages (UI + key guides) | writing | translation | medium | open |
| tasks/oer-science-labs-steward-020.json | oer-science-labs-steward-020 | Classroom field-testing of ≥ 5 guides with a partner; incorporate feedback | research | document | medium | open |
| tasks/oer-science-labs-code-021.json | oer-science-labs-code-021 | Production deployment + versioned cache/update + non-endorsement disclaimer | code | pr | low | open |
| tasks/oer-science-labs-ops-022.json | oer-science-labs-ops-022 | Outcomes-tracking process + annual/event-driven safety re-review cadence | maintenance | document | low | open |
| tasks/oer-science-labs-content-023.json | oer-science-labs-content-023 | Easy-read / low-literacy guide variants | writing | document | medium | open |
| tasks/oer-science-labs-content-024.json | oer-science-labs-content-024 | Pictograph/icon set for materials, hazards & PPE (license-clean) | design-spec | document | low | open |
| tasks/oer-science-labs-content-025.json | oer-science-labs-content-025 | Outdoor / field-science guides (weather, ecology, astronomy-by-eye) | writing | document | medium | open |
| tasks/oer-science-labs-feat-026.json | oer-science-labs-feat-026 | Materials-availability presets per region (advisory, no PII) | code | pr | low | open |
| tasks/oer-science-labs-feat-027.json | oer-science-labs-feat-027 | "Teacher pack" bundle export (multi-guide printable + materials list) | code | pr | low | open |
| tasks/oer-science-labs-data-028.json | oer-science-labs-data-028 | Additional curriculum frameworks added to crosswalk | data | dataset | medium | open |
| tasks/oer-science-labs-ops-029.json | oer-science-labs-ops-029 | Annual safety + curriculum re-validation pass | maintenance | document | medium | open |
| tasks/oer-science-labs-sec-030.json | oer-science-labs-sec-030 | Dependency/supply-chain audit + SRI hardening | maintenance | pr | low | open |

**Total: 30 task files (1 seed + 29 generated). Validation: ALL VALID (30/30). Fan-out dimensions: none.**
