# Scope and limitations

[Home](../README.md) · [Hands-on guide](demo-guide.md)

## Implemented demonstration

The prototype demonstrates a fictional screening follow-up pathway, original PDF comparison and registration, source-linked review items, named next actions, handoffs, human confirmations, conditional closure, correction-driven review and history retention. It provides care-team and patient-facing views.

The public application is in synthetic-demo mode. Use only fictional data and the supplied fixtures. No real patient or provider is contacted. Demo role selection does not verify identity or clinical qualifications.

## Boundaries

- The application does not determine diagnosis, urgency, treatment or whether a test is clinically necessary.
- Source wording and checklist completion do not prove that a procedure occurred or that a report is clinically adequate.
- AI proposals require inspection and human decisions. Zero proposed items does not establish completeness.
- Institution-specific pathways, clinical deadlines and escalation arrangements require local definition.
- EHR/FHIR, OCR and live provider messaging are not integrated in the demonstrated scope.
- Session expiry and public resource limits can stop an exercise. This demonstration does not establish production availability, load capacity or an operational service-level commitment.
- Tokyo hosting and global model routing do not establish UAE-only data residency.

## Future pilot

A real deployment would need institution-specific review, verified identities and access, agreed data handling, pathway and language review, and evaluation of patient and operational outcomes. Clinical/expert reviews and real-user evaluation are outside the present construction scope and have not been completed as validation evidence.

The intended benefit is to make unfinished follow-up visible and actionable. Improvements in completion rates, clinical outcomes, time to action or patient understanding remain subjects for future evaluation.
