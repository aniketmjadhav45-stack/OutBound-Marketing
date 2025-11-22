# OutBound-Marketing
📣 Outbound Marketing Automation — n8n Workflow Documentation

This repository contains an automated outbound marketing workflow built in n8n.
It takes a list of company URLs, extracts social media handles (especially Instagram), verifies data quality, filters valid leads, and saves everything into Google Sheets — ready for outreach.

🚀 Workflow Overview

The automation contains three major pipelines, each starting from a Webhook trigger. All pipelines follow the same logic with different input sources.

🧩 Pipeline Breakdown
1. Input Capture (Webhook Trigger)

Each workflow begins when a user submits a company website URL.
This URL is captured through a Webhook or an HTTP API trigger.

2. Lead Extraction (Apify Scraper / HTTP Requests)

After input is received, the workflow sends the company URL to an Apify scraper actor (or any scraping API).
The scraper extracts:

Website social icons

Visible Instagram links

Contact meta-data

Public-facing handles

Multiple HTTP Request nodes are used to:

✔ Send the scraping job
✔ Poll Apify for results
✔ Retrieve the final cleaned JSON data

3. Data Cleaning & Filtering

Several Code nodes transform the raw scraper output:

Parse extracted handles

Remove duplicates

Validate Instagram URLs

Standardize output format

Then IF nodes filter only:

✔ Valid handles
✔ Unique handles
✔ Reachable social links

Invalid or empty entries are discarded.

4. Email Verification (NeverBounce API)

Another HTTP Request is sent to NeverBounce to verify email addresses (if included).

Removes:

❌ Personal emails
❌ Disposable emails
❌ Invalid or risky addresses

Keeps:

✔ Business domain emails
✔ Deliverable addresses

5. Save to Google Sheets

All validated records are merged and appended to a Google Sheet for outreach.
Each row contains:

Website

Instagram handle

Email (if valid)

Verification status

Scraping timestamp

Lead source pipeline

This becomes your master outbound prospecting sheet.

📊 How the Workflow Works (Step-by-Step)

1️⃣ User submits a URL → Webhook receives it
2️⃣ Scraper runs → Extracts social links + metadata
3️⃣ Code nodes clean the output
4️⃣ IF nodes filter invalid data
5️⃣ Email validation happens via API
6️⃣ All good leads are merged
7️⃣ Final data stored in Google Sheets
8️⃣ Ready for Instagram/Email outreach

📁 Files Included in This Repo
/workflow/
    outbound-marketing.json   # Full n8n workflow export
/docs/
    architecture.png          # High-level workflow diagram
    description.md            # Technical documentation

🛠 Tech Stack

n8n (workflow automation)

Apify (web scraping)

Google Sheets API

NeverBounce (email verification)

Custom JavaScript parsers

✅ Key Benefits

Fully automated lead extraction

No manual research required

Clean & verified social handles

Highly scalable for hundreds of URLs

Works with any scraping API
