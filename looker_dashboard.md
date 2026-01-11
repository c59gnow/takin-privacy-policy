# Looker Studio dashboard (GA4)

This repo includes a helper script to copy a Looker Studio template report.
GA4 itself does not import dashboards, so the "automatic" path is to copy a
template report and connect it to your GA4 property.

## Requirements
- GA4 property connected to Firebase.
- Looker Studio API enabled on a Google Cloud project.
- OAuth client secrets JSON (Desktop app).
- Python 3.9+ with:
  - google-auth
  - google-auth-oauthlib
  - google-api-python-client

Install deps:
```bash
pip install google-auth google-auth-oauthlib google-api-python-client
```

## Create a template report (one-time)
1) In Looker Studio, create a report and connect it to your GA4 property.
2) Build the layout you want (see AGENTS.md -> Analytics for events/params).
3) Copy the report ID from the URL:
   https://lookerstudio.google.com/reporting/REPORT_ID

## Copy the template with the script
```bash
python scripts/create_looker_dashboard.py \
  --client-secrets path/to/client_secrets.json \
  --template-report-id REPORT_ID \
  --title "Taquin Analytics"
```

The script prints a URL to the new report.

## After copy
- If the template uses a different GA4 property, use
  "Resource -> Manage added data sources -> Replace" to swap it.
- Create GA4 custom definitions for params (mode, theme_id, size, placement,
  app_language, etc.) so they appear in the report.
