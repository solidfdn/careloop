# CareLoop

**Helping screening results lead to the necessary tests and care.**

CareLoop helps care teams keep follow-up visible: who owns the next action, what the source report actually says, and what still needs attention. When a report is corrected, the case returns for review while the earlier evidence and decisions remain available.

[日本語](README.ja.md) · [Open the demo](https://careloop-demo-864232222461.asia-northeast1.run.app/entry/) · [Hands-on guide](docs/demo-guide.md) · [Architecture](docs/architecture.md) · [Review map](docs/reviewer-map.md)

*A working prototype with fictional data. Explore the case, try the workflow, then inspect its architecture and evidence.*

## The gap CareLoop addresses

A completed specialist visit can still leave the intended procedure unfinished. A status field alone can hide the gap between an abnormal screening result and the tests or care that need to follow.

CareLoop brings the source evidence, responsible team, next action and human confirmations into the same pathway. The prototype uses a fictional follow-up case after a positive faecal immunochemical test (FIT).

## Try it

1. Open the application in [English](https://careloop-demo-864232222461.asia-northeast1.run.app/?lang=en) or [Japanese](https://careloop-demo-864232222461.asia-northeast1.run.app/?lang=ja). Arabic is also available from the language selector.
2. Select **CL-001 / Alex Morgan / SYN-001** and follow the [hands-on guide](docs/demo-guide.md).
3. Use the two supplied [fictional PDF fixtures](demo-data/README.md) to compare a later completion report with its correction.

Use a separate browser profile or private window for an independent workspace. Tabs in the same profile share a session. The interface is v0.4.12; Japanese scheduling uses Japan time, while English and Arabic use Abu Dhabi time. A new workspace begins at the start of the pathway.

[![CareLoop v0.4.12: initial CL-001 case, accountable owner and missing confirmations](assets/careloop-case.en.png)](assets/careloop-case.en.png)

*Current application, CL-001 initial state (v0.4.12, 3 November 2026). The case detail is shown at native resolution; click to enlarge. Three required confirmations are missing, so closure is unavailable.*

## What the demonstration shows

| Situation | CareLoop behaviour |
| --- | --- |
| The visit is complete, but the source says the procedure was not performed. | The source statements remain visible and closure stays unavailable while required confirmations are missing. |
| A team requests a handoff. | The current team remains accountable until the receiving team accepts. |
| A later report documents completion. | It is registered as new evidence. People record the supporting source, resolution of earlier findings, action completion, result review and explanation. |
| The later report is corrected. | The case returns to review. Dependent confirmations are invalidated; earlier reports and the previous closure remain available. |

## System at a glance

[![CareLoop system architecture](assets/architecture.svg)](docs/architecture.md)

The service connects original evidence, accountable teams and human decisions. Optional AI proposes review items; the API enforces closure conditions. See the [evidence lifecycle and data relationships](docs/architecture.md#from-a-pdf-to-a-decision), [access and operating controls](docs/security-and-operations.md), and [implementation-to-evidence map](docs/reviewer-map.md).

## People make the decisions

Deterministic rules point back to relevant source wording. Optional Gemini support proposes source-linked review items. People inspect the evidence, decide how to handle the items and record their reasons. AI does not authorize closure or determine diagnosis, urgency or treatment.

## Technical reference

| Document | Purpose |
| --- | --- |
| [Hands-on guide](docs/demo-guide.md) | Reproduce the source, closure and correction flow. |
| [Architecture and evidence lifecycle](docs/architecture.md) | Inspect both diagrams, components, data relationships and AI input/output boundaries. |
| [Access, data controls and operation](docs/security-and-operations.md) | See persona permissions, retention, dependencies, capacity, failure handling and cost assumptions. |
| [Implementation and review map](docs/reviewer-map.md) | Connect features to evidence and assessment topics; distinguish future pilot hypotheses. |
| [Validation](docs/validation.md) | See versioned technical checks and what they establish. |
| [Scope and limitations](docs/scope-and-limitations.md) | Understand the prototype's operating and evaluation limits. |
| [Fixture details](demo-data/README.md) | Identify the supplied PDFs and verify their bytes. |
| [Rights and attribution](NOTICE.md) | Understand ownership and the publication scope. |

This repository publishes product documentation, selected illustrations and fictional fixtures. The application implementation is not included. Technical results are developer checks on synthetic workflows; clinical outcomes, staff-time savings and independent user evaluation have not been measured.

Prepared by [SOLIFAN](https://www.solid-fdn.co.jp/) for Future Health Digital Innovation Challenge, **Challenge 05: Closing the Screening-to-Care Loop**.
