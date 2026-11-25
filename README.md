# USAspending Scraper & Unofficial API (Python, Node.js, MCP)

[Run USAspending Scraper - Federal Contracts & Awards on Apify](https://apify.com/evpp/usaspending) to export USAspending data as clean JSON, CSV, Excel, or an API feed. This repository is a developer quick-start kit with working Python and Node.js clients, an MCP configuration, a real sample dataset, and an n8n automation template.

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-orange)](https://apify.com/evpp/usaspending)

## Why use this USAspending scraper?

- Export USAspending data without building or maintaining a custom scraper
- Get flat, schema documented JSON ready for analytics, lead generation, market research, and AI agents
- Run manually, on a schedule, through the Apify API, or through MCP compatible AI tools
- Use the included 25 plus row sample dataset to prototype before running the live Actor

Built for GovCon BD teams, federal contractors tracking competitors' awards, journalists, investors in gov-exposed companies.

## Quick start on Apify

Open [https://apify.com/evpp/usaspending](https://apify.com/evpp/usaspending) and use this input:

```json
{
  "awardTypes": "contracts",
  "agency": "Department of Defense",
  "minAmount": 1000000,
  "sortBy": "amount",
  "includeDetails": true,
  "maxItems": 10
}
```

## Python

```bash
pip install -r requirements.txt
export APIFY_TOKEN=your_apify_token
python python/run.py
```

On Windows PowerShell, use `$env:APIFY_TOKEN="your_apify_token"` instead of `export`.

## Node.js

```bash
npm install
export APIFY_TOKEN=your_apify_token
node node/run.mjs
```

## MCP and AI agents

Add the hosted Apify MCP server from `mcp-config.json` to your MCP client:

```json
{
  "mcpServers": {
    "apify": {
      "type": "http",
      "url": "https://mcp.apify.com/?tools=evpp/usaspending"
    }
  }
}
```

Then ask your agent to run `evpp/usaspending`, inspect the output schema, or export the latest dataset. The direct MCP URL is `https://mcp.apify.com/?tools=evpp/usaspending`.

## n8n automation

Import `n8n-workflow.json` into n8n, select your Apify credential, replace the webhook placeholder, and activate the schedule. The workflow runs the Actor every morning and posts fresh dataset items to your webhook.

## Output schema

| Field | Type | Description |
|---|---|---|
| `awardId` | string | Public award identifier (PIID for contracts, FAIN/URI for assistance) |
| `generatedId` | string | USAspending generated unique award ID |
| `recipientName` | string | Legal name of the award recipient (contractor / grantee) |
| `recipientUei` | string | Unique Entity Identifier (UEI) of the recipient |
| `awardAmount` | number | Total obligated amount in USD |
| `awardType` | string | Award type description (e.g. DEFINITIVE CONTRACT, COOPERATIVE AGREEMENT) |
| `awardCategory` | string | USAspending award category (contract, grant, direct payment, loan, idv) |
| `startDate` | string | Period of performance start date |
| `endDate` | string | Period of performance current end date |
| `awardingAgency` | string | Top-tier awarding agency |
| `awardingSubAgency` | string | Sub-tier awarding agency / office |
| `fundingAgency` | string | Top-tier funding agency |
| `fundingSubAgency` | string | Sub-tier funding agency / office |
| `description` | string | Award description / purpose text |
| `naicsCode` | string | NAICS industry code (contracts only) |
| `naicsDescription` | string | NAICS industry description (contracts only) |
| `pscCode` | string | Product or Service Code (contracts only) |
| `cfdaNumber` | string | Assistance Listing (CFDA) number (grants and assistance only) |
| `cfdaTitle` | string | Assistance Listing (CFDA) program title (grants and assistance only) |
| `recipientCity` | string | Recipient city |
| `recipientState` | string | Recipient state name |
| `recipientCountry` | string | Recipient country |
| `url` | string | Award profile page on usaspending.gov |

## Real sample output

The first sanitized row from the included sample dataset:

```json
{
  "awardId": "W912DQ24C3003",
  "generatedId": "CONT_AWD_W912DQ24C3003_9700_-NONE-_-NONE-",
  "recipientName": "SEVENSON ENVIRONMENTAL SERVICES, INC.",
  "recipientUei": "VHPJR3MJWV49",
  "awardAmount": 180000000,
  "awardType": "DEFINITIVE CONTRACT",
  "awardCategory": "contract",
  "startDate": "2024-09-12",
  "endDate": "2032-09-11",
  "awardingAgency": "Department of Defense",
  "awardingSubAgency": "Department of the Army",
  "fundingAgency": "Environmental Protection Agency",
  "fundingSubAgency": "Environmental Protection Agency",
  "description": "CDE OU4 REMEDIAL ACTION",
  "naicsCode": "562910",
  "naicsDescription": "REMEDIATION SERVICES",
  "pscCode": "F108",
  "recipientCity": "NIAGARA FALLS",
  "recipientState": "NEW YORK",
  "recipientCountry": "UNITED STATES",
  "url": "https://www.usaspending.gov/award/CONT_AWD_W912DQ24C3003_9700_-NONE-_-NONE-"
}
```

## Files in this kit

| File | Purpose |
|---|---|
| `python/run.py` | Working Python Apify API example |
| `node/run.mjs` | Working Node.js Apify API example |
| `mcp-config.json` | MCP server configuration for AI agents |
| `sample-output.json` | First five sanitized sample rows |
| `dataset-snapshot.csv` | 25 plus row evaluation snapshot |
| `DATASET_CARD.md` | Dataset documentation and provenance |
| `n8n-workflow.json` | Scheduled n8n automation template |

## Fresh data

This repository contains a static evaluation sample. For current data, run the live Actor: https://apify.com/evpp/usaspending

## Responsible use

The Actor reads public data from `usaspending.gov`. Review the source site's terms and applicable privacy rules before production use.
