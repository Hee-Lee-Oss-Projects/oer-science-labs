# PLAN — oer-science-labs (open, low-cost, safety-reviewed science experiment guides)

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## Executive summary

**oer-science-labs** is an open library of **no-/low-cost, hands-on science experiment guides** for
K–12 and early-college learners, each **aligned to curriculum standards** and **safety-reviewed for
physical hazards** before it ships. The goal is concrete: let any teacher, tutor, homeschool parent,
or after-school educator — including those with **no laboratory, no budget, and limited
connectivity** — run a real, standards-aligned science investigation using household or inexpensive
materials, without guessing at the safety risks.

The project has two coupled lanes of work: (1) **content** — structured, source-cited experiment
guides (materials, cost, procedure, the science, assessment, and an explicit safety block) authored
to a fixed schema and **dual-reviewed for science/curriculum accuracy and for hazard safety**; and
(2) **a thin delivery layer** — a static, accessible, offline-capable browse-and-print site plus
authoring/validation tooling that enforces the schema, the citation rules, and the **hard hazard
exclusion list** in CI. Code is **MIT**, content is **CC-BY-4.0**; only **open / public-domain / CC**
sources are reused, with per-source license verification.

This is a **medium risk-tier** project. A mis-stated experiment can cause real, physical harm —
chemical burns, eye injury, fire, electric shock, ingestion/allergy, or environmental damage from bad
disposal. Two consequences follow and are non-negotiable: **(a)** every guide passes a **credentialed
safety review** (author ≠ safety approver) against a published hazard taxonomy, and **(b)** a **hard
exclusion list** bars whole classes of dangerous activity from the library entirely (no concentrated
acids/bases, no toxic-gas generation, no energetic/explosive or pyrotechnic reactions, no high-voltage
mains work, etc.). Guides are **educational resources, not a substitute** for local safety
regulations, a qualified teacher's judgment, or required adult supervision — stated on every guide.

**Honesty note on the partner / verified need.** No partner school, district, teacher network, or
ministry of education, and no MOU or letter of support, exists yet. The need for free, safe,
low-resource science labs is well evidenced in general (see *Problem & beneficiaries*), but a
**named partner and a written verified need are TO BE SECURED**. Until one exists, `verifiedNeed`
is `false` across all tasks, `requestor` is `TBD`, and the project ships as a **generic public good**
that a partner can later endorse and field-validate (see *Quality, review & risk gates*).

## Problem & beneficiaries

**The problem.** Hands-on science raises engagement and understanding, but high-quality lab
activities are gated behind money and equipment that most classrooms — and almost all home and
informal settings — do not have. Existing experiment write-ups are scattered, frequently **omit or
under-specify safety** (hazards, PPE, age-appropriateness, disposal), assume lab supplies or
internet access, are often **copyright-restricted** (textbook publishers, commercial "STEM kit"
vendors), and are rarely mapped to the curriculum a teacher is actually accountable to. Some popular
"viral" home experiments circulating online are **genuinely dangerous** (e.g. concentrated-chemical
or fire demos) and are presented with no safety framing at all. The gap is not a lack of activities;
it is a lack of *free, safe, low-cost, standards-aligned, and accurately reviewed* ones.

**Who is helped (beneficiaries).**
- **Teachers in under-resourced schools** (rural, low-income, large-class, lab-less) who must teach
  practical science with little or no budget and equipment.
- **Homeschool parents and tutors** who are not science specialists and need both the activity and an
  honest hazard assessment they can trust.
- **After-school / informal / community educators** (libraries, clubs, refugee and community-learning
  programs) running STEM enrichment on a shoestring.
- **Students themselves** (independent and curious learners), where the guide explicitly requires the
  stated supervision and age-appropriateness.
- **Curriculum and OER coordinators** who need an openly-licensed, mappable, vetted bank of labs to
  recommend or remix.

