# Competitive + Improvement Analysis — oer-science-labs

> Scope: open, low-cost, **hands-on** (not virtual) science experiment guides for K–12 / early-college,
> targeting low-resource settings. Risk tier: medium (physical hazards). Analysis grounded in web
> research with cited sources. Reviewed against `PLAN.md` v0.1.0 and `TASKS.md`.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually mature for a v0.1.0 draft: all 17 spec sections present, an honest
`verifiedNeed=false` partner posture, a content-format-ADR-before-schema sequencing rule, and a
defensible "Publicly Shipped (generic public good)" fallback. The safety architecture is the
strongest part. Findings, ordered by importance:

**(a) Safety model — strong, but one structural tension.** The plan correctly makes safety
first-class: a published hazard taxonomy, a credentialed safety-reviewer bar (author ≠
science-reviewer ≠ safety-approver), a CI-enforced **hard exclusion list**, per-step callouts,
allergen/ingestion + disposal fields, second-educator physical dry-run, and an incident channel with
72h triage + non-dismissible hard-invalidation. This is more rigorous than essentially every
competitor surveyed. **The tension:** the plan markets to settings with "no lab, no budget, limited
connectivity" yet *also* requires a credentialed safety reviewer + a second educator to physically
dry-run every guide. The supply of credentialed lab-safety reviewers willing to volunteer is the
true bottleneck (Open Question 5 names it but doesn't size it). Recommend: (i) a tiered credential
model so low-hazard "kitchen-science" guides (e.g. density tower, shadow clocks) clear with a lighter
bar than heat/chemical guides; (ii) explicitly anchor the exclusion list and per-substance handling
to an existing authority — **CLEAPSS hazcards / Student Safety Sheets** and **NSTA/ACS school-safety
guidance** — rather than inventing a taxonomy from scratch (CLEAPSS is the de-facto UK school-science
safety authority and is exactly the wheel not to reinvent;
https://science.cleapss.org.uk/resources/student-safety-sheets/ ).

**(b) Virtual vs hands-on positioning is correct and is the moat — but under-stated as strategy.**
The plan is hands-on-only and treats simulations as out of scope. Research validates this as the gap:
PhET/Labster/Gizmos are all *simulations*, and the literature explicitly notes simulations "lack
procedural fidelity," don't build "hands-on skills such as optical alignment," and are less
motivating than real experiments (https://arxiv.org/pdf/2507.10286 ;
https://arxiv.org/pdf/2601.05433 ). The plan should state this contrast explicitly as the
differentiator (it currently buries it).

**(c) Low-resource / frugal-science feasibility — partially addressed, one gap.** Per-guide cost
ceiling + substitutions + "no special lab equipment" check are good and CI-enforced. But the plan
treats *materials availability* as a single global ceiling, when the real constraint is
**locale-specific availability** (a "$2" item may be unobtainable, not just unaffordable). The
substitution model exists but isn't tied to the i18n/locale layer. Recommend a per-locale
availability flag, and consider aligning with established frugal-science instruments (Foldscope ~\$1
paper microscope; https://www.goldengooseaward.org/01awardees/foldscopes ) so a guide can name a
known sub-\$1 tool rather than assume a school microscope.

**(d) Standards alignment — correct on licensing, thin on coverage realism.** The code+link-not-text
approach to NGSS (© Achieve) and Crown-copyright curricula is exactly right and avoids a real legal
trap. But "≥2 frameworks" with a single non-English locale is modest given the global low-resource
target; many priority beneficiaries sit under national curricula (India NCERT, Nigeria, Kenya, South
Africa CAPS) the plan doesn't yet name. Acceptable to defer to a partner, but list candidate
frameworks so M2 isn't blocked on the partner.

**(e) Accuracy & educator review — well-specified.** Distinct science reviewer + misconceptions field
+ dry-run reproduction is strong. Minor: the plan asserts reviewer *roles* but not reviewer
*throughput*; 30 guides × dual review × dry-run is a large human-labor commitment that should be
sized in TASKS (content-018 is "large" but the reviewer pipeline is the limiter, not authoring).

**(f) Accessibility — comprehensive.** WCAG 2.2 AA + manual AT matrix + printable + offline-after-
first-load is appropriate and notably exceeds PhET, whose own HTML5 sims still lack full
keyboard/screen-reader support (https://www.per-central.org/items/perc/4806.pdf ). Good.

**(g) Scope — appropriately bounded** by the hard exclusion list and non-goals; the
no-PII/no-telemetry defense-in-depth (CSP `connect-src 'none'` + runtime interception E2E) is
well above sector norm.

**Net:** correct and complete; the two load-bearing risks are *reviewer-supply scaling* and *not
reusing an existing safety authority*. Neither is a correctness defect, but both threaten delivery.

---

## 2. Competitive landscape

| Project | License / Cost | Type | Strength | Weakness vs. our niche |
| --- | --- | --- | --- | --- |
| **PhET (CU Boulder)** | CC-BY; code MIT/GPL; free | Virtual sims (125+), 121 languages, offline-capable | Huge reach, openly licensed, translated, free | **Simulations, not real experiments**; no hands-on skill, materials, or safety procedures; sim accessibility still partial |
| **Labster** | Proprietary, **paid** (~\$79–109+/student) | Virtual 3D labs (300+) | Polished, LMS/grading, course mapping | Paywalled; institutional-only; useless offline / no-budget; not open |
| **Gizmos (ExploreLearning)** | Proprietary, **paid** (~\$6/student; \$149 home) | Virtual sims (550+) | Standards-aligned, large library | Paid subscription; closed; virtual-only |
| **OpenStax** | **CC-BY-NC-SA**, free | Textbooks (not labs) | Peer-reviewed, free, trusted | NC clause; textbooks not experiments; no safety/hands-on procedures |
| **CK-12** | Custom "Curriculum Materials License" (free, but **not pure CC**) | FlexBooks + sims + practice | Free, standards-aligned, customizable | License is bespoke/restrictive for reuse; sims are virtual |
| **Foldscope / frugal science** | Hardware product + community | Physical \$1 instrument | Genuinely low-cost, field-proven in developing nations | A *tool*, not a curriculum of safety-reviewed guides |
| **Exploratorium Science Snacks** | **CC-BY-NC-SA 4.0**, free | 300+ hands-on activities, common materials | Closest analog: cheap, hands-on, teacher-tested | **NC clause** blocks some reuse; not systematically standards-mapped; safety not structured/credentialed; not offline-packaged |
| **RSC / Nuffield practical chemistry + CLEAPSS** | Free to use (RSC terms) | Hundreds of class experiments w/ CLEAPSS hazcards | **Gold-standard safety integration**; technician-grade | UK-curriculum-centric; assumes a school lab + technician; not low-resource/home; not openly forkable data |
| **Arduino Science Journal** (ex-Google) | Free, open-source | Phone-sensor data-logging app | Turns a phone into lab instruments; hands-on data | A tool/app, not guided safety-reviewed activities; needs a smartphone |
| **Lab-in-a-box / African science-kit programs** | Mixed (mostly project/NGO) | Physical kits + booklets | Proven distribution to low-resource schools | Hardware logistics; not an open, forkable, standards-mapped content bank |

Sources: PhET https://phet.colorado.edu/ , https://en.wikipedia.org/wiki/PhET_Interactive_Simulations ;
Labster https://www.labster.com/ , https://medium.com/@valeriya.ruta/labster-explained-pros-cons-and-pricing-of-a-virtual-laboratory-6d2bed5178b9 ;
Gizmos https://gizmos.explorelearning.com/ , https://help.explorelearning.com/en/articles/9000368-purchasing-gizmos ;
OpenStax https://openstax.org/license/ ; CK-12 https://www.ck12info.org/curriculum-materials-license/ ;
Foldscope https://www.goldengooseaward.org/01awardees/foldscopes , https://en.wikipedia.org/wiki/Foldscope ;
Exploratorium https://www.exploratorium.edu/snacks/about ; RSC/Nuffield https://edu.rsc.org/resources/collections/nuffield-practical-collection ,
CLEAPSS https://science.cleapss.org.uk/resources/student-safety-sheets/ ;
Arduino Science Journal https://blog.arduino.cc/2020/08/05/the-science-journal-is-graduating-from-google-coming-to-arduino-this-fall/ ;
lab-in-a-box https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12324123/ , https://today.usc.edu/low-cost-science-kits-help-fill-experimental-gaps-facing-african-undergraduates/ .

**Key landscape insight:** the market splits cleanly into (1) free-but-*virtual* (PhET, CK-12,
OpenStax), (2) paid-virtual (Labster, Gizmos), (3) free-hands-on-but-*not-low-resource-or-not-truly-
open* (Exploratorium NC-licensed; RSC/Nuffield lab-assuming, UK-centric), and (4) hardware tools
(Foldscope, Arduino, kits). **No one occupies the intersection: truly open (CC-BY, no NC),
hands-on, low-resource-feasible, credentialed-safety-reviewed, standards-mapped, offline/printable.**

---

## 3. Gaps we can fill

1. **The "open + hands-on + low-resource + safety-reviewed" intersection is empty.** The closest
   analog, Exploratorium Science Snacks, is **CC-BY-NC-SA** (NC blocks commercial reuse/remix) and
   has no structured, credentialed safety block or standards crosswalk. We are CC-BY (no NC) with a
   real safety apparatus.
2. **Structured, machine-checkable safety data.** Competitors put safety in prose. We make hazards,
   PPE, min-age, disposal, allergens, and a hard exclusion list **first-class schema fields enforced
   in CI** — uniquely auditable and forkable.
3. **Offline + printable by design** for zero/low connectivity. PhET runs offline but is virtual;
   Exploratorium/RSC are web pages. A precached, printable guide bank for a lab-less classroom is
   unserved.
4. **Genuinely low-resource costing.** A CI-enforced per-guide cost ceiling + substitution model is
   absent from all competitors; "low-cost" is asserted, never machine-verified.
5. **License-clean standards crosswalk across multiple national frameworks**, not just NGSS — a need
   none of the free OER players fully serves outside their home country.
6. **A neutral safety floor for the "viral home experiment" problem** — replacing dangerous,
   unsourced YouTube/TikTok demos with a vetted, exclusion-list-bounded alternative.

---

## 4. Differentiators to win (vs PhET sims and Labster)

1. **Real experiments, not simulations.** Research shows sims lack procedural fidelity and hands-on
   skill-building and are less motivating than physical work (https://arxiv.org/pdf/2507.10286 ).
   We deliver the thing simulations only approximate. *This is the single strongest differentiator.*
2. **Free + open + no account vs Labster's paywall.** Labster is institutional, paid, online-only;
   we are CC-BY, zero-cost, offline, no login, no PII.
3. **Credentialed, structured, CI-enforced safety** — beyond anyone open. We borrow the *rigor* of
   CLEAPSS/RSC but package it as open, forkable data for *non-lab* settings.
4. **Low-resource-native:** cost ceilings, substitutions, printable, offline — PhET/Labster all
   assume a device + (for Labster) connectivity + budget.
5. **Auditable provenance + non-dismissible safety invalidation** — a trust mechanism (integrity
   hash, review log, hard-invalidate) that closed commercial products don't expose and free PDF
   collections don't have.
6. **Standards-mapped + multilingual with safety-term re-review** — depth Exploratorium/Snacks lack.

---

## 5. Claude API leverage (and hard limits)

**Where Claude accelerates (all human-gated):**
- **Drafting structured guide content** to the fixed schema — first-pass procedure steps, materials
  lists with cost/substitution candidates, misconceptions, assessment/extension questions, and
  reading-level-targeted learner text per grade band. Big throughput win on the *authoring*
  bottleneck.
- **Safety *annotation drafting* (not assurance):** propose candidate hazards/PPE/disposal/allergen
  flags and cross-check a draft against the hard exclusion list as a **pre-screen** before a human
  safety reviewer — surfaces issues earlier, never approves.
- **Low-cost-materials substitution brainstorming** and locale-availability suggestions for the
  reviewer to verify.
- **Standards crosswalk drafting:** propose candidate NGSS/national codes + alignment rationale (by
  code/link, never pasting restricted text) for science-reviewer validation.
- **i18n/localization first drafts + a safety-term glossary diff** flagging where a translation may
  have altered hazard meaning — routed to the translation+safety reviewer.
- **Readability scoring, schema/citation lint assistance, and review-log summarization.**
- **MCP/agent tooling** to run the exclusion-list pre-screen and cost-ceiling check in authoring.

**Where Claude must NOT decide (hard guardrails, per CLAUDE.md + medium risk tier):**
- **Safety is expert-assured, never LLM-assured.** No guide ships on Claude's safety judgment; a
  *credentialed* human safety reviewer (distinct from author) signs off. An LLM hazard miss is a
  physical-injury risk.
- **Accuracy + pedagogy require an educator/science reviewer.** Claude can draft; it cannot be the
  science-correctness or curriculum-alignment authority.
- **No hazardous/dangerous procedures, ever.** Claude must refuse and flag anything tripping the
  exclusion list; it must not "optimize" a procedure toward higher hazard.
- **No unreviewed content reaches the published bank** — Claude output is always `draft`/`in-review`.
- **License verification is human-confirmed.** Claude may surface a source's stated license; a human
  verifies reuse terms (esp. NGSS © Achieve, Crown copyright, NC-licensed sources like Exploratorium)
  before any reuse.
- **No dry-run substitution.** Claude cannot replace the second-educator physical reproduction.

---

## 6. Ten concrete optimizations

1. **Anchor the hazard taxonomy + exclusion list to CLEAPSS / NSTA / ACS** rather than inventing it;
   cite hazcards/Student Safety Sheets per substance. Faster, more defensible, expert-trusted.
2. **Tier the safety-credential bar by hazard class** (light bar for no-heat/no-chemical "kitchen
   science"; full credential for heat/chemical) to unblock reviewer throughput without lowering the
   floor where it matters.
3. **Add a per-locale materials-availability flag** tied to the i18n layer, so "low-cost" also means
   "obtainable here," not just "cheap somewhere."
4. **Ship a Claude-assisted authoring + exclusion-list pre-screen tool** (MCP server) so drafts hit
   reviewers already schema-valid and pre-flagged — multiplies scarce reviewer time.
5. **Seed from license-compatible sources first:** Exploratorium ideas are CC-BY-**NC** (cannot be
   reused under our CC-BY) — instead originate guides informed by *public-domain government* + CC-BY
   PhET descriptions + RSC/Nuffield *method patterns* (cite, don't copy). Make license-compat a
   first-class authoring filter.
6. **Publish a "dangerous viral experiment" counter-index** — a short, safety-framed list mapping
   popular hazardous home demos to the vetted exclusion rationale + a safe alternative guide. High
   public-good value, strong differentiator, SEO/discovery magnet.
7. **Name candidate national frameworks now** (NGSS + e.g. India NCERT / South Africa CAPS / UK NC
   under OGL) so M2 isn't partner-blocked; build the crosswalk additively.
8. **Add an explicit reviewer-throughput plan / SLA** in TASKS (reviewers-per-discipline, guides-per-
   review-cycle) — the human pipeline, not authoring, is the real scaling constraint.
9. **Pair guides with frugal-science instruments** (Foldscope for biology, phone-sensor + Arduino
   Science Journal for physics data-logging) so "no lab equipment" still enables real measurement.
10. **Bundle an offline "classroom pack"** (zipped/printable PDF set per discipline+grade) for
    teachers with one-time connectivity — distributable via USB/SD, matching the lab-in-a-box
    distribution model that works in the field.

---

## 7. Parallel & perpendicular spin-offs

**Parallel (same model, adjacent domain):**
- **`lab-protocols-open`** — direct sibling: same schema + safety apparatus applied to *protocols*
  (bio/chem lab methods) for the early-college tier; shares the hazard taxonomy and review-log
  machinery. Strongest reuse candidate.
- **`bioinformatics-from-zero`** — perpendicular: *zero-hazard, no-materials* computational science;
  removes the safety bottleneck entirely and can scale faster, complementing the hands-on bank (and
  pairs with Foldscope imaging downstream).
- **`math-manipulatives-printables`** — shares the printable/offline/low-resource delivery layer and
  reading-level + a11y CI gates; no safety review needed, so it can prove the delivery stack quickly.
- **`oer-everything`** — umbrella/aggregator: a shared OER index + common schema, license-verification
  tooling, and crosswalk model across all sibling projects; oer-science-labs becomes its
  highest-rigor exemplar.

**Perpendicular / new artifacts:**
- **A frugal-science lab-kit library** — a parametric, openly-licensed bill-of-materials + build
  guides for sub-\$X instruments (Foldscope-style microscope, phone spectroscope, balance), with the
  same cost-ceiling + safety review, turning "no equipment" into "buildable equipment."
- **An MCP server ("safety-lint")** exposing the hazard taxonomy + exclusion-list pre-screen + cost-
  ceiling + readability checks as tools any Claude/agent authoring workflow (across all siblings) can
  call — productizes the safety machinery as reusable Hee-Lee Oss infrastructure.

---

## 8. Open questions

1. **Reviewer supply at scale:** how are credentialed safety reviewers + dry-run educators recruited,
   verified, and *throughput-budgeted* for 30+ guides? (The true delivery bottleneck.)
2. **Adopt vs invent the safety authority:** commit to CLEAPSS/NSTA/ACS as the citable basis, or
   maintain an independent taxonomy? (Affects defensibility + legal exposure.)
3. **Liability + disclaimer:** is a one-time legal review of the standards-reuse + injury-liability
   disclaimer warranted before any hands-on guide is published? (Plan flags this; needs a decision.)
4. **Tiered credential bar:** acceptable to governance, or must every guide clear the full bar?
5. **Source-license compatibility:** confirm the seed-source list excludes NC-only material
   (Exploratorium, OpenStax NC, CK-12 bespoke license) from *reuse* under our CC-BY.
6. **National frameworks + first non-English locale** — choose candidates now or hard-block on a
   partner?
7. **Named partner** — still TO BE SECURED; gates the full Definition of Shipped.
8. **Frugal-instrument scope** — does an instrument-build library belong inside this repo or as the
   spin-off kit-library?

---

## Summary (for relay)

**Top 3 competitors:** (1) **PhET** — free, CC-BY, 125+ sims in 121 languages, the dominant open
player, but *virtual only*; (2) **Labster** — polished 300+ virtual labs, but proprietary and
paywalled (~\$79–109+/student), useless offline/no-budget; (3) **Exploratorium Science Snacks** —
the closest hands-on analog (300+ cheap activities) but **CC-BY-NC** (no commercial reuse), no
structured/credentialed safety, not standards-mapped or offline-packaged. (Honorable mentions:
Gizmos paid-virtual; CK-12/OpenStax free-but-textbook/virtual with non-pure-CC licenses; RSC/Nuffield
+ CLEAPSS, the safety gold standard but lab- and UK-centric; Foldscope/Arduino/lab-in-a-box as
tools/distribution, not open guide banks.)

**Single strongest differentiator:** we deliver **real, low-resource, hands-on experiments with
open (CC-BY) credentialed-safety-reviewed, CI-enforced structured safety data** — the empty
intersection no competitor occupies. The whole open market is *virtual* sims; the hands-on players
are either NC-licensed, lab-assuming, or not truly open. Research confirms simulations lack
procedural fidelity, hands-on skill, and motivation versus real experiments.

**Top 3 Claude-API ideas:** (1) draft schema-structured guides (procedure, costed materials +
substitutions, misconceptions, grade-targeted readable text) to multiply scarce authoring/reviewer
time; (2) a **safety-annotation + exclusion-list pre-screen** (MCP "safety-lint" server) that flags
hazards before — never instead of — a credentialed human reviewer; (3) localization first-drafts with
an automated **safety-term-drift diff** routed to translation+safety reviewers.

**Two most important plan-correctness findings:** (1) **Safety scaling tension** — the plan's
mandatory *credentialed* safety reviewer + second-educator physical dry-run per guide is excellent for
the medium risk tier and beats every competitor, but reviewer *supply/throughput* (not authoring) is
the real delivery bottleneck and is under-sized; mitigate via a hazard-tiered credential bar and a
Claude pre-screen. (2) **Reinventing the safety wheel + license traps** — anchor the hazard taxonomy
and exclusion list to existing authorities (CLEAPSS hazcards, NSTA/ACS) instead of inventing them,
and make license-compatibility a first-class authoring filter, since the most obvious seed sources
(Exploratorium, OpenStax, CK-12) are NC/bespoke-licensed and **cannot be reused** under our CC-BY.
