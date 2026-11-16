# CRM Lead Capture & Auto-Reply — Make.com

A production lead-management workflow built in **Make.com** for [SA SYNEXIS](https://sasynexis.com). It runs live behind the contact form on sasynexis.com.

Every enquiry is validated, de-duplicated, stored in a Google Sheets CRM, logged, and answered within seconds — with no manual work.

## What it does

```
Website form ──► Webhook ──► Validate & normalise ──► Look up existing leads (Google Sheets)
                                                              │
                                    ┌─────────────────────────┴─────────────────────────┐
                                New lead                                         Returning lead
                                    │                                                   │
                      Add row to LEADS sheet                              Update their existing row
                      Log to ENQUIRY_LOG                                  Log to ENQUIRY_LOG
                      Personalised auto-reply to client                   Alert owner to reply personally
                      Instant alert email to owner
```

## Features

- **Validation filter** — name, phone, service and message must be present; email checked with a regex.
- **Email normalisation** — trimmed and lower-cased, so `John@Mail.com ` and `john@mail.com` are the same lead.
- **No duplicates** — an array lookup finds an existing row by email; returning leads update their row instead of creating a new one.
- **Two sheets** — `LEADS` (one row per person, with status) and `ENQUIRY_LOG` (every enquiry, for history).
- **Instant personalised auto-reply** to new leads (HTML email).
- **Owner alerts** for both new and returning leads.
- **Error handling** — the client auto-reply retries 3 times via a *Break* handler; owner alerts use *Ignore* so a mail hiccup never blocks the CRM.

## Stack

Make.com · Webhooks · Google Sheets · Gmail · Regex · Array functions · Error handlers (Break / Ignore)

## How to use this blueprint

1. In Make.com, create a new scenario → **⋯ → Import Blueprint** → choose `blueprint.json`.
2. Create a webhook in the first module and point your website form to it (POST JSON: `name`, `email`, `phone`, `service_interest`, `message`).
3. Create a Google Sheet with two tabs, `LEADS` (columns A–I) and `ENQUIRY_LOG`, and replace `YOUR_SPREADSHEET_ID`.
4. Connect your Google and Gmail accounts, then replace `owner@example.com`, `YOUR COMPANY` and `YOUR NAME`.
5. Turn the scenario on.

> All private IDs, connections and email addresses have been removed from this public copy.

## Author

**Mohammed Shafiul Alam** — Founder & CEO, SA SYNEXIS™ · Full Stack Developer · n8n System Architect · Make Advanced certified
🌐 [sasynexis.com](https://sasynexis.com) · London, UK

Need a system like this for your business? [Book a free consultation](https://sasynexis.com/#contact).
