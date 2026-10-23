# n8n from zero: enquiry form with a human approval step

The free workflow from the BideenBuilds video **"n8n from zero: your first useful workflow in 20 minutes (with a human approval step)"**.

Video: [VIDEO_LINK_PLACEHOLDER]

## What it does

1. **Form Trigger** - a simple enquiry form (name, email, company, message).
2. **Clean the data** - trims spaces, lowercases the email, flags obviously bad emails.
3. **Valid?** - bad input goes to a log branch and stops there.
4. **Check for duplicate** - looks the email up in a Google Sheet. Existing leads are skipped.
5. **Save lead** - appends new leads to the sheet with status `pending approval`.
6. **Ask me first** - emails *you* an Approve / Decline request (Gmail "send and wait for response"). Nothing goes to the lead until you answer.
7. **Approved** - sends the lead a confirmation email. **Declined** - updates the sheet row to `rejected - no email sent`.

The approval step is the point: an automation should not email anyone without a person saying yes, and every outcome is logged.

## How to import

1. In n8n, create a new workflow, open the menu (top right) and choose **Import from File**.
2. Select `n8n-from-zero-workflow.json`.
3. Add your credentials (below), set your sheet ID and approval email, then click **Test workflow** and submit the form.

Self-hosted community edition or n8n Cloud both work. Check n8n's site for current options.

## Credentials you add yourself

No credentials are included. You need:

- **Google Sheets OAuth2** - on the three Google Sheets nodes.
- **Gmail OAuth2** - on "Ask me first (approval)" and "Send confirmation email".

Then replace:

- `YOUR_GOOGLE_SHEET_ID` with your sheet's ID. The sheet needs a `Leads` tab with the columns `name, email, company, message, received_at, status`.
- `you@example.com` with the address that should get approval requests.

Never paste passwords or API keys into node fields. Use n8n credentials.

## Test data

`sample-data.json` has made-up leads (example.com emails), including one bad email so you can test the rejection path. Test with messy data, not just perfect data.

## Three beginner mistakes this avoids

- Testing only with perfect data.
- Pasting passwords and API keys into nodes instead of using credentials.
- Letting automations send to customers with no approval and no log.

## Licence

MIT - see `LICENSE`.

---

Built by BerleyData - Systems, not hacks.
