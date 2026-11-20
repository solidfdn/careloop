# Sample PDFs for the CL-001 exercise

[Home](../README.md) · [English guide](../docs/demo-guide.md) · [日本語ガイド](../docs/demo-guide.ja.md)

These files support the optional **CL-001 upload and closure exercise** in the hands-on guide. The records for the main video cases, **CL-015** and **CL-025**, are already present in the 300-patient workspace. Upload these files only to CL-001.

Download both files using the direct links below for the optional exercise. Keep their contents unchanged.

| File | Role in the demonstration |
| --- | --- |
| [CareLoop_Demo_Completed_SYN001_v1.pdf](https://github.com/solidfdn/careloop/raw/refs/heads/main/demo-data/CareLoop_Demo_Completed_SYN001_v1.pdf) | A later report stating that all required procedure steps were performed. Register it as **new evidence**. |
| [CareLoop_Demo_Correction_SYN001_v1.pdf](https://github.com/solidfdn/careloop/raw/refs/heads/main/demo-data/CareLoop_Demo_Correction_SYN001_v1.pdf) | A correction stating that only the first stage was performed and required steps remain pending. Register it as a **correction to the later completion report**. |

Both documents were created for the **CL-001 / SYN-001** demo case. The first visit is already recorded in CareLoop. Add the completion report as a later event, then link the correction to that completion report. The first visit stays in the case history.

The PDFs retain their original `v0.4.4` internal headings and `01 Nov 2026` record dates. Those labels identify the source fixtures; the current application interface is v0.5.2 (RC32). The historical v0.4.11 technical walkthrough and v0.4.12 rules-only verification used these same files.

## SHA-256

| File | Hash |
| --- | --- |
| Completed | `dc9ba8ebff87a3fc39fc73a60c2388ed9896d905d603dcffe0c532c4a720c84a` |
| Correction | `54bcdba3721237c6fe5c4fc501fd1023e3f82458e1ac0fd5991b28e1dec3dc72` |

日本語：上の2点は任意のCL-001取込み・終了演習用です。動画で扱うCL-015とCL-025の資料は、最初から各症例に登録されています。演習には、2点をそのままダウンロードして使用します。最初のPDFは後日の新しい報告として追加し、2点目はその後日の報告に対する訂正として登録します。文書の旧版表記と現行アプリの版は別です。どちらも演習用に作成した資料です。
