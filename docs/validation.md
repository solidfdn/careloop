# Validation and evidence

[Home](../README.md) · [Machine-readable summary](../evidence/technical-verification.json)

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
