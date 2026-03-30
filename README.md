# Jobbird Scraper

Extract structured data from [jobbird.com](https://jobbird.com) — the Netherlands' dedicated job board. Structured salary ranges, employment types, and incremental change tracking for new and updated listings.

**[Jobbird Scraper on Apify →](https://apify.com/blackfalcondata/jobbird-scraper)**

---

## Key features



**Search with filters** — Search by keyword and location. Filter by sort by, and more.

**Detail enrichment** — Fetch full job descriptions, salary data, employer profiles, direct apply URLs for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

---

## Use cases



**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from jobbird.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from jobbird.com.

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

---

## Related products by Black Falcon Data



- [StepStone Scraper](https://github.com/BlackFalconData-org/stepstone-scraper) — Job listings from 18 European portals
- [Indeed Job Scraper](https://github.com/BlackFalconData-org/indeed-job-scraper) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://github.com/BlackFalconData-org/glassdoor-job-scraper) — Glassdoor listings with company ratings

---

*Last updated: 2026 03*
