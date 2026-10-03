<!-- SHOWCASE_START --><div align="center">[![Typing](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=22&duration=2800&pause=900&color=58A6FF&center=true&vCenter=true&width=900&lines=operational%20lead%20tracking%20workflow;AI%20%7C%20Automation%20%7C%20Engineering;Explore%20the%20project%20%F0%9F%9A%80)](https://github.com/shaikshahid777/operational-lead-tracking-workflow)<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0D1117,50:161B22,100:58A6FF&height=110&section=header&text=operational-lead-tracking-workflow&fontSize=26&fontColor=FFFFFF&animation=twinkling&fontAlignY=65" width="100%" alt="Animated project banner"/>

[![Repository](https://img.shields.io/badge/Repository-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/shaikshahid777/operational-lead-tracking-workflow) [![Issues](https://img.shields.io/badge/Report-Issue-red?style=for-the-badge&logo=github)](https://github.com/shaikshahid777/operational-lead-tracking-workflow/issues/new) [![Stars](https://img.shields.io/github/stars/shaikshahid777/operational-lead-tracking-workflow?style=for-the-badge&logo=github)](https://github.com/shaikshahid777/operational-lead-tracking-workflow/stargazers) [![Fork](https://img.shields.io/github/forks/shaikshahid777/operational-lead-tracking-workflow?style=for-the-badge&logo=github)](https://github.com/shaikshahid777/operational-lead-tracking-workflow/fork) [![Profile](https://img.shields.io/badge/Profile-Visit-0A66C2?style=for-the-badge&logo=github)](https://github.com/shaikshahid777)</div>

> ✨ **Project Showcase Mode:** animated banner • interactive navigation • live repository actions

[🚀 Repository](https://github.com/shaikshahid777/operational-lead-tracking-workflow) · [🐞 Report Issue](https://github.com/shaikshahid777/operational-lead-tracking-workflow/issues/new) · [⭐ Star](https://github.com/shaikshahid777/operational-lead-tracking-workflow/stargazers) · [🔱 Fork](https://github.com/shaikshahid777/operational-lead-tracking-workflow/fork) · [👤 Profile](https://github.com/shaikshahid777)

<!-- SHOWCASE_END -->

# Operational Lead Tracking Workflow — Lesson 5 Assessment

Production-style n8n workflow using Google Sheets as an operational tracking database.

## Workflow

```text
Manual Trigger
      ↓
READ_GetSpreadsheetRows
      ↓
FILTER_PendingStatus
      ↓
LOCK_UpdateStatusProcessing
      ↓
ACTION_ProcessInvoice
      ↓
IF_ProcessSuccess
   ↙             ↘
Success           Failure
 ↓                  ↓
UPDATE_StatusCompleted   UPDATE_StatusFailed
```

## Google Sheets Schema

The operational spreadsheet uses:

- `lead_id`
- `name`
- `email`
- `lead_status`
- `execution_id`
- `updated_at`
- `error_details`

## Processing Logic

1. Read lead records from Google Sheets.
2. Filter to records where `lead_status = Pending`.
3. Match the selected row using `lead_id`.
4. Update the status to `Processing` and record execution ID and timestamp.
5. Run the downstream business-action simulation.
6. Continue on processing error for controlled failure handling.
7. Route success to `Completed`.
8. Route failure to `Failed` and store `error_details`.

## Audit Fields

`execution_id` provides traceability to the n8n execution. `updated_at` records the most recent state change. `error_details` preserves failure information for operational troubleshooting.

## Validation Evidence

The tested lead `L001` (Rahul) was successfully processed and the Google Sheet final state showed `lead_status = Completed`.

## Files

```text
operational-lead-tracking-workflow/
├── README.md
├── workflow/
│   └── Operational_Lead_Tracker.json
├── documentation/
│   └── Lead_Tracking_n8n_Workflow_Guide.pdf
├── screenshots/
│   └── execution-final.png
└── setup/
    └── setup-instructions.md
```

## Security

Google Service Account credentials are kept in n8n and must not be committed to this public repository. Do not upload private keys, passwords, tokens, or other secrets.
