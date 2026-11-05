# SEEK, JobStreet & JobsDB Scraper

Scrape job listings and salaries from SEEK, JobStreet and JobsDB across 8 countries in one run. No login, no API key. Runs on [Apify](https://apify.com/smoldesk/seek-jobs-scraper).

## What you get

- **8 markets**: SEEK in AU and NZ, JobStreet in MY, SG, PH and ID, JobsDB in HK and TH.
- **Search**: keywords times markets, with location, posted-within, work type and remote or hybrid filters.
- **Salary**: the label parsed into `salaryMin`, `salaryMax`, `salaryCurrency`, `salaryPeriod` and annualised values.
- **Job data**: title, company, location, classification, work type, listing date and company profile link.
- **Full ad** (optional): description as Markdown and HTML, expiry date, company industry and size.
- **New jobs only** mode for daily alerts.

## Run it

Open the [SEEK Scraper on Apify](https://apify.com/smoldesk/seek-jobs-scraper), fill in the form and click Start. Or call it from code with your [Apify token](https://console.apify.com/settings/integrations):

```bash
curl -X POST "https://api.apify.com/v2/acts/smoldesk~seek-jobs-scraper/run-sync-get-dataset-items?token=YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "keywords": ["software engineer", "data analyst"],
    "markets": ["MY", "SG"],
    "location": "Kuala Lumpur",
    "dateRange": "7",
    "maxJobsPerSearch": 200,
    "includeDetails": true
  }'
```

## Sample output

```json
{
  "market": "MY",
  "id": "95194226",
  "url": "https://my.jobstreet.com/job/95194226",
  "title": "Software Engineer (Full-Stack, AI-Assisted Development)",
  "company": "Ekomas Technologies",
  "location": "Alam Damai, Kuala Lumpur",
  "classification": "Information & Communication Technology",
  "workType": "Full time",
  "salaryLabel": "RM 5,000 to RM 7,500 per month",
  "salaryMin": 5000,
  "salaryMax": 7500,
  "salaryCurrency": "MYR",
  "salaryPeriod": "month",
  "salaryAnnualMin": 60000,
  "salaryAnnualMax": 90000,
  "listedAt": "2026-10-12T00:23:39Z",
  "companyIndustry": "Computer Software & Networking",
  "companySize": "11-50 employees"
}
```

Export as JSON, CSV or Excel, or pipe it into Google Sheets, Make, Zapier or n8n.

## Pricing

Pay per result. No start fee, no monthly fee.

| Result | Per 1,000 |
|---|---|
| Job listing | $0.80 |
| Full description add-on | +$0.40 |

## Limits

- SEEK caps results at about 550 per search. Split by location, date or work type for more.
- About half of SEEK ads show no salary, so those fields are `null`.
- Jobs whose full description fails to load are saved without it and not charged the add-on.

## FAQ

**Does SEEK or JobStreet have a public API?**
Not for job search. The official APIs are for advertisers and ATS partners. This returns the same listings as JSON.

**How do I get JobStreet salary data?**
Every job with a visible salary has `salaryMin`, `salaryMax`, `salaryCurrency`, `salaryPeriod` and annualised values. Average them per role straight from the dataset.

**Can I scrape JobStreet Malaysia only, or one city?**
Yes. Set `markets` to `["MY"]` and `location` to a city such as `Penang`.

**How do I get alerts for new jobs?**
Turn on `onlyNewJobs`, set `sortBy` to `date` and schedule the run daily. Send results to Slack, Google Sheets or a webhook.

**Do I need an account or a proxy?**
No. It reads the same public search any visitor uses.

## More scrapers

SEEK is one of 15 no-login scrapers by Smoldesk Studios. See the full list: [smoldesk/apify-scrapers](https://github.com/smoldesk/apify-scrapers).
