# Jobbird Scraper

Extract structured data from [jobbird.com](https://jobbird.com) — the Netherlands' dedicated job board. Structured salary ranges, employment types, and incremental change tracking for new and updated listings.

**[Jobbird Scraper - Netherlands Job Board on Apify →](https://apify.com/blackfalcondata/jobbird-scraper?fpr=1h3gvi)**

---

## Key features





**Search with filters** — Search by keyword and location. Filter by sort by, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, direct apply URLs for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases





**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from jobbird.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from jobbird.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on jobbird.com to inform pricing decisions, hiring plans, or candidate negotiations.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "software engineer",
  "maxResults": 50,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords. |
| `location` | string | — | City or region in the Netherlands. |
| `radius` | integer | `30` | Search radius around the location in kilometres. |
| `category` | string | — | Filter by category slug (e.g. 'ict-automatisering'). |
| `contractType` | string | — | Filter by contract type (e.g. 'fulltime', 'parttime', 'temporary'). |
| `sortBy` | enum | `"date"` | Sort order for results. |
| `maxResults` | integer | `25` | Maximum total results (0 = unlimited). |
| `includeDetails` | boolean | `true` | Fetch full job details (description, skills, benefits, salary, hours). |
| `descriptionMaxLength` | integer | `0` | Truncate description to N chars. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `incrementalMode` | boolean | `false` | Compare against previous run state and emit only new/changed jobs. |
| `stateKey` | string | — | Stable identifier for tracked universe (required when incrementalMode is true). |

---

## FAQ

**How many results can I get?**
The number of results depends on available listings matching your query. Use `maxResults: 0` for unlimited results. Typical keyword searches return between 50 and 5000+ results.

**Does it support location-based filtering?**
Yes. Set `location` to a Dutch city or region (e.g. "Amsterdam", "Utrecht", "Rotterdam") and `radius` (default 30 km) to control the search area.

**Can I filter by contract type?**
Yes. Use `contractType` with values like `fulltime`, `parttime`, or `temporary`. Use `category` to filter by job category slug (e.g. `ict-automatisering`).

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

**Is it legal to scrape jobbird.com?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**Can I integrate with Zapier or Google Sheets?**
Yes. Use Apify's built-in integrations to export results to Google Sheets, trigger Zapier workflows, or connect to Make (Integromat) when a run completes.

---

## Known limitations

- Jobbird.com only covers the Netherlands — not suitable for other countries
- Salary data is not present on all listings — unavailable fields are returned as `null`
- Contact details (email, phone) are not exposed by jobbird.com's public API — these fields are always `null`
- Category filter requires an exact slug (e.g. `ict-automatisering`) — free-text category names are not resolved
- Pagination is sequential (no parallelism) because Jobbird's API does not return total result counts upfront


## Output fields

Every listing returns the same 28-field schema. Missing values are `null` — never omitted.

- `jobId`
- `title`
- `company`
- `companyId`
- `companyUrl`
- `location`
- `locationUrl`
- `salaryMin`
- `salaryMax`
- `salaryType`
- `employmentType`
- `hoursMin`
- `hoursMax`
- `hoursType`
- `category`
- `educationLevel`
- `skills`
- `benefits`
- `description`
- `applicationUrl`
- `recruitmentType`
- `isPremium`
- `url`
- `postedDate`
- `scrapedAt`
- `source`
- `portalUrl`
- `changeType`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "e0c99d3769b75b1489f079a44073248c7359e014b230feae757ce63dd6cbbd3c",
  "title": "backoffice medewerker Verkoop, Ochtrup Duitsland",
  "company": "GGM Gastro International GmbH",
  "companyId": 49224,
  "companyUrl": null,
  "location": "Enschede",
  "locationUrl": "https://www.jobbird.com/nl/vacatures/enschede",
  "salaryMin": 280000,
  "salaryMax": 320000,
  "salaryType": "MONTHLY",
  "employmentType": "fulltime",
  "hoursMin": 40
}
```

*Truncated — full records contain 28 fields. See Output fields for the complete schema.*


**[Try Jobbird Scraper - Netherlands Job Board now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/jobbird-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.001 |

See the [actor on Apify](https://apify.com/blackfalcondata/jobbird-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data





- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal


## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---
---

*Last updated: 2026 03*
