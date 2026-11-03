# CareLoop hands-on guide

[Home](../README.md) · [日本語](demo-guide.ja.md)

Follow the fictional **CL-001 / Alex Morgan / SYN-001** pathway from an incomplete procedure report to a human closure decision, then inspect what a correction changes. Use synthetic data only.

## Before you start

- Open the [English application](https://careloop-demo-864232222461.asia-northeast1.run.app/?lang=en).
- For a separate workspace, use another browser profile or private window. Tabs within the same profile share the session. A workspace lasts 24 hours; if it expires, use the application's new-workspace control. If a demo resource limit is reached, stop and contact SOLIFAN instead of repeatedly creating sessions.
- Download the [later completion report](https://github.com/solidfdn/careloop/raw/refs/heads/main/demo-data/CareLoop_Demo_Completed_SYN001_v1.pdf) and [correction report](https://github.com/solidfdn/careloop/raw/refs/heads/main/demo-data/CareLoop_Demo_Correction_SYN001_v1.pdf). Keep both files unchanged. Their historical version labels identify the fixtures, not the current application; [fixture details](../demo-data/README.md) include checksums.
- Select **Clinician** under **Operating role**. These roles are demo personas, not verified clinical identities.
- English scheduling uses **Abu Dhabi time (UTC+4)**. Japanese scheduling uses **Japan time (UTC+9)**. Use a future demo date in the displayed time zone; the schedule is not a clinical deadline.

A new workspace starts with the original report. Follow the steps in order.

## 1. Inspect the original source

Select **CL-001**, open **Evidence**, and expand **Specialist visit report**. Read the source statement: consultation only; colonoscopy not performed; rebooking required.

Return to **Care pathway**. Keep **Rules baseline** selected under **Check method**, then click **Check evidence**. Inspect the source quotations and closure checklist. A completed visit does not establish completion of the procedure; closure remains unavailable while requirements are unmet.

## 2. Record the next action

Click **Record next action** and enter:

| Field | Synthetic example |
| --- | --- |
| Next-action owner | Screening coordination |
| Next action | Obtain and review the later procedure report for SYN-001. |
| Scheduled time | A future demo date and time, in the displayed zone. |

Click **Save record** and check the saved owner, action and schedule.

## 3. Add the later report as new evidence

In **Evidence**, select `CareLoop_Demo_Completed_SYN001_v1.pdf` under **PDF to import**, then click **Import PDF**. Expand the extracted page and use **Open original** to compare the patient reference and full statement with the original PDF.

Give **Evidence title** a recognizable name, such as `Later procedure completion report - SYN-001`. Keep **Earlier evidence being corrected** set to **Add as new evidence**. Check the comparison declaration and click **Register confirmed evidence**. Wait until registration completes.

This later report describes a subsequent event. Preserve the earlier report, which accurately recorded that the procedure had not yet been performed.

## 4. Record the human confirmations

Return to **Care pathway**.

1. **Confirm procedure**: choose the later report under **Active evidence supporting completion**. Explain how the later report resolves the earlier incomplete findings, check the verification declaration and save.
2. **Complete next action**: record that the requested report was obtained and reviewed, with the supporting reason, then save.
3. **Review result & plan**: record the synthetic result/plan review and save.
4. **Record explanation**: record the synthetic explanation and save.

Describe the exercise as a process demonstration. The fixture contains no real clinical findings, and no real patient has been contacted. Inspect all six checklist items; the seed case supplies the other demonstration confirmations.

## 5. Check the current evidence and close

Run **Check evidence** after changes. The verified v0.4.12 rules-only walkthrough produced zero review items. If **Review items and judgments** shows zero, no item judgment is needed; the six closure confirmations still apply.

If review items are listed:

1. Compare each quotation with its linked source, then click **Review and record judgment**.
2. Under **Disposition**, choose **Resolved** if the evidence establishes resolution, **Not applicable** if the item does not apply, or **Action required** if follow-up is needed. For **Action required**, first record an owner and an open next action; adopting an item does not resolve it or permit closure.
3. Select the relevant **Active evidence reviewed**, enter the **Reason and verification**, then click **Save judgment**. Base the decision on the current source documents.

When all required confirmations are current and current review items have been handled, click **Close pathway**. Enter the synthetic closure reason, check the declaration and save. The case becomes **Closed**, and its closure decision is retained.

Gemini is optional. If you choose **Gemini + rules (not clinically validated)**, inspect the **AI execution records** and review any proposed items against the original source. Candidate count may be zero. The principal walkthrough can use the deterministic rules without a model call.

## 6. Correct the later report

In **Evidence**, import `CareLoop_Demo_Correction_SYN001_v1.pdf`. Compare the original and extracted text. Its statement says that only the first stage was performed and required steps remain pending.

Enter a recognizable title. Under **Earlier evidence being corrected**, select the **later completion report from step 3**. Check the comparison declaration and register the confirmed evidence.

## 7. Verify the resulting state

Inspect **Care pathway**, **Evidence** and **History**. Run **Check evidence** again and confirm:

- The case requires renewed review.
- The correction explicitly refers to the later report; that report is superseded.
- Procedure evidence, clinician result review and plan communication require renewed confirmation. In the verified walkthrough, three of six confirmations remain valid.
- Closure is unavailable while the corrected incomplete state remains unresolved.
- Earlier source PDFs and the previous closure decision remain available.

Do not confirm completion against a source that says required steps remain pending.

## Optional views

**CL-002** shows a pending handoff: the current team remains accountable until acceptance. **Patient journey** shows guidance and ways to record questions or preferences. Keep the main walkthrough focused on CL-001.

See [validation](validation.md) for the versioned technical evidence and [scope and limitations](scope-and-limitations.md) for the boundaries of the demonstration.
