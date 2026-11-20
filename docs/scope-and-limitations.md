# Scope and limitations

[Home](../README.md) · [日本語](scope-and-limitations.ja.md) · [Hands-on guide](demo-guide.md)

## Implemented demonstration

CareLoop v0.5.2 RC32 opens a list of 300 patients created for the demo. The care team can find an overdue result or a missed appointment, inspect the record, assign a next action and reply to a patient. The patient can read the reply and ask for clarification. Additional examples cover PDF registration, referral acceptance, human confirmation and reopening follow-up after a corrected report.

The public application is in synthetic-demo mode. Use only fictional data and the supplied fixtures. No real patient or provider is contacted. Demo role selection does not verify identity or clinical qualifications.

## Boundaries

- The application does not determine diagnosis, urgency, treatment or whether a test is clinically necessary.
- Source wording and checklist completion do not prove that a procedure occurred or that a report is clinically adequate.
- Gemini interprets questions and selects relevant supplied records or passages. The server binds answers to recorded facts and source references, shows checked time, and reports missing information, conflicts and scope limits. Answers can still be incomplete or select the wrong relevant material; inspect the cited record.
- Questions do not update case records or approve closure. The patient demo role cannot query staff worklists.
- AI review proposals require inspection and human decisions. Zero proposed items does not establish completeness.
- Worklist questions can report distinct patients and open the matching records. The priority bands count follow-up records. Queues can overlap, and the results change as reviewers update cases. Production capacity has not been measured.
- Institution-specific pathways, clinical deadlines and escalation arrangements require local definition.
- EHR/FHIR, OCR and live provider messaging are not integrated in the demonstrated scope.
- Session expiry and public resource limits can stop an exercise. This demonstration does not establish production availability, load capacity or an operational service-level commitment.
- Tokyo hosting and global model routing do not establish UAE-only data residency.

## Future pilot

A real deployment would need institution-specific review, verified identities and access, agreed data handling, pathway and language review, and evaluation of patient and operational outcomes. Clinical/expert reviews and real-user evaluation are outside the present construction scope and have not been completed as validation evidence. Patient responses are recorded self-reports; the existence of that feature is not evidence of improved understanding.

The intended benefit is to make unfinished follow-up visible and actionable. Improvements in completion rates, clinical outcomes, time to action or patient understanding remain subjects for future evaluation.
