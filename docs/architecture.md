# Architecture and evidence lifecycle

[Home](../README.md) · [日本語](architecture.ja.md) · [Controls and operations](security-and-operations.md) · [Implementation and evidence](reviewer-map.md)

CareLoop connects source documents, accountable teams and human decisions in a screening follow-up pathway. The API owns the workflow state and closure checks. The browser presents the record; optional AI proposes items for human review.

## System architecture

[![CareLoop architecture: browser, FastAPI on Cloud Run, Firestore, PDF originals and optional Vertex AI](../assets/architecture.svg)](../assets/architecture.svg)

The diagram describes the deployed prototype's component arrangement. Implementation details were checked against the retained **v0.4.11** source package. The public interface identifies itself as **v0.4.12**, with Japanese record and scheduling changes. This documentation update is not a new application release or a full backend revalidation.

| Component | Responsibility | Data or boundary |
| --- | --- | --- |
| React / TypeScript / Vite | Care-team and patient views; PDF comparison with locally served PDF.js assets | Shared records across English, Japanese and Arabic. The role selector chooses a demo persona. |
| FastAPI on Cloud Run | Session scoping, role/action and revision checks, rules, decisions and closure | Application hosted in Tokyo (`asia-northeast1`). Browser state cannot authorize closure. |
| Firestore | Case/workspace state, evidence references, decision history, extraction metadata and resource records | Case and workspace revisions detect conflicting changes. Runtime access uses a service account. |
| Cloud Storage | Original PDF bytes | Create-only uploads, pinned object generations and hash checks. Originals are retrieved through the scoped API. |
| Vertex AI / Gemini, optional | Source quotations and proposed review items | Documented model: `gemini-3.1-flash-lite`; global endpoint. No direct workflow, database or closure access. |

Solid connections show the normal application path; dashed connections show explicitly requested AI calls. Tokyo hosting and global model routing are separate settings. UAE-only data residency is not claimed. SQL and the Firestore emulator are test/development backends, not additional databases in this deployment.

## From a PDF to a decision

[![Evidence lifecycle: original report, later completion evidence, human closure and correction-driven review](../assets/evidence-lifecycle.svg)](../assets/evidence-lifecycle.svg)

1. **Import and extract.** Check the case/session and expected revision. A bounded `pypdf` worker extracts page text. Store an accepted PDF with its original hash; record page hashes, joined-text hash and extractor version separately. Import alone does not register case evidence.
2. **Compare and register.** A reviewer compares original and extracted text and confirms the current hashes. Arabic text also requires an order check. Registration links the evidence to its original; it does not establish clinical truth.
3. **Choose the relationship.** Add a later event as new evidence. A correction instead names the active same-case report it supersedes. Preserve earlier documents in both cases.
4. **Review and act.** Rules identify source wording; optional AI adds validated, source-linked candidates. A clinician persona records the decision, reason and active-source references. Adopting an item requires an open next action and does not resolve it.
5. **Confirm and close.** Record procedure evidence, result/plan review, explanation and action completion. The API requires a current review and all applicable conditions before accepting closure.
6. **Reconsider changes.** Adding clinical evidence, including a correction, clears procedure, result-review and plan-communication confirmations. A closed case becomes `review_required`. Decisions bound to an older source set need renewed review; previous decisions remain in history.

CL-001 preserves three different facts: a visit without the procedure, a later report of completion, and a correction of that later report. The correction must not be attached to the earlier truthful report.

## Records and relationships

These are logical application records, not a claim that each row is a separate database table.

| Record | Main fields and links | Purpose |
| --- | --- | --- |
| Workspace | Expiry, workspace revision, four fictional cases | Separate browser-session copies; expiry is distinct from deletion. |
| Case | Patient reference, revision, current/pending owner, pathway, status, next action | Preserve responsibility and unfinished work. |
| PDF extraction | Original hash/generation, page text and hashes, extractor/version | Check originals and extracted text independently. |
| Evidence | ID, text hash, version, `supersedes`, PDF reference, comparison record | Change active sources without overwriting originals. |
| Review item and decision | Evidence ID, quote, source hashes, disposition, reason, actor, revision | Do not silently reuse a decision after supporting sources change. |
| Confirmation and closure | Procedure source, reconciliation reason, result review, explanation, pathway/revision | Distinguish completion from a visit, booking or alternative disposition. |
| History | Action, time, demo role, revision, previous-event hash | Trace earlier actions; not external tamper-proof certification. |

PDF quotations can carry page numbers and character offsets. A hash checks byte/text consistency; it does not authenticate a report issuer or prove a medical finding.

## AI input, output and authority

| Stage | Implemented behaviour |
| --- | --- |
| Input | Active evidence IDs, titles, text, versions and timestamps, with the requested explanation language. A still-current human reconciliation can be included. This text-analysis path does not send original PDF bytes. |
| Output | Structured findings with an evidence ID, quotation and message. The server validates schema, quotation membership, and context/language requirements. |
| Human decision | `adopted`, `resolved` or `not_applicable`, with reasons and active-source references. Adoption does not complete the action. |
| Authority | The model cannot write case state, decide diagnosis/treatment/urgency, or approve closure. The deterministic workflow enforces requirements. |
| Failure | Invalid or incomplete output is an error, not an empty successful review. Zero findings does not establish completeness. |

The core walkthrough works with rules alone. Neither source matching nor AI proposals are clinically validated classifiers.

## Workflow rules

The six visible checks cover patient acknowledgement, clinician consultation, procedure evidence, result review, plan communication and accepted referral. The API also checks owner, pending handoff, supported pathway, hold status, open next action and unresolved source/AI items. An older revision's review cannot authorize closure.

| Event | Required behaviour |
| --- | --- |
| Handoff request | Keep the current owner until the pending recipient accepts. |
| Hold | Keep a reason, owner, next action and scheduled review; block normal completion. |
| Decline or alternative plan | Use a distinct, evidence-backed disposition; do not mark the original procedure performed. |
| Patient requests clarification | Retain the request and require renewed plan communication. Self-reported understanding does not authorize closure. |
| Stale or concurrent update | Reject with a revision conflict; reload before deciding against the new state. |

## Language and time

In the observed v0.4.12 interface, Japanese schedules use **Asia/Tokyo (UTC+9)**; English and Arabic use **Asia/Dubai (UTC+4)**. Schedules are stored as timezone-aware UTC values. Localization does not rewrite uploaded originals or a user's original-language message. Arabic uses right-to-left layout; specialist-language validation is outstanding.

See the [hands-on guide](demo-guide.md) for the walkthrough and [controls and operations](security-and-operations.md) for access, retention and deployment limits.
