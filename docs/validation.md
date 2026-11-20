# Validation and evidence

[Home](../README.md) · [日本語](validation.ja.md) · [RC4–RC9 verification record](../evidence/careloop-v0.5.2-verification.json)

The v0.5.2 RC32 walkthrough follows two patients, one waiting for test results (CL-015) and one who missed an appointment (CL-025). The checks below identify the version and workspace used. Counts from earlier suites have overlapping coverage and are reported separately.

## RC32 walkthrough · 20 November 2026

- **Result delivery and missed appointment.** The reviewer entry links to the corresponding work queues. For CL-015, the reviewer can open the dated evidence of the undelivered result and record the responsible team and next action. For CL-025, the reviewer can inspect the attendance record, record a call to arrange a new booking, and answer the patient’s question in the app.
- **Worklist count.** After the patient in CL-025 requested clarification, the Japanese workspace returned 30 patients awaiting further explanation out of 300. The answer linked to 30 follow-up records. Their case identifiers matched the list, including CL-025. This is the recorded state after that action. Another workspace can show a different count.

## Earlier versioned results

| Evidence | Tested version / date | Recorded result | What it establishes within the exercised scope |
| --- | --- | --- | --- |
| Full backend regression | v0.5.2 RC4; 5 November 2026 | 1,247 tests; 0 failures, errors or skips | Workflow, evidence, patient response, questions, isolation and persistence checks. The run included 418 tests requiring the official Firestore emulator, using no production database. |
| Real Gemini questions and source review | RC4; 5 November | 46 inputs passed automated checks and a separate review of their recorded answers | Requested facts, exact source passages, citations, missing information, conflicting sources and the distinction between current confirmations and historical decisions. The set comprised 36 repeated development inputs and 10 additional inputs defined before execution. |
| Hosted API checks | RC4; 5 November | 21 checks passed over 54 requests; no AI calls | Access and revision boundaries, history pagination, original PDF bytes, extraction/registration separation and record preservation during reads. |
| Answer-function regression | v0.5.2 RC6; 7 November | 144 tests; 0 failures, errors or skips | Concise answers and the existing selection, citation, detail, refusal and recovery boundaries. |
| Real Gemini questions for the CL-006 walkthrough | RC6; 7 November | 7 inputs passed: English 3, Japanese 2, Arabic 2 | CL-006 reason questions, paraphrases and a combined reason/owner/next-action question. Answers contained 5–6 references; the case record hash was unchanged after the run. |
| Interface and publication checks | v0.5.2 RC9; 7 November | Build, copy checks, question-UI checks and EN/JA/AR file-picker checks passed | Language-appropriate file selection, hidden patient upload, empty-state behaviour and matching published asset bytes. |

The [machine-readable summary](../evidence/careloop-v0.5.2-verification.json) contains test-module counts, source-report hashes and the boundaries of each run. It is a sanitized summary of retained developer records, not an independently certified test report.

During the RC9 publication check, unauthenticated requests to the health endpoint, reviewer entry and English and Japanese workspaces returned HTTP 200. This check made no AI calls or record changes.

## What was checked for natural-language questions

Gemini interprets a free-text question and selects relevant supplied record blocks or original passages. The service validates the selection and binds displayed facts, references and checked time to the records. It does not accept model-generated dates, counts or action results as new case facts.

The recorded checks cover source attribution, absent requested details, active versus superseded sources, current responsibility versus a proposed recipient, and requests that would change records. Asking a question does not approve closure or perform a workflow action. A missing confirmation is not, by itself, proof that care did not occur.

In the RC6 CL-006 walkthrough, a correction states that only consultation occurred, three confirmations need renewed review, and the earlier closure decision remains in history. A combined question also identifies Follow-up team A and states that the next action and its due date are not recorded.

## How the evidence relates to RC9

The 65 backend Python files in the retained RC6 source snapshot match the retained RC9 snapshot byte for byte. The recorded hashes of the question service and question UI also match RC9. Subsequent changes concerned the sidebar logos and file-picker interface. RC9's build, language and question-UI checks passed after those changes.

This continuity supports applying the RC6 answer evidence to the unchanged components. It does not turn either earlier suite into a new full RC9 test run. During development, a separate provider rate-limit response was observed and a later retry recovered; the seven successful inputs are not an uptime or all-request success-rate claim.

## Retained earlier evidence

Earlier results remain available for traceability:

| Record | Version / date | Scope |
| --- | --- | --- |
| [Hosted PDF workflow](../evidence/hosted-workflow-v0.4.12.json) | v0.4.12; 3 November 2026 | A separate synthetic CL-001 workspace exercised PDF import, later completion evidence, human closure and a correction that reopened review. Rules-only execution, no model calls. |
| [Backend module counts](../evidence/backend-regression-v0.4.11.json) | v0.4.11; 2 November | 1,011 tests, with zero failures, errors and skips. Historical regression evidence. |
| [Earlier combined summary](../evidence/technical-verification-20261103.json) | Historical versions recorded in the file | Earlier API and browser checks. This is not the current release summary. |

The [hands-on guide](demo-guide.md) starts with CL-015 and CL-025. The CL-006 correction scenario and CL-001 PDF exercise remain available separately.

## Reproduction and limits

Reviewers can try the hosted application using the [guide](demo-guide.md). The [PDF fixtures](../demo-data/README.md) support the separate CL-001 import exercise. Application source and the complete test harness are not published, so this repository alone cannot reproduce the backend suite or deploy a new instance.

These are developer technical checks using synthetic data. The 46-input and seven-input sets are bounded development checks, not a blinded clinical benchmark or a general accuracy percentage. Clinical outcomes, staff-time savings, patient understanding and real-user usability have not been measured. Clinical and specialist-language validation remain outstanding. The [review map](reviewer-map.md) distinguishes the demonstrated behaviour from future pilot measures.
