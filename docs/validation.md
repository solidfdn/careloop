# Validation and evidence

[Home](../README.md) · [日本語](validation.ja.md) · [Machine-readable summary](../evidence/technical-verification.json)

The **hosted v0.4.12 workflow passed on 3 November 2026** using the published PDFs and rules-only review. The retained **v0.4.11 backend suite passed 1,011 tests**. These are different checks, with their versions and scope recorded below.

| Evidence | Version / date | Recorded result | What it supports |
| --- | --- | --- | --- |
| [Hosted PDF workflow through the public API](../evidence/hosted-workflow-v0.4.12.json) | v0.4.12; 3 November 2026 | Passed in a separate synthetic workspace; no model calls | Incomplete closure rejection, PDF extraction/registration separation, original-byte preservation, later evidence, human confirmation and closure, then correction and renewed review. |
| Public availability and Japanese scheduling label | v0.4.12; 3 November 2026 | Health and public entry responses received; Japanese form displays Japan time | Deployment identity, reachable EN/JA entry paths and the observed scheduling interface. |
| Backend regression suite | v0.4.11; 2 November 2026 | 1,011 tests; 0 failures, errors or skips | Technical behaviour across SQL and the official Firestore emulator. |
| Guided PDF workflow through the API | v0.4.11; 2 November 2026 | Passed | Incomplete closure rejection, later evidence registration, human confirmation and closure, correction/review, and original preservation. |
| Browser correction walkthrough | v0.4.11; 2 November 2026 | Passed through case revision 13 | Correction registration, invalidation of three dependent confirmations, disabled closure and retained earlier records in the observed workspace. |

## Current hosted workflow

The v0.4.12 check used one new workspace and the two unchanged fixture PDFs. It verified that a later event did not supersede the initial report, required a reconciliation reason, completed the next action, and accepted closure after the human confirmations and current evidence review. The correction then superseded the later completion report, invalidated three dependent confirmations, preserved the earlier report and closure, and blocked incomplete closure again.

| Checkpoint | Case revision | Recorded state |
| --- | ---: | --- |
| Original incomplete source | 2 | Open; closure unavailable. |
| Current confirmations recorded | 9 | Open; ready for a human closure decision. |
| Human closure recorded | 10 | Closed. |
| Correction reviewed | 12 | Review required; procedure, result-review and plan-communication confirmations invalidated; closure unavailable. |

No review candidates were returned in this rules-only run. The source checks and human-confirmation requirements still controlled closure. This was a **public API walkthrough**, not a full v0.4.12 backend regression run or a complete browser replay. [The run record](../evidence/hosted-workflow-v0.4.12.json) includes the timestamps, checks, state checkpoints and fixture hashes.

## What the 1,011 checks cover

The retained v0.4.11 JUnit report contains the following results. All groups have zero failures, errors and skips. [Module-level counts and the source-report hash](../evidence/backend-regression-v0.4.11.json) allow the total to be inspected.

| Test family | Checks |
| --- | ---: |
| Workflow and patient interaction | 137 |
| Source wording, context and completion boundaries | 638 |
| PDF import and original retrieval | 97 |
| AI control and transport | 38 |
| Persistence and import | 68 |
| Session isolation and capacity | 33 |
| **Total** | **1,011** |

The counts were checked against the retained report. Some persistence/configuration tests cover development or legacy paths rather than the deployed Firestore service. A test count is not a patient count or an accuracy percentage.

## Reproduction and limits

The [hands-on guide](demo-guide.md) and [fixture PDFs](../demo-data/README.md) let reviewers try the hosted workflow. The application source and complete test harness are not published here, so this repository alone cannot reproduce the backend suite or deploy a new instance.

These are developer technical checks on synthetic workflows. Historical AI evaluations used repeated development cases, not blinded or independent clinical evaluation. Clinical outcomes, staff-time savings, patient understanding and real-user usability have not been measured; clinical and specialist-language validation remain outstanding. The [implementation map](reviewer-map.md) separates the demonstrated behaviour from those future evaluations.
