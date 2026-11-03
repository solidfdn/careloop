# Access, data controls and operation

[Home](../README.md) · [日本語](security-and-operations.ja.md) · [Architecture](architecture.md) · [Validation](validation.md)

This public service is a **synthetic demonstration**. The controls below describe the retained v0.4.11 implementation and documented deployment, not a certification or an independent security assessment. The v0.4.12 interface has a separately scoped availability/localization check.

## Access boundaries

| Boundary | Implemented control | Limit |
| --- | --- | --- |
| Browser session | Random session token in an HttpOnly, SameSite=Strict cookie; Secure on HTTPS. Server stores its hash. | Possession of the session is not verified personal identity. Tabs in one profile share it. |
| Workspace | A copy of four fictional cases; case/document/resource lookups are scoped to the session. | The public demo is not a hospital tenant or patient identity system. |
| Operation | Server checks the selected persona against allowed actions. | Persona selection does not verify clinician qualifications or facility membership. |
| Update | Expected case/workspace revisions and atomic compare-and-set writes | A stale operation is rejected; the user must reload and reconsider. |
| Browser request | Exact-origin checks on mutations and bounded request sizes | These controls do not replace production authentication or a penetration test. |
| Cloud resources | Server-side service identity; storage/model credentials are not supplied to the browser | Production IAM, tenant access and regional policy need institution-specific review. |

### Demonstrated role permissions

| Operation | Coordinator | Clinician | Patient |
| --- | :---: | :---: | :---: |
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
- **AI:** an explicit Gemini action sends current evidence text and relevant current reconciliation to Vertex AI's global endpoint. Rules-only review avoids that model request. Do not put real patient data in either path.
- **Communication:** messages, support preferences and simulated handoffs are recorded inside CareLoop. No SMS, email, booking or provider message is sent.

## Dependencies and capacity

The documented public service uses Cloud Run, Firestore, Cloud Storage and optional Vertex AI. The frontend is React/TypeScript; the service is FastAPI/Python; PDF text extraction uses pypdf and preview uses PDF.js. Original storage must be available for PDF import; Vertex access is needed only for Gemini review. No OCR is integrated.

The retained deployment setting is **1 CPU / 512 MiB, minimum 1 and maximum 2 Cloud Run instances**, with request-based billing and an HTTP health startup probe. Shared admission limits allow one heavy PDF/AI operation at a time. Scaling the container alone does not remove that shared limit.

| Limit in the v0.4.11 snapshot | Per workspace / request | Lifetime service setting |
| --- | --- | --- |
| Workspace | 24 hours; 100 successful updates | 250 created workspaces |
| PDF import | 3 imports / 20 MB total; each PDF ≤10 MB and ≤20 pages | 500 imports / 2.5 GB |
| AI review | 8 calls / 200 KB input total; one input ≤32,000 bytes | 1,200 calls / 25 MB input |
| Original PDF retrieval | 30 requests / 100 MB | 1,500 requests / 12 GB |

These are configured ceilings, not the current remaining allowance, concurrent-user capacity or a service-level commitment. Failed work may consume a reservation. Expiry/restarts do not reset lifetime counters. Do not create repeated workspaces to work around a limit.

### Failure and recovery

| Observation | Expected handling |
| --- | --- |
| Revision conflict | Reload and review the current case before retrying an action. |
| Unreadable, encrypted or oversized PDF | Reject import; do not silently use OCR or register unverified text. |
| Failed PDF storage or integrity check | Report failure; do not present successful registration or an unchecked original. |
| Model timeout/invalid response | Report the failure and retain existing case records; do not claim successful AI review. |
| Resource limit or expired session | Preserve records; stop the affected operation. Follow the displayed session guidance or contact SOLIFAN. |

A prior v0.4.10 recovery exercise restored application records and original object generations into an isolated environment. It was **not** a fresh-cloud-project IAM/billing/DNS failover. No uptime or disaster-recovery target has been validated for this public demo.

### Cost assumption

The retained **2 November 2026 planning estimate** was **USD 20–35 for one month of low-volume review and 1,000 additional AI calls**, excluding tax and credits. It assumed the small deployment above and allowances for storage/builds. This is a historical planning estimate, not a current price quote, invoice, guaranteed spending cap or production cost per patient. Relevant cost drivers are active/idle compute, database traffic and history growth, originals/egress, builds/logs and model tokens. Provider prices and measured usage must be checked before a new operating commitment. Application call/reservation limits do not cap the total cloud bill.

## What a real pilot still needs

Verified identities and facility access, a locally approved pathway and escalation policy, agreed hosting/model routing and retention, specialist-language review, external-system integration where needed, security assessment and patient/operational evaluation are future pilot work. The [review map](reviewer-map.md) identifies what is demonstrated and what remains an untested hypothesis.

This documentation repository cannot deploy the service: application source, dependency locks, cloud configuration and credentials are not included. It provides a hosted walkthrough, architecture, versioned evidence and fictional fixtures for review.
