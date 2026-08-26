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
