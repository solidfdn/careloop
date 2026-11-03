# Validation and evidence

[Home](../README.md) · [日本語](validation.ja.md) · [Machine-readable summary](../evidence/technical-verification.json)

Technical checks are reported against the version actually tested. The current public interface is not presented as a new run of an older test suite.

| Evidence | Version / date | Recorded result | What it supports |
| --- | --- | --- | --- |
| Backend regression suite | v0.4.11; 2 November 2026 | 1,011 tests; 0 failures, errors or skips | Technical behaviour across SQL and the official Firestore emulator. |
| Guided PDF workflow through the API | v0.4.11; 2 November 2026 | Passed | Incomplete closure rejection, later evidence registration, human confirmation and closure, correction/review, and original preservation. |
| Browser correction walkthrough | v0.4.11; 2 November 2026 | Passed through case revision 13 | Correction registration, invalidation of three dependent confirmations, disabled closure and retained earlier records in the observed workspace. |
| Public availability and Japanese scheduling label | v0.4.12; 3 November 2026 | Health and public entry responses received; Japanese form displays Japan time | Current deployment identity, reachable EN/JA entry paths and the observed scheduling interface. This is not a full rerun of v0.4.12. |

The regression count was checked against the retained JUnit report, not inferred from the illustrations. Its SHA-256 is included in the summary. The two fixture hashes are also recorded so the demonstration inputs can be identified independently.

The API walkthrough and browser walkthrough are distinct checks. Historical AI evaluations were inspected during development; repeated runs are development regressions, not blinded or independent evaluations. No clinical accuracy or effectiveness percentage is claimed.

Clinical outcomes, staff-time savings, patient understanding and real-user usability have not been measured. Clinical and specialist-language validation are not established. These limitations do not change what the technical workflow checks recorded.

## What the 1,011 checks cover

The table below is a fresh aggregation of the retained v0.4.11 JUnit result, not a rerun. All groups have zero failures, errors and skips. [Module-level counts and the source-report hash](../evidence/backend-regression-v0.4.11.json) allow the published total to be inspected.

| Test family | Checks |
| --- | ---: |
| Workflow and patient interaction | 137 |
| Source wording, context and completion boundaries | 638 |
| PDF import and original retrieval | 97 |
| AI control and transport | 38 |
| Persistence and import | 68 |
| Session isolation and capacity | 33 |
| **Total** | **1,011** |

A test count is not a patient count, an accuracy percentage or proof of clinical safety. Some persistence/configuration tests cover development or legacy paths rather than the deployed Firestore service.

## What a reviewer can reproduce

The [hands-on guide](demo-guide.md) and [unchanged fixture PDFs](../demo-data/README.md) reproduce the hosted workflow: incomplete evidence → later event → current human decisions → closure → correction and renewed review. The public repository does not contain the application source or complete test harness, so it cannot reproduce the backend suite or deploy a new instance on its own.

The [implementation map](reviewer-map.md) ties the claims to these checks and distinguishes future patient/operational evaluation. Neither this documentation update nor the availability check replaces a full v0.4.12 regression run.