**Verified need / partner org: TO BE SECURED.** General need is well-documented by education and OER
bodies, but this project will treat the need as **plausible but unverified** until at least one named
partner (a school/district, a teacher association, a recognized OER/education nonprofit, or a science
educators' body) confirms it in writing, names priority **disciplines, grade bands, languages, and
material-availability constraints**, and ideally offers classroom field-testing. Foundation work
(M0–M1) proceeds on the strength of general need; partner endorsement + field validation is required
before the full *Definition of Shipped* is met.

## Goals and non-goals

**Goals.**
- Publish **standards-aligned experiment guides** that are runnable with **household / low-cost
  materials** (explicit per-guide cost ceiling and substitution options).
- Make **safety first-class**: every guide carries a structured, reviewed safety block (hazards, PPE,
  minimum age / supervision, allergens/ingestion, disposal, prohibited substitutions) and passes
  **credentialed safety review**; a **hard exclusion list** keeps dangerous classes of activity out.
- Be **accurate**: each guide is science-correct, addresses common misconceptions, and is mapped to
  named curriculum standards by code with a written alignment rationale.
- Be genuinely **free, open, and forkable**: MIT code / CC-BY-4.0 content; only open/PD/CC sources
  reused, license-verified; no ads, no paywall, no account, no student PII.
- Be **usable in low-resource conditions**: accessible (WCAG 2.2 AA), **printable**, and **offline-
  capable** after first load.
- Be **internationalizable** (units, language, locale formatting) with ≥ 1 non-English localization,
  safety terms re-checked for accuracy.
- Be **field-credible**: each guide is dry-run/reproduced by a second educator and (at scale)
  validated in a real classroom via a partner.

**Non-goals.**
- **Not** a provider of dangerous, energetic, or high-stakes demonstrations — see the hard exclusion
  list (no concentrated acids/bases, toxic gases, explosives/pyrotechnics, mains/high-voltage, etc.).
- **Not** medical, clinical, or pharmacological experimentation; **not** human-subjects or
  vertebrate-animal experimentation; **not** experiments requiring controlled/regulated substances.
- **Not** a substitute for local laws, school safety policies, lab-safety regulations, or a qualified
  educator's supervision (we state this; we do not replace it).
- **Not** a data-collection, accounts, analytics, or grading product; no student profiles or PII.
- **Not** a verbatim re-host of copyrighted textbook/kit-vendor content or full restricted standards
  text (we map by code + link, and author original guidance).
- **Not** a commercial product, kit-sales funnel, or lead-gen for any vendor or brand.
- **Not** a take-a-position platform on socially contested science; we present **accurate, sourced
  consensus science** (e.g. evolution, climate, vaccines) factually and non-editorially.

## Success metrics (outcomes)

Outcome-centric and beneficiary-first. Baselines are zero at project start unless noted. Because we
collect **no student PII and no in-app analytics**, classroom/reach outcomes are measured by
**partner/educator self-report**, an explicit privacy-for-precision trade-off (see *Sustainability*).

| Outcome | Baseline | Target (first 12 months post-launch) | How measured (privacy-preserving) |
| --- | --- | --- | --- |
| Safety-reviewed guides published | 0 | ≥ 30 guides, each dual-reviewed (science/curriculum + safety) | In-repo review log |
| Discipline & grade-band coverage | 0 | ≥ 3 disciplines (physics, chemistry-safe, biology, earth/space) × ≥ 3 grade bands | Coverage matrix in CI |
| Curriculum frameworks mapped | 0 | ≥ 2 frameworks (e.g. NGSS + 1 national/regional), code-level crosswalk | Alignment report in repo |
| Material-cost achievability | n/a | 100% of published guides runnable within the per-guide cost ceiling using listed substitutions | Cost field validated in CI; spot-checked |
| Accessibility conformance | none | WCAG 2.2 AA verified (automated + manual AT); printable + readable offline | axe/pa11y + manual audit; offline E2E |
| Reading-level fit | n/a | Each guide's learner-facing text within the target reading level for its grade band | Readability check in CI + reviewer confirm |
| Reported safety incidents / near-misses | 0 | **0 harm incidents**; any report triages within 72h and hard-invalidates the guide if implicated | Incident-report channel + review log |
| Languages localized (UI + ≥1 guide) | 1 (en) | ≥ 2 languages, safety terms accuracy-reviewed | Translation completeness check in CI |
| Educator usefulness / would-reuse | n/a | ≥ 80% of surveyed educators rate a tried guide "useful and safe to run again" | Optional educator survey (no PII) |
| Partner adoption / field validation | 0 | ≥ 1 named partner adopts and field-tests ≥ 5 guides in real classrooms | Signed letter/MOU + partner report |
| Privacy posture | n/a | 0 telemetry endpoints, 0 trackers, 0 student-PII fields | Static audit + runtime network-interception E2E (CSP `connect-src 'none'`) |

We deliberately avoid vanity metrics (downloads, stars). **Zero harm incidents is the headline
outcome** — a single avoidable injury would outweigh any reach number.

**Reach/adoption measurement — windows & denominators.** "Classrooms/educators reached" counts
**distinct educators or class groups** (not page views or downloads) over a **rolling 12-month
window** from launch, partner/educator-attested, de-duplicated at roll-up by the steward, with
estimates recorded separately from confirmed counts. No student-level counting of any kind.

## Scope

**In scope.**
- A structured **experiment-guide content schema** (materials + cost + substitutions, procedure, the
  science + misconceptions, assessment/extension, curriculum alignment, and a mandatory **safety
  block**) with authoring + CI validation.
- A published **hazard taxonomy**, a **safety-review rubric**, and a **hard exclusion list** enforced
  in CI (a guide tripping an exclusion cannot merge).
- **Guides** across core school-science disciplines and grade bands, each dual-reviewed and dry-run.
- A **curriculum crosswalk** mapping guides to standards by **code** (with written rationale; not
  reproducing restricted standard text).
- A thin **static, accessible, offline-capable** browse-and-print delivery site + per-guide printable
  output.
- **i18n** framework (language + units + locale formatting) and ≥ 1 non-English localization with
  safety-accuracy review.
- A **provenance/review log**, an **incident-report channel**, and a **content-version manifest** with
  forced invalidation for safety corrections.

**Out of scope (explicit).**
- Any activity on the **hard exclusion list** (concentrated/strong acids & bases beyond household-
  dilution norms; toxic / asphyxiant / corrosive gas generation; explosives, energetics,
  pyrotechnics, thermite, or flame + volatile-fuel demos; mains / high-voltage / high-current
  electricity; high-pressure vessels; ionizing radiation sources; pathogen culture; controlled or
  regulated substances; ingestion of non-food chemicals; vertebrate-animal or human-subject harm).
- Medical/clinical/pharmacological or diagnostic procedures; first-aid *instruction* beyond linking
  official guidance.
- Student accounts, grading, analytics, social features, or any server-side PII.
- Telemetry, advertising, kit sales, or any monetization / vendor lead-gen.
- Verbatim re-hosting of copyrighted textbook, kit-vendor, or restricted-standard content.
- Localized or aligned content for languages/frameworks we cannot source-verify and review.
- Native app-store binaries at launch (PWA/printable only; native wrappers are backlog).

## Solution approach & architecture

**Overview.** A **content-first** project: the durable public good is the bank of safety-reviewed,
source-cited, standards-aligned guides expressed in a stable schema. The delivery layer is
deliberately thin — a **static** site with no backend, so there is nothing to leak and the content
is trivially forkable, printable, and usable offline.

**Components.**
- **Content store:** versioned, structured guides (one record per guide per language) as static
  JSON/MDX bundles (format fixed by ADR before the schema is finalized). No runtime content fetch
  required; everything can be precached or printed.
- **Authoring & validation tooling:** a CLI/CI validator that enforces the schema, required citation
  fields, the **hard exclusion list**, the **per-guide cost ceiling**, reading-level targets, and the
  **no-self-approval** rule (author ≠ safety approver). A guide that fails any gate cannot merge.
- **Safety framework:** the **hazard taxonomy** (hazard classes, severity, required PPE, minimum age
  / supervision, allergen/ingestion flags, disposal class, photosensitivity/seizure & sensory flags)
  + the **safety-review rubric** + the **hard exclusion list**. These are first-class versioned
  artifacts, not prose buried in a guide.
- **Curriculum crosswalk:** maps each guide to standards by **code** across ≥ 1 framework, with a
  written alignment rationale; structured so additional frameworks are additive.
- **Delivery site (UI):** TypeScript/ESM static site, WCAG 2.2 AA, print-optimized CSS, offline
  service-worker precache; browse/filter by discipline, grade band, cost, materials, hazard level,
  and standard; **per-guide printable/PDF** output generated client-side.
- **i18n layer:** message catalogs + per-guide localization keyed by `(guideId, lang)`; unit handling
  (metric primary, imperial secondary), ICU pluralization, locale formatting, build-time completeness
  check, safe fallback to English (never a blank safety block).
- **Incident & invalidation path:** a public **incident-report channel** feeds a triage process; a
  **content-version manifest** (per-guide version + integrity hash + `hardInvalidate` flag) lets the
  site purge and force-refresh a corrected/withdrawn guide (non-dismissible), so an unsafe guide is
  never served stale.
- **Build/CI:** pnpm workspace; lint, typecheck, unit, schema-validation, exclusion-list,
  cost-ceiling, readability, a11y, and offline E2E gates.

**Tech stack.** TypeScript, ESM, pnpm workspaces; static site generator + PWA (manifest + service
worker); static hosting (GitHub Pages / Netlify / Cloudflare Pages — no app server). Testing: Vitest
(unit/schema), axe-core/pa11y (a11y), Playwright (offline + network-interception E2E). License: MIT
(code) / CC-BY-4.0 (content).

**Data model (experiment guide — provisional until the content-format ADR lands).**
```
ExperimentGuide {
  id: string                       // e.g. "density-tower-01"
  title: localized string
  discipline: "physics"|"chemistry"|"biology"|"earth-space"|"general"
  gradeBands: string[]             // e.g. ["K-2","3-5","6-8"]
  minAge: integer                  // minimum recommended age
  supervision: "none"|"recommended"|"required-adult"
  setting: ("classroom"|"home"|"outdoor")[]
  timeMinutes: integer
  groupSize: string                // e.g. "1-4"
  materials: Material[]            // { item, quantity, unit, estCostLocal, substitutions[], hazardFlags[] }
  estTotalCost: { amount, currency, ceilingRespected: boolean }
  procedure: Step[]                // ordered; each step may carry inline safety callouts
  science: { concept, explanation, commonMisconceptions[] }
  assessment: { questions[], extensions[] }
  curriculumAlignments: Alignment[] // { framework, code, statementRef(link), rationale }  // codes/links, not restricted full text
  safety: {
    hazards: Hazard[]              // { class, severity, mitigation }
    ppe: string[]                  // e.g. ["safety goggles","gloves"]
    allergensIngestion: string[]   // food/allergen + ingestion notes
    disposal: { class, instructions, environmentalNote }
    photosensitivitySensory: string[] // strobe/flash/loud/odor flags
    prohibitedSubstitutions: string[]  // "do NOT substitute X with Y"
    firstAidRef: link              // links official guidance; not first-aid instruction
    exclusionCheck: "pass"         // CI-asserted; a guide hitting the exclusion list cannot exist here
  }
  readingLevel: { target, measured }
  sources: Citation[]              // { org, title, url, retrievedDate, sourceLicense }
  reviewStatus: "draft"|"in-review"|"science-approved"|"safety-approved"|"published"
  authoredBy: string               // author/educator
  scienceReviewedBy: string        // curriculum/science accuracy reviewer (distinct from author)
  safetyApprovedBy: string         // credentialed safety reviewer (distinct from author)
  reviewLogRef: string             // PR-tied, append-only review-log entry
  lastReviewed: date
  lang: string
  contentLicense: "CC-BY-4.0"
  contentVersion: string
  integrityHash: string
  hardInvalidate: boolean          // true => purge cached copies & force refresh (non-dismissible)
}
```

**Key decisions (recorded as ADRs in M0).**
1. **Content format** (JSON vs. MDX) — decided **first**; the schema + precaching depend on it.
2. Static-site generator + service-worker tooling, precache budget/eviction, content-version
   manifest / hard-invalidation mechanism.
3. Hazard taxonomy + safety-rubric structure + **hard exclusion list** representation (how it is
   encoded so CI can enforce it).
4. Curriculum-crosswalk model (how alignments are stored to stay additive and license-clean).
5. Hosting target, versioning/update strategy for cached clients, and PDF/print approach.

**Decision ordering (important).** The **content-format ADR (#1)** lands **before** the guide schema
is finalized and before any content precaching is built. The **hard-exclusion-list ADR (#3)** lands
**before** the first guide is authored, so safety enforcement exists before any guide. Until those
ADRs land, the schema above is **provisional**. TASKS.md sequences these dependencies explicitly.

## Data, licensing & compliance

**This section is load-bearing for a medium-risk safety + curriculum project. Be conservative.**

**Content sources.** Guides are authored originally and informed by **open / public-domain / CC**
educational and safety sources: openly-licensed OER (e.g. CC-BY OpenStax, CK-12, PhET descriptions
where licensing permits), **public-domain government science/education material**, and **authoritative
lab-safety guidance** (e.g. national science-teacher associations' published safety guidelines,
occupational-safety agencies, poison-control/first-aid authorities — cited and linked, not copied).
Every guide records its `sources[]` with org, title, URL, retrieval date, and license.

**Curriculum-standard handling (critical, often misunderstood).** Standards frameworks have
**different licenses**, and many are restrictive:
- **Map by code + link, do not reproduce restricted full text.** We store the **standard code**
  (a fact) and a **link** to the official statement, plus **our own** alignment rationale. We do not
  paste full standard text where the framework's license forbids reuse.
- **NGSS** is free to use but is **© Achieve, Inc.**, typically requiring attribution and carrying
  **non-commercial-style** reuse conditions — verified per use; attribution recorded.
- **Crown-copyright / national curricula** (e.g. UK National Curriculum under the Open Government
  Licence, or other national frameworks) have their own terms — verified per framework before mapping;
  where reuse is not permitted we link only.
- The crosswalk is built so a framework whose license we cannot clear is **referenced by code/link
  only**, never embedded.

**Licensing rigor.**
- **Our outputs:** code **MIT**; content **CC-BY-4.0**.
- **Source reuse:** verify each source's terms before any reuse; **paraphrase and cite, never copy
  verbatim**; never reuse third-party logos/trademarks or kit-vendor proprietary procedures. Where a
  source is unclear or restrictive, **link, don't embed**. Provenance + license recorded per guide.
- **Images/diagrams:** only original or open/PD/CC-licensed media, attribution recorded; no scraped
  textbook figures.
- **Translations:** derivative works under the same source rules; reviewed for **safety accuracy**,
  not just fluency.

**Privacy / PII stance.** **Zero student PII.** No accounts, no analytics, no telemetry, no
third-party scripts, no cookies beyond what the service worker needs offline. The site is static and
read-only; nothing about a learner is collected. The **incident-report channel** must accept reports
**without** requiring personal data and must not solicit student-identifying information; any
incidental PII received is minimized and not committed to the repo.

**Attribution & non-endorsement.** Source orgs and standards bodies are credited per guide and on a
credits page. We do **not** imply endorsement by any agency, standards body, or school we cite unless
they have explicitly endorsed the project.

**Scientific-accuracy & non-partisan stance.** Where a topic is socially contested but scientifically
settled (evolution, climate change, vaccines), guides present **accurate, sourced consensus science**
factually and without political editorializing, and avoid framing that targets or demeans any group.

## Quality, review & risk gates

**Risk tier: medium.** Domain-accuracy **and** hazard-safety review are mandatory; a mis-stated
experiment can cause physical harm.

**Required reviews before a deed is "done":**
- **Code / site tasks:** maintainer code review + CI green (lint, typecheck, unit, schema-validation,
  **exclusion-list**, **cost-ceiling**, **readability**, **a11y**, **offline E2E**). Accessibility and
  exclusion-list regressions block merge.
- **Content tasks (medium risk) — dual review, no self-approval:**
  - **Science/curriculum review:** a reviewer with relevant subject knowledge verifies the science is
    correct, misconceptions are addressed, and the curriculum alignment (codes + rationale) is valid.
  - **Safety review (credentialed):** a **distinct** reviewer who meets the safety credential bar
    confirms hazards, PPE, minimum age/supervision, allergen/ingestion, disposal, and prohibited
    substitutions, and confirms the guide does **not** trip the hard exclusion list.
  - **Role separation:** `authoredBy`, `scienceReviewedBy`, and `safetyApprovedBy` must be **distinct
    people**; the author may not approve their own guide on either axis.
  - **Safety credential bar:** a qualified science teacher with documented lab-safety training, a
    school/lab safety officer, an industrial-hygiene/occupational-safety professional, or an
    equivalent recognized qualification — recorded with the sign-off.
  - **Dry-run / reproduction:** each guide is **physically dry-run or reproduced by a second educator**
    (not the author) before publish, confirming materials, cost, timing, and that the procedure works
    as written — recorded in the review log.
  - **Tamper-evident review log:** every approval writes a **PR-tied, append-only** entry (PR #, commit
    SHA, `contentVersion`, the three named roles, sources checked, exclusion-check result, dry-run
    result, any divergence decision). This is the auditable record the *Definition of Shipped* checks.
- **Accessibility:** every UI-affecting change passes automated checks **and** a **manual
  assistive-technology audit** across a defined support matrix (NVDA+Firefox/Win, JAWS+Chrome/Win,
  VoiceOver+Safari/macOS·iOS, TalkBack+Chrome/Android, plus keyboard-only per desktop browser),
  signed off by a qualified accessibility reviewer; cadence is before each milestone exit and each
  production release, with regression passes on navigation/focus/interaction changes.

**Definition of Shipped (project-level).** A deployed, accessible, offline-capable, printable library
that: (1) passes WCAG 2.2 AA (automated + manual); (2) works offline after first load and prints
cleanly; (3) ships only source-cited guides that pass **dual review (science/curriculum + credentialed
safety)** and the **hard exclusion list**, each **dry-run by a second educator**; (4) collects no
student PII/telemetry; (5) maps guides to ≥ 2 curriculum frameworks; and (6) is **adopted and
field-validated by a named partner** in real classrooms in that community's language(s). Until a
partner is secured, criterion (6) is **outstanding**.

**"Publicly Shipped (generic public good)" success state.** Criteria (1)–(5) can be fully met with no
partner. If, by a **decision point 6 months after the M3 build is production-ready**, no partner is
secured, the steward + Hee-Lee Oss governance may declare **"Publicly Shipped (generic public good)"**: the
library is deployed and distributed directly and via educator/OER channels, with outcomes tracked by
best-effort educator self-report. This is a recognized, honest success state distinct from the fuller
"Shipped (partner-validated)" state; a later endorsement upgrades the status rather than gating launch.

## Roadmap & milestones

Phased; each phase has measurable exit criteria. M0 is a thin cold-start foundation.

- **M0 — Foundation & cold-start (thin slice).**
  Goal: the safety + content scaffolding and one fully-reviewed sample guide.
  Exit criteria: repo + MIT/CC-BY licensing; **content-format ADR (#1) recorded before** the guide
  schema is finalized; **hazard taxonomy + safety rubric + hard exclusion list (ADR #3) recorded
  before** the first guide is authored; CI enforces schema-validation + exclusion-list +
  no-self-approval; **one sample guide** authored, science-reviewed, **credentialed-safety-approved**,
  and **dry-run by a second educator**, rendering from the schema with full citations; no-telemetry
  audit green (CSP `connect-src 'none'` + runtime interception E2E).

- **M1 — Safety framework hardening & first guide set.**
  Goal: the safety/cost/disposal model proven across a real spread of guides, plus an accessible
  browse/print site.
  Exit criteria: ≥ 8 guides across ≥ 2 disciplines and ≥ 2 grade bands, each dual-reviewed + dry-run;
  cost-ceiling + readability gates enforced in CI; static browse/filter + per-guide printable output
  works offline; WCAG 2.2 AA pass with manual AT audit; incident-report channel + triage process live.

- **M2 — Curriculum alignment & i18n.**
  Goal: standards crosswalk and the first non-English localization.
  Exit criteria: code-level crosswalk to ≥ 2 frameworks with alignment review and license-clean
  handling (codes/links, no restricted full text); i18n framework with build-time completeness check;
  ≥ 1 non-English locale complete for UI + ≥ 1 guide; safe fallback; localized safety terms
  accuracy-reviewed.

- **M3 — Scale, partner adoption & classroom validation.**
  Goal: breadth, a named partner, real-classroom field-testing, and the full Definition of Shipped.
  Exit criteria: ≥ 30 reviewed guides across ≥ 3 disciplines × ≥ 3 grade bands; ≥ 2 frameworks
  mapped; ≥ 2 languages; **named partner endorsement/adoption on file**; ≥ 5 guides **field-tested in
  real classrooms** with feedback incorporated; production build deployed; outcomes-tracking +
  annual safety re-review cadence operational.

Dependencies: M1 depends on M0 (schema + safety framework). M2 depends on M1 (stable guides + site).
M3 depends on M2 (aligned, multilingual base) and on the **partner being secured** (pursued in
parallel from M1).

## Work breakdown

The itemized, schema-mapped backlog lives in **TASKS.md**, organized by the M0–M3 milestones above.
Each task maps to a Hee-Lee Oss Task JSON (see schema), is sized (small/medium/large), risk-tagged, and
names a reviewer. TASKS.md also includes acceptance criteria for the most important tasks per
milestone, milestone Definitions of Done, a backlog, and a complete, schema-valid example Task JSON.

## Governance, roles & stakeholders

- **Maintainer (Owner): TBD.** Owns the repo, roadmap, releases, schema, and review standards.
- **Code reviewers:** rotation of TS/static-site-competent contributors; ≥ 1 approval + CI green.
- **Science/curriculum reviewers:** contributors with subject + standards knowledge per discipline.
- **Safety reviewers (credentialed):** qualified science teachers with lab-safety training, school/lab
  safety officers, or occupational-safety/industrial-hygiene professionals; **distinct from the
  author**; sign off against the hazard taxonomy + exclusion list.
- **Reproduction/dry-run educators:** a second educator who physically runs each guide before publish.
- **Accessibility reviewer:** contributor competent with assistive tech; performs manual audits.
- **Translation reviewers:** competent speakers per locale, paired with a safety-accuracy re-check.
- **Steward (last-mile owner): TBD** — owns deployment, the partner relationship, classroom
  field-testing, and the incident-triage process.
- **Partner / requestor: TO BE SECURED** — a named school/district, teacher association, or OER/
  education nonprofit confirming need, priorities, and field-validating in classrooms.
- **Hee-Lee Oss governance/board:** arbitrates edge cases, exclusion-list changes, and risk-tier decisions.

## Dependencies & integrations

- **External content sources:** open/PD/CC OER (OpenStax, CK-12, PhET per license), public-domain
  government science/education material, published lab-safety guidance, poison-control/first-aid
  authorities (read-only references; license-checked).
- **Curriculum frameworks:** NGSS (© Achieve; attribution + reuse terms verified) and ≥ 1 national/
  regional framework (license verified; codes/links where reuse is restricted).
- **Tooling/libraries:** static-site generator, service-worker/PWA tooling, i18n library, readability
  checker, test stack (Vitest, Playwright, axe-core/pa11y), client PDF/print.
- **Hosting:** static host (GitHub Pages / Netlify / Cloudflare Pages) — no app server.
- **Hee-Lee Oss pieces:** Task schema (`packages/schema`), CLI workspace prep / PR flow (donated lane),
  good-deed definition & risk-tier governance, review/sign-off process.
- **Human/expert dependency:** credentialed safety reviewers, science/curriculum reviewers,
  reproduction educators, and a partner org — the gating non-software dependencies.

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| A published guide causes physical injury (burn, eye, fire, ingestion, shock) | Low–Medium | High | Mandatory credentialed safety review (author ≠ approver); hard exclusion list enforced in CI; per-step safety callouts, PPE, min-age/supervision, disposal; second-educator dry-run; incident channel + 72h triage + hard-invalidation | Safety reviewer / Steward |
| Dangerous "viral" experiment slips into scope | Low | High | Hard exclusion list encoded + CI-enforced; exclusion check recorded in review log; governance approves any list change | Maintainer |
| Curriculum-standard copyright misuse (e.g. pasting NGSS/Crown text) | Medium | High | Map by code + link + own rationale; verify each framework license; never embed restricted text; provenance log | Maintainer |
| Source content copyright/trademark misuse (textbooks, kit vendors) | Medium | High | Paraphrase + cite, never copy verbatim; only open/PD/CC media; "link, don't embed" default | Maintainer |
| Inaccurate science / reinforced misconception | Medium | Medium–High | Science/curriculum review distinct from author; misconceptions field required; sources cited | Science reviewer |
| Allergen/ingestion harm from food-based experiments | Medium | High | Allergen + ingestion flags required; "do not ingest non-food chemicals"; prohibited-substitution list; safety review | Safety reviewer |
| No partner secured (verified need unconfirmed) | Medium | High | Pursue partner from M1; 6-month-post-M3 decision point to declare "Publicly Shipped (generic public good)"; later endorsement upgrades status | Steward |
| Content goes stale vs. updated safety/curriculum guidance | High | Medium | `lastReviewed` dates + **annual** safety re-review; re-review after any incident or guidance change; staleness flagging | Safety reviewer |
| Translation introduces a safety error | Medium | High | Translations re-checked for safety meaning, not just fluency; competent speaker + safety reviewer pair | Translation reviewer |
| Accessibility regressions slip in | Medium | High | a11y CI gate blocking merge; periodic manual AT audits; AA hard requirement; printable + offline | A11y reviewer |
| Cost/equipment creep makes guides unusable in low-resource settings | Medium | Medium | Per-guide cost ceiling enforced in CI; substitutions required; "no special lab equipment" check | Maintainer |
| Hostile fork implies false endorsement by a school/agency | Low | Medium | Non-endorsement disclaimer; trademark/attribution terms; "not an official product unless endorsed" notice | Maintainer |
| Maintainer bandwidth / bus factor | Medium | Medium | Reviewer rotation, documented processes, MIT/CC-BY low lock-in | Maintainer |

## Security & privacy

**Threat surface.** As a static, no-backend, no-PII site the attack surface is small. Principal
concerns: (1) supply-chain risk in dependencies, (2) service-worker cache poisoning / stale-content
risk for safety content, (3) third-party script/tracker creep, (4) hostile forks implying false
endorsement, (5) incidental PII arriving via the incident-report channel.

**Controls.**
- **No secrets** in the app; static hosting only; no API keys/tokens/credentials in code, logs, or
  receipts (per Hee-Lee Oss rule).
- **No telemetry / no student PII — defense in depth:** strict CSP with **`connect-src 'none'`**
  (plus locked-down `script-src`/`img-src`/`font-src 'self'`); a **runtime network-interception E2E**
  that fails the build on any unexpected outbound request; and a static CI audit for trackers/PII
  fields. The incident channel collects reports **without** requiring personal data; incidental PII is
  minimized and never committed.
- **Supply chain:** pinned/locked deps (pnpm lockfile), dependency review, minimal deps, Subresource
  Integrity where applicable, CI dependency audit.
- **Service-worker hygiene & forced invalidation:** scoped SW, integrity-checked precache, explicit
  versioning; a **content-version manifest** with per-guide `integrityHash` + `hardInvalidate` so a
  corrected or withdrawn guide is purged and force-refreshed (non-dismissible) — an unsafe guide is
  never served stale from cache; HTTPS-only.
- **Content integrity:** all guides source-cited, dual-reviewed, exclusion-checked, and dry-run.
- **Abuse/misuse:** prominent disclaimer that the resource is educational, requires the stated adult
  supervision, and is not an official product unless a named partner endorses it; trademark/attribution
  terms documented; license requires attribution.

## Sustainability & maintenance

- **Ownership after delivery:** the **maintainer** owns code/releases/schema; the **steward** owns
  deployment, partner relationship, classroom field-testing, and incident triage. Both are **TBD** and
  must be named before M3.
- **Content & safety freshness:** guides carry `lastReviewed`; a **re-review cadence — at least
  annually, and immediately after any reported incident or change in official safety/curriculum
  guidance** — is enforced via maintenance tasks; stale guides are flagged and may be hard-invalidated.
- **Outcomes tracking:** no telemetry, so adoption/usefulness/incidents are tracked via **educator/
  partner self-report**, the **incident-report channel**, and a manual record of endorsements/MOUs —
  an explicit privacy/measurement trade-off.
- **Low lock-in:** MIT/CC-BY, static hosting, standard web tech, and forkable structured content keep
  the project cheap to run and survivable.

## Open questions

1. **Partner org:** Who is the named partner (school/district, teacher association, OER nonprofit)?
   The need is plausible but unverified — a human decision is required before full *Definition of
   Shipped*.
2. **Priority disciplines, grade bands, and material-availability constraints:** should be
   partner-driven once secured.
3. **Priority curriculum frameworks:** NGSS first (license terms confirmed) + which second framework?
4. **Priority languages:** first non-English locale (provisional pending a partner).
5. **Safety-credential bar specifics & reviewer recruitment:** how do we source and verify
   credentialed safety reviewers, and is a one-time legal review of our standards-reuse + liability
   disclaimer warranted?
6. **Hard exclusion list ratification:** the initial list needs governance/expert ratification and a
   defined change process.
7. **Hosting/deployment target** and who operates it (steward).
8. **Field-testing protocol:** how classroom validation is run safely and consent/PII-free.

## References

- Hee-Lee Oss work rules — `C:\code\hee-lee-oss\CLAUDE.md`
- Good-deed definition & risk tiers — `C:\code\hee-lee-oss\docs\good-deed-definition.md`
- Task schema — `C:\code\hee-lee-oss\packages\schema\src\schemas.ts`
- Portfolio roadmap — `C:\code\hee-lee-oss\planning\ROADMAP.md`
- Exemplar plan (depth/structure reference) — `C:\code\Ofelia\plan.md`
- Sibling medium-risk plan (house style) — `C:\code\hee-lee-oss\planning\projects\proper-prepper\PLAN.md`
- Open content/standards sources (license-checked per use): OpenStax, CK-12, PhET; NGSS (© Achieve,
  Inc.); national curricula (e.g. UK National Curriculum under OGL); published science-teacher-
  association lab-safety guidance; occupational-safety and poison-control/first-aid authorities.
- WCAG 2.2 AA (W3C Web Content Accessibility Guidelines).

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified against the first draft and **applied** to the
PLAN and TASKS above (not merely proposed). Each notes what changed and where.

1. **Hard exclusion list, CI-enforced.** Added a concrete, versioned list of barred activity classes
   (concentrated acids/bases, toxic gases, explosives/pyrotechnics, mains/high-voltage, pathogens,
   etc.) enforced as a CI gate, not just prose — *Scope, Solution approach, Quality gates, ADR #3*.
2. **Triple role separation (author ≠ science reviewer ≠ safety approver).** Strengthened the
   no-self-approval rule across two review axes — *Quality gates, data model, TASKS review rule*.
3. **Credentialed safety-reviewer bar defined.** Named the qualifying credentials rather than a vague
   "expert" — *Quality gates, Governance*.
4. **Second-educator physical dry-run/reproduction before publish.** Added a reproducibility gate so
   guides are confirmed to actually work and be affordable — *Quality gates, data model, TASKS*.
5. **Per-guide cost ceiling enforced in CI.** Made "low-cost" measurable and machine-checked with a
   substitution model for unavailable items — *Goals, Solution approach, Success metrics, M1 exit*.
6. **Curriculum-standard licensing handled by code+link, not full-text reuse.** Prevented a common,
   real copyright trap (NGSS © Achieve, Crown copyright) — *Data/licensing, Dependencies, Risks*.
7. **Allergen & ingestion safety as first-class fields.** Food-based experiments now carry allergen +
   "do not ingest non-food chemicals" flags — *data model, Risks, Quality gates*.
8. **Disposal & environmental safety per guide.** Added a disposal class + environmental note so
   guides don't cause downstream harm — *data model, Goals*.
9. **Minimum age + supervision level required.** Explicit `minAge` + `supervision` enum on every guide
   — *data model, Quality gates*.
10. **Photosensitivity/seizure & sensory flags.** Strobe/flash/loud/odor activities flagged for
    safety and accessibility — *data model*.
11. **Incident-report channel + 72h triage + hard-invalidation.** A real feedback/withdrawal loop so a
    dangerous guide can be pulled fast — *Solution approach, Success metrics, Security, Sustainability*.
12. **Zero-harm-incidents as the headline success metric.** Reframed metrics so safety outranks reach
    — *Success metrics*.
13. **Reading-level target per grade band, CI-checked.** Ensures learner-facing text is age-appropriate
    — *Success metrics, Solution approach, M1 exit*.
14. **WCAG 2.2 AA + printable + offline for low-resource/low-connectivity use.** Accessibility and
    offline are hard gates, not nice-to-haves — *Goals, Solution approach, Quality gates*.
15. **Content-version manifest + integrity hash + forced refresh.** Borrowed the safety-content
    integrity pattern so corrections can't be served stale — *Solution approach, Security*.
16. **Non-partisan / consensus-science stance.** Explicit handling of contested-but-settled topics
    (evolution, climate, vaccines) — accurate, sourced, non-editorial — *Non-goals, Data/licensing*.
17. **Decision ordering for ADRs.** Content-format ADR before schema; exclusion-list ADR before the
    first guide — sequencing made explicit — *Solution approach, M0 exit, TASKS sequencing rule*.
18. **i18n with units + locale formatting + safety-term review.** Metric/imperial, ICU pluralization,
    and safety terms re-checked for accuracy on translation — *Solution approach, M2*.
19. **No-telemetry/no-PII via defense in depth.** CSP `connect-src 'none'` + runtime network-
    interception E2E + static audit, not a grep alone — *Success metrics, Security, M0/TASKS*.
20. **Incident channel collects no required PII.** Closed a privacy gap created by the feedback loop —
    *Data/licensing, Security*.
21. **"Publicly Shipped (generic public good)" fallback state + 6-month decision point.** A finished
    library isn't stranded if no partner is found — *Quality gates, M3, Risks*.
22. **Honest verifiedNeed=false / requestor=TBD default.** No invented partner; status explicitly TO
    BE SECURED — *Executive summary, Problem, TASKS mapping + example JSON*.
23. **Outcome de-duplication & windows.** Distinct educators/class groups over a rolling 12-month
    window, no student-level counting — *Success metrics*.
24. **Materials-availability / "no special lab equipment" check.** Guides must be runnable without a
    lab; substitution required — *Scope, Risks, M1*.
25. **Annual + event-driven safety re-review cadence.** Re-review at least yearly and after any
    incident or guidance change, with staleness flagging — *Sustainability, Risks, backlog task*.

---

## Review sign-off

**Reviewed for completeness against the 17-section spec.** All required H2 sections are present and in
order: Executive summary; Problem & beneficiaries; Goals and non-goals; Success metrics (outcomes);
Scope; Solution approach & architecture; Data, licensing & compliance; Quality, review & risk gates;
Roadmap & milestones; Work breakdown; Governance, roles & stakeholders; Dependencies & integrations;
Risks & mitigations; Security & privacy; Sustainability & maintenance; Open questions; References —
plus Appendix A and this sign-off.

**Reviewed for correctness against Hee-Lee Oss rules and the good-deed definition.**
- *Good-deed criteria:* tangible public benefit (free, safe science labs), freely available (MIT /
  CC-BY-4.0), not primarily for-profit (no kit sales/lead-gen), no harm/discrimination/misinformation
  (hard exclusion list + consensus-science stance), specific enough for AI sessions with required
  human/expert review — all satisfied.
- *Risk tier:* correctly set to **medium** with the binding consequence (credentialed safety review +
  hard exclusion list + dry-run) made explicit; high-hazard activity is **excluded**, not gated.
- *Guardrails:* license/provenance (open/PD/CC only, per-source verification, standards by code+link),
  privacy/PII (zero student PII, incident channel collects none), non-partisan/consensus science, and
  expert review for safety/curriculum accuracy with a "not a substitute for local regs/supervision"
  framing — all present.
- *Partner honesty:* partner and verified need are marked **TO BE SECURED**; `verifiedNeed=false`,
  `requestor=TBD` everywhere, with a defined path to flip them and a no-partner fallback success state.

**Fixes applied during review.** (1) Aligned the Definition of Shipped (6 criteria) with the M3 exit
criteria and success metrics so they are mutually consistent. (2) Ensured the data model's review
fields (`authoredBy`/`scienceReviewedBy`/`safetyApprovedBy`) match the governance roles and the TASKS
review rule exactly. (3) Confirmed every TASKS milestone maps to a roadmap phase and every example
Task JSON field is schema-valid (enums, required fields, funded-budget rule N/A for donated).

**Outstanding items requiring a human decision** (carried to *Open questions*): naming a partner;
ratifying the hard exclusion list + its change process; recruiting/verifying credentialed safety
reviewers; choosing the second curriculum framework + first non-English locale; and deciding whether a
one-time legal review of standards-reuse + the liability disclaimer is warranted.

**Status:** Draft v0.1.0 — ready for maintainer and Hee-Lee Oss-governance review.
