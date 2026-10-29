# Trade Compliance Automation | n8n

**Automating supplier document follow-ups with human approval built in.**

A practical workflow automation prototype built with **n8n, Google Sheets, and Gmail** to improve document tracking, overdue monitoring, and supplier communications in Global Trade and Trade Compliance operations.

---

## 🎯 Project Overview

Supplier document management often involves repetitive status checks, deadline monitoring, and follow-up emails. When repeated across multiple records, these tasks can create a significant operational workload.

This project demonstrates how workflow automation can structure these activities while keeping human approval in control of outbound communications.

## ⚙️ Workflows

### 1. Supplier Follow-up

Evaluates document records in Google Sheets and identifies their status based on document receipt and due dates.

**Key capabilities:**
- Identifies overdue documents.
- Flags pending documents that are still within their deadlines.
- Identifies records requiring review.
- Prepares supplier follow-up emails.
- Updates tracking records with evaluation results.
- Marks emails as pending approval instead of sending them automatically.

### 2. Approved Email Dispatch

Checks configured approval and status conditions before sending supplier emails through Gmail.

**Key capabilities:**
- Validates the record against configured sending conditions.
- Requires an explicit `APPROVED` status.
- Sends the prepared email through Gmail.
- Updates the tracking record after successful dispatch.

**Human approval is a key control:** the first workflow prepares the follow-up, while the second handles email dispatch only when the configured conditions are met.

## 🔄 Workflow Architecture

    Google Sheets
          |
          v
    Supplier Follow-up
          |
          v
    Evaluate document status and deadlines
          |
          v
    Prepare supplier follow-up email
          |
          v
    Set status: PENDING_APPROVAL
          |
          v
    Human reviews and approves
          |
          v
    Approved Email Dispatch
          |
          v
    Send email through Gmail
          |
          v
    Update tracking status: SENT

Both workflows are configured for manual execution in this prototype. Scheduled execution is not configured.

## 🧰 Technology Stack

| Technology | Purpose |
|---|---|
| n8n | Workflow automation and orchestration |
| Google Sheets | Document tracking and status management |
| Gmail | Supplier email dispatch |

## 📋 Google Sheets Configuration

Create a Google spreadsheet with a worksheet named:

`Supplier_Tracking`

Use the following column headers in the first row:

| Column | Description |
|---|---|
| `document_record_id` | Unique document record identifier |
| `operation_id` | Related operation identifier |
| `supplier` | Supplier name |
| `document_required` | Required document description |
| `document_status` | Document receipt status |
| `due_date` | Document due date |
| `supplier_email` | Supplier email address |
| `follow_up_status` | Follow-up evaluation result |
| `evaluation_date` | Evaluation date |
| `email_subject` | Prepared email subject |
| `email_body` | Prepared email body |
| `email_status` | Email processing status |
| `approval_status` | Approval status |

### Supported status values

**Document status**
- `pending`
- `received`

**Follow-up status**
- `OVERDUE`
- `PENDING_ON_TIME`
- `RECEIVED`
- `REVIEW_REQUIRED`

**Email status**
- `PENDING_APPROVAL`
- `SENT`

**Approval status**
- `NOT_APPROVED`
- `APPROVED`

Use a unique `document_record_id` for each record. Supported date formats are `YYYY-MM-DD` and `DD/MM/YYYY`.

The workflows rely on configured conditions and expected column names. Review the workflow logic before changing these values.

## 🚀 Installation and Setup

### Prerequisites

- An n8n instance.
- A Google account with access to Google Sheets and Gmail.
- A spreadsheet configured with the required columns.
- Google Sheets and Gmail credentials configured in n8n.

### Step 1 — Import the workflows

1. Download the JSON files from this repository.
2. Open your n8n instance.
3. Import `Supplier-Follow-up.json`.
4. Import `Approved-Email-Dispatch.json`.

### Step 2 — Configure Google Sheets

1. Create your spreadsheet and add the required column headers.
2. Copy the spreadsheet ID from its URL.
3. Open the Google Sheets nodes in both workflows.
4. Replace the placeholder spreadsheet ID with your own.
5. Confirm that the worksheet name is `Supplier_Tracking`.

### Step 3 — Configure credentials

Configure your own Google Sheets and Gmail credentials in n8n.

**Never publish OAuth client secrets, access tokens, passwords, or private account information.**

### Step 4 — Test the workflows

1. Populate the spreadsheet with fictitious test records.
2. Execute the Supplier Follow-up workflow manually.
3. Review the evaluation results and prepared emails.
4. Review the relevant record and set its approval status to `APPROVED`.
5. Execute the Approved Email Dispatch workflow manually.
6. Verify the email and the final tracking status.

**Use fictitious supplier data and a controlled test inbox before connecting the workflows to real records.**

## 🛡️ Controls and Limitations

This project is a prototype intended for demonstration and testing.

- Email dispatch depends on the configured approval conditions, spreadsheet data, and credentials.
- Scheduled execution is not configured.
- The prototype does not guarantee that an email is delivered or read.
- If an email is sent but the subsequent spreadsheet update fails, the record may not reflect the actual sending status.
- Review records before retrying a failed execution to reduce the risk of duplicate emails.
- Production use would require additional testing, monitoring, error handling, access controls, and safeguards against duplicate dispatches.

## 💡 Business Value

The project explores how workflow automation can help Global Trade and Trade Compliance teams:

- Reduce repetitive manual status checks.
- Improve visibility into pending and overdue documentation.
- Standardize supplier follow-up preparation.
- Preserve human oversight before email dispatch.
- Create a more structured and traceable operational process.

No quantified productivity improvements or time savings are claimed. The prototype demonstrates the workflow design and its potential applications.

## 👨‍💻 About This Project

This independent project combines experience in Global Trade operations with an interest in workflow automation and process improvement.

**The objective is simple: reduce repetitive operational work without removing human oversight from critical process steps.**

It demonstrates practical process thinking, operational controls, and low-code automation using n8n.

---

*Disclaimer: This is an independent demonstration project and is not affiliated with or endorsed by any employer or software vendor. Test with fictitious data and review all workflows before using them in a live environment.*
