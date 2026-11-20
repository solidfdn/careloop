# Access, data controls and operation

[Home](../README.md) · [日本語](security-and-operations.ja.md) · [Architecture](architecture.md) · [Validation](validation.md)

The public workspace contains records created for the demo. The controls and limits below describe v0.5.2 RC32. Historical deployment exercises and cost estimates are dated separately.

## Access boundaries

| Boundary | Implemented control | Limit |
| --- | --- | --- |
| Browser session | Random session token in an HttpOnly, SameSite=Strict cookie; Secure on HTTPS. Server stores its hash. | Possession of the session is not verified personal identity. Tabs in one profile share it. |
| Workspace | A new reviewer session starts with 300 demonstration patients. Case, document and resource requests use that session’s records. | The demo does not verify hospital membership or patient identity. |
| Operation | Server checks the selected persona against allowed actions. | Persona selection does not verify clinician qualifications or facility membership. |
| Update | Expected case/workspace revisions and atomic compare-and-set writes | A stale operation is rejected; the user must reload and reconsider. |
| Browser request | Exact-origin checks on mutations and bounded request sizes | These controls do not replace production authentication or a penetration test. |
| Cloud resources | Server-side service identity; storage/model credentials are not supplied to the browser | Production IAM, tenant access and regional policy need institution-specific review. |

### Demonstrated role permissions

| Operation | Coordinator | Clinician | Patient |
| --- | :---: | :---: | :---: |
| Ask the record in natural language | Yes | Yes | No |
| Import/register evidence, run review, record/complete next action | Yes | Yes | No |
| Request/accept/reject a demo handoff | Yes | Yes | No |
| Record consultation, procedure evidence and result review | No | Yes | No |
| Decide review candidates; record closure/disposition | No | Yes | No |
| Record plan communication | Yes | Yes | No |
| Acknowledge guidance or submit an understanding/clarification response | No | No | Yes |
| Record support preferences or case-linked messages | Yes | Yes | Yes |

These are action permissions for a simulation. Switching roles is possible within a reviewer workspace; this is not a patient-access security model.

## Data and retention

- **Originals and extraction:** preserve accepted PDF bytes separately from extracted page text and registered evidence. Original retrieval checks the pinned generation and original hash. Registration requires explicit comparison confirmation.
- **Corrections:** retain superseded reports and earlier closure/history. New evidence clears dependent confirmations. A source-set change makes earlier candidate decisions stale.
- **History:** actions include the demo identity status and a chained hash. This detects consistency failures; it is not externally anchored, tamper-proof clinical audit storage.
- **Expiry:** a reviewer workspace lasts 24 hours. Expiry denies further session access; it does **not** automatically delete its records or originals. This demo has no automatic erasure promise. Retention, deletion and subject-access processes must be agreed before any real deployment.
- **AI:** a natural-language question sends bounded, scoped record blocks, computed totals, relevant history and original-source passages to the configured Gemini service. Optional evidence review sends the current evidence and relevant reconciliation. The documented deployment uses Vertex AI's global endpoint. Rules-only review avoids that model request. Only synthetic data is allowed.
- **Answers:** the model selects supplied identifiers; the server validates selections and binds displayed facts and quotations to the records. Answers include source references, checked time and coverage limits. Asking is read-only for case data, while execution and resource-use logs are stored. The patient demo role is denied staff-worklist questions.
- **Communication:** messages, support preferences and simulated handoffs are recorded inside CareLoop. No SMS, email, booking or provider message is sent.

## Dependencies and capacity

The documented public service uses Cloud Run, Firestore, Cloud Storage and optional Vertex AI. The frontend is React/TypeScript; the service is FastAPI/Python; PDF text extraction uses pypdf and preview uses PDF.js. Original storage must be available for PDF import; Vertex access is needed for natural-language questions and Gemini evidence review. No OCR is integrated.

The retained deployment setting, also referenced by the current admission control, is **1 CPU / 512 MiB, minimum 1 and maximum 2 Cloud Run instances**, with request-based billing and an HTTP health startup probe. Shared admission limits allow one heavy PDF/AI operation at a time. Scaling the container alone does not remove that shared limit.

| Configured limit in v0.5.2 RC32 | Per workspace / request | Lifetime service setting |
| --- | --- | --- |
| Workspace | 24 hours, 100 successful updates | 1,000 created workspaces |
| PDF import | 3 imports / 20 MB total; each PDF ≤10 MB and ≤20 pages | 500 imports / 2.5 GB |
| AI questions and review, sharing one budget | 8 attempts / 200 KB input total; one input ≤32,000 bytes | 1,200 calls / 25 MB input |
| Original PDF retrieval | 30 requests / 100 MB | 1,500 requests / 12 GB |

These are configured ceilings, not the current remaining allowance, concurrent-user capacity or a service-level commitment. Failed work and automatic recovery attempts may consume a reservation. Question answering permits at most two attempts within a 70-second server deadline. This bounds retry work; it does not guarantee successful recovery. Expiry/restarts do not reset lifetime counters. Do not create repeated workspaces to work around a limit.

### Failure and recovery

| Observation | Expected handling |
| --- | --- |
| Revision conflict | Reload and review the current case before retrying an action. |
| Unreadable, encrypted or oversized PDF | Reject import; do not silently use OCR or register unverified text. |
| Failed PDF storage or integrity check | Report failure; do not present successful registration or an unchecked original. |
| Question timeout, incomplete selection or selected recoverable provider error | Attempt bounded recovery when time and resource budget permit; otherwise report failure and preserve case data. |
| Records change during an answer | Reject the stale answer and ask again against current records. |
| Invalid evidence-review response | Report failure; do not turn invalid output into a successful empty review. |
| Resource limit or expired session | Preserve records; stop the affected operation. Follow the displayed session guidance or contact SOLIFAN. |

A prior v0.4.10 recovery exercise restored application records and original object generations into an isolated environment. It was **not** a fresh-cloud-project IAM/billing/DNS failover. No uptime or disaster-recovery target has been validated for this public demo.

### Cost assumption

The retained **2 November 2026 planning estimate** was **USD 20–35 for one month of low-volume review and 1,000 additional AI calls**, excluding tax and credits. It assumed the small deployment above and allowances for storage/builds. This is a historical planning estimate, not a current price quote, invoice, guaranteed spending cap or production cost per patient. Relevant cost drivers are active/idle compute, database traffic and history growth, originals/egress, builds/logs and model tokens. Provider prices and measured usage must be checked before a new operating commitment. Application call/reservation limits do not cap the total cloud bill.

## What a real pilot still needs

Verified identities and facility access, a locally approved pathway and escalation policy, agreed hosting/model routing and retention, specialist-language review, external-system integration where needed, security assessment and patient/operational evaluation are future pilot work. The [review map](reviewer-map.md) identifies what is demonstrated and what remains an untested hypothesis.

This documentation repository cannot deploy the service: application source, dependency locks, cloud configuration and credentials are not included. It provides a hosted walkthrough, architecture, versioned evidence and fictional fixtures for review.
