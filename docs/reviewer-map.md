# Review map: implementation, evidence and next validation

[Home](../README.md) · [日本語](reviewer-map.ja.md) · [Hands-on guide](demo-guide.md)

This page connects the product claims to the working demonstration and retained evidence. **Implemented** means checked in the retained source; **recorded test** means a versioned technical result; **future evaluation** means no outcome claim is made.

## Review the product in three passes

1. **Understand:** read the [system and evidence diagrams](architecture.md). Identify who owns the next action, which source supports a decision, and who can close the pathway.
2. **Try:** follow [CL-001](demo-guide.md) using the supplied [completion and correction PDFs](../demo-data/README.md). Inspect the resulting case, sources and history. Use CL-002 for the handoff example.
3. **Assess:** compare the behaviours below with [versioned results](validation.md), [operating controls](security-and-operations.md) and [limitations](scope-and-limitations.md).

## Function-to-evidence map

| Capability | Implementation / demonstration | Available evidence | Boundary |
| --- | --- | --- | --- |
| Find a gap after a recorded visit | Source-linked rules distinguish a visit from procedure completion | CL-001 guide; v0.4.11 source-language and workflow tests | Phrase matching does not establish clinical completeness. |
| Keep responsibility clear | Current owner remains until handoff acceptance; next action has owner and schedule | CL-002; v0.4.11 workflow/pathway tests | Acceptance is simulated; no receiving-provider authentication. |
| Trace PDF evidence | Original bytes, page text/hashes, explicit comparison and same-case registration | Published fixtures; v0.4.11 PDF/API walkthrough | Text PDFs only; no OCR or issuer verification. |
| Handle later events and corrections differently | New event added; correction explicitly supersedes a report; old material retained | CL-001 guide; API and browser correction records | Constructed scenario, not a clinical outcome study. |
| Require current human decisions | Source-bound judgments, required confirmations, action completion and current review gate closure | v0.4.11 workflow, AI-control and completion tests | Demo persona, not authenticated clinical sign-off. |
| Respond to patient needs | Guidance responses, clarification requests, support preferences and holds | v0.4.11 patient-response/pathway tests | No measured comprehension or patient-use study. |
| Keep alternative outcomes distinct | Evidence-backed decline/alternative disposition; no false procedure-completion flag | v0.4.11 pathway tests | Local clinical policy still needs approval. |
| Maintain state under change | Revision conflicts, scoped sessions, retained histories and usage limits | v0.4.11 SQL/Firestore-emulator and isolation tests | No production load or service-level validation. |
| Support EN / JA / AR | Shared records, Arabic RTL, locale-specific scheduling | Current EN/JA reachability and observed Japanese schedule label; historical language checks | Specialist-language validation is outstanding; UI language does not translate originals. |

Test families are identified in the [public regression breakdown](../evidence/backend-regression-v0.4.11.json). The original application source and full test suite are not in this repository; the hosted walkthrough can be repeated, but the 1,011-test run cannot be rebuilt from this repository alone.

## Coverage of the assessment topics

The [official challenge page](https://hack2skill.com/event/futurehealthchallenge/) lists six assessment areas (checked 3 November 2026). The labels below paraphrase those areas; this is a document map, not an organizer endorsement or a claim that formal submission is complete.

| Assessment topic | Where to inspect CareLoop | Present status |
| --- | --- | --- |
| Health need and potential benefit | [Problem and scenario](../README.md), CL-001 walkthrough | Follow-up gap demonstrated with fictional records; health benefit unmeasured. |
| System design and technical substance | [Architecture](architecture.md), source lifecycle, data relationships and AI boundary | Implemented prototype architecture documented against retained source. |
| Observable working behaviour | [Hands-on guide](demo-guide.md), [fixtures](../demo-data/README.md), [validation](validation.md) | Hosted interaction and versioned technical results available. |
| AI oversight and data controls | [Access and data controls](security-and-operations.md) | Source validation, human decisions and demo boundaries documented; no independent safety certification. |
| Operating model and scale | [Capacity, dependencies, failure handling and cost assumptions](security-and-operations.md) | Low-volume demonstration; scaling and production resilience unvalidated. |
| Adoption and a route to pilot | Pilot hypothesis below | Intended users and evaluation questions defined; no confirmed pilot, price or customer outcome claimed. |

## Pilot hypothesis and measurable questions

The intended users are screening coordinators and clinicians following an abnormal result across teams. A plausible initial sponsor is a provider or screening programme responsible for completing that follow-up. The proposition to test is whether source-linked work and explicit ownership reduce untracked gaps and make changed evidence easier to review. This is an adoption hypothesis, not a validated commercial offer.

| Future question | Proposed measure | Evidence needed |
| --- | --- | --- |
| Does follow-up become more complete? | Proportion of eligible pathways with documented, appropriate disposition | Institution-defined eligibility and completion criteria, baseline and follow-up period. |
| Is action taken sooner? | Time from actionable result to accepted owner and next appropriate action | Comparable timestamps and case-mix review. |
| Does source review improve? | Unresolved discrepancies and incorrect closure decisions in adjudicated scenarios | Independent expert labels, fixed cases and documented error review. |
| Does coordination take less effort? | Staff time per reviewed case and handoff effort | Observed tasks, denominator and comparison method. |
| Do patients understand their next step? | Task-based understanding, clarification needs and usability | Consented user study with language/access needs represented. |

Before a pilot, agree the local pathway, verified identities, data handling/retention, hosting/model routing, required integrations, escalation responsibility and evaluation protocol. Pricing, procurement requirements, willingness to pay and delivery cost need validation with an actual institution. No pilot date or partner commitment is implied.

## Publication boundary

This repository provides documentation, diagrams, selected illustrations, synthetic fixtures and sanitized technical summaries. Application source, private cloud configuration and full internal logs are not published. A reproducible application build or additional organizer-only material would require a separate delivery scope. The repository does not assert completion of registration, acceptance of terms or submission of the official form.
