# Review map: implementation, evidence and next validation

[Home](../README.md) · [日本語](reviewer-map.ja.md) · [Hands-on guide](demo-guide.md)

This page connects the product claims to the working demonstration and retained evidence. **Implemented** means checked in the retained source; **recorded test** means a versioned technical result; **future evaluation** means no outcome claim is made.

## Review the product in three passes

1. **Understand:** read the [system and evidence diagrams](architecture.md). Identify who owns the next action, which source supports a decision, and who can close the pathway.
2. **Try** the [hands-on guide](demo-guide.md). In CL-015, trace the overdue result to the source and assign follow-up. In CL-025, check attendance, record the next call and read the patient’s question. The guide also covers referral acceptance (CL-002), the corrected report (CL-006) and the optional [PDF exercise](../demo-data/README.md) (CL-001).
3. **Assess:** compare the behaviours below with [versioned results](validation.md), [operating controls](security-and-operations.md) and [limitations](scope-and-limitations.md).

## Function-to-evidence map

| Capability | Implementation / demonstration | Available evidence | Boundary |
| --- | --- | --- | --- |
| Find unfinished follow-up | The roster links work queues, priorities, owners and next actions | CL-015 result follow-up and CL-025 missed appointment in the 300-patient demo | Priority bands count records. Matching lists can show several records for the same patient. |
| Ask the record in natural language | Answers show recorded facts, source references and the matching list for worklist counts | RC32 clarification count and case-list check; RC6 case questions in English, Japanese and Arabic | Questions are read-only. These checks cover the demonstrated inputs. |
| Keep responsibility clear | Current owner remains until handoff acceptance; next action has owner and schedule | CL-006 owner/next-action view; CL-002 handoff; versioned workflow tests | Acceptance is simulated; no receiving-provider authentication. |
| Trace PDF evidence | Original bytes, page text/hashes, explicit comparison and same-case registration | Published fixtures; versioned PDF and hosted API checks | Text PDFs only; no OCR or issuer verification. |
| Handle later events and corrections differently | New event added; correction explicitly supersedes a report; old material retained | CL-006 prior closure and corrected report; optional CL-001 exercise; API checks | Constructed scenario, not a clinical outcome study. |
| Require current human decisions | Source-bound judgments, required confirmations, action completion and current review gate closure | v0.5.2 RC4 regression and hosted API checks | Demo persona, not authenticated clinical sign-off. |
| Respond to patient needs | Record the patient’s question and a staff reply; show the latest reply above the patient’s message field | CL-025 asks who will call to rebook, then receives the team’s answer | No measured change in patient understanding. |
| Keep alternative outcomes distinct | Evidence-backed decline/alternative disposition; no false procedure-completion flag | Versioned pathway regression tests | Local clinical policy still needs approval. |
| Maintain state under change | Revision conflicts, scoped sessions, retained histories and usage limits | RC4 full regression, including Firestore emulator; revision-conflict checks | No production load or service-level validation. |
| Support EN / JA / AR | Shared records, Arabic RTL, locale-specific scheduling | RC6 live question samples in EN/JA/AR; RC9 localized file-picker checks | Specialist-language validation is outstanding; UI language does not translate originals. |

The [RC4–RC9 verification record](../evidence/careloop-v0.5.2-verification.json) reports 1,247 backend tests on RC4 and 144 answer tests on RC6. Coverage overlaps. The [validation page](validation.md) records the RC32 walkthrough separately and identifies each run’s scope.

## Coverage of the assessment topics

The [official challenge page](https://hack2skill.com/event/futurehealthchallenge/) lists six assessment areas (checked 7 November 2026). The table maps each area to the relevant implementation and evidence.

| Assessment topic | Where to inspect CareLoop | Present status |
| --- | --- | --- |
| Health need and potential benefit | [Problem and scenario](../README.md), CL-015 and CL-025 | Unresolved follow-up is demonstrated with records created for the demo. Health benefit is unmeasured. |
| System design and technical substance | [Architecture](architecture.md), source lifecycle, data relationships and AI boundary | Implemented prototype architecture documented against retained source. |
| Observable working behaviour | [Hands-on guide](demo-guide.md), [fixtures](../demo-data/README.md), [validation](validation.md) | Hosted interaction and versioned technical results available. |
| AI oversight and data controls | [Access and data controls](security-and-operations.md) | Source validation, human decisions and demo boundaries documented; no independent safety certification. |
| Operating model and scale | [Capacity, dependencies, failure handling and cost assumptions](security-and-operations.md) | Low-volume demonstration; scaling and production resilience unvalidated. |
| Adoption and a route to pilot | Pilot hypothesis below | Intended users and evaluation questions defined; no confirmed pilot, price or customer outcome claimed. |

## Pilot hypothesis and measurable questions

The intended users are screening coordinators and clinicians following an abnormal result across teams. A plausible initial sponsor is a provider or screening programme responsible for completing that follow-up. The proposition to test is whether source-linked work and explicit ownership reduce untracked gaps and make changed evidence easier to review. This is an adoption hypothesis, not a validated commercial offer.

| Future question | Proposed measure | Evidence needed |
| --- | --- | --- |
| Does unresolved follow-up decrease? | Open required cases at a checkpoint / eligible actionable cases; appropriate dispositions tracked separately | Institution-defined eligibility and completion criteria, baseline and follow-up period. |
| Is action taken sooner? | Time from actionable result to a recorded next action with an accountable owner | Comparable timestamps and case-mix review. |
| Does source review improve? | Unresolved discrepancies and incorrect closure decisions in adjudicated scenarios | Independent expert labels, fixed cases and documented error review. |
| Does coordination take less effort? | Staff time per reviewed case and handoff effort | Observed tasks, denominator and comparison method. |
| Do patients understand their next step? | Task-based understanding, clarification needs and usability | Consented user study with language/access needs represented. |

Before a pilot, agree the local pathway, verified identities, data handling/retention, hosting/model routing, required integrations, escalation responsibility and evaluation protocol. Pricing, procurement requirements, willingness to pay and delivery cost need validation with an actual institution. No pilot date or partner commitment is implied.

## Publication boundary

This repository provides documentation, diagrams, selected illustrations, synthetic fixtures and sanitized technical summaries. Application source, private cloud configuration and full internal logs are not published. The repository supports public review and a hosted trial. Formal challenge submission is completed separately through the organizer’s portal and required deck template.
