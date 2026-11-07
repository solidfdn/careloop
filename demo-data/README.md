# Synthetic PDF fixtures

[Home](../README.md) · [English guide](../docs/demo-guide.md) · [日本語ガイド](../docs/demo-guide.ja.md)

These files support the optional **CL-001 upload and closure exercise** in the hands-on guide. The current video and primary walkthrough use **CL-006**, whose reports are already included after adding the 300-record demonstration dataset. Do not import these CL-001 PDFs into CL-006.

Download both files using the direct links below for the optional exercise. Keep their contents unchanged.

| File | Role in the demonstration |
| --- | --- |
| [CareLoop_Demo_Completed_SYN001_v1.pdf](https://github.com/solidfdn/careloop/raw/refs/heads/main/demo-data/CareLoop_Demo_Completed_SYN001_v1.pdf) | A later report stating that all required procedure steps were performed. Register it as **new evidence**. |
| [CareLoop_Demo_Correction_SYN001_v1.pdf](https://github.com/solidfdn/careloop/raw/refs/heads/main/demo-data/CareLoop_Demo_Correction_SYN001_v1.pdf) | A correction stating that only the first stage was performed and required steps remain pending. Register it as a **correction to the later completion report**. |

Both documents concern fictional case **CL-001 / SYN-001** and are marked as synthetic records. The initial specialist report is already present in the application. Do not replace that initial truthful report with the later completion report.

The PDFs retain their original `v0.4.4` internal headings and `01 Nov 2026` record dates. Those labels identify the source fixtures; the current application interface is v0.5.2 (RC9). These same fixture bytes were used in the historical v0.4.11 technical walkthrough and v0.4.12 rules-only verification; those checks remain versioned evidence, not a new RC9 execution.

## SHA-256

| File | Hash |
| --- | --- |
| Completed | `dc9ba8ebff87a3fc39fc73a60c2388ed9896d905d603dcffe0c532c4a720c84a` |
| Correction | `54bcdba3721237c6fe5c4fc501fd1023e3f82458e1ac0fd5991b28e1dec3dc72` |

日本語：上の2点は任意のCL-001取込み・終了演習用です。現在の動画で使うCL-006へは取り込まないでください。演習には、2点をそのままダウンロードして使用します。最初のPDFは後日の新しい報告として追加し、2点目はその後日の報告に対する訂正として登録します。文書の旧版表記と現行アプリの版は別です。いずれも架空資料で、実在する人の診療情報は含みません。
