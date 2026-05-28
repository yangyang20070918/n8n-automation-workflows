# n8n Automation Workflows

Workflow automation templates built with **n8n** (self-hosted via Docker). Demonstrates practical automation patterns including RSS aggregation, GitHub event monitoring, and CSV data processing.

## Tech Stack

- **n8n** — Open-source workflow automation (self-hosted)
- **Docker / Docker Compose** — Container deployment
- **Node types used:** Schedule Trigger, Webhook, RSS Feed Read, Filter, Switch, Code, Set, Item Lists, Respond to Webhook

## Workflows

### 1. RSS News Aggregator (`01_rss_news_aggregator.json`)
Fetches news from Google News Japan RSS feed, filters and formats articles.
- **Trigger:** Schedule (every 6 hours) or Webhook (GET `/news-feed`)
- **Flow:** RSS Read → Filter valid items → Limit to 10 → Format output → Respond
- **Use case:** News monitoring, content aggregation

### 2. GitHub Webhook Monitor (`02_github_webhook_monitor.json`)
Receives GitHub webhook events and routes them by event type (push, issue, PR).
- **Trigger:** Webhook (POST `/github-events`)
- **Flow:** Receive event → Route by type (Switch) → Format per type → Build notification
- **Use case:** Repository monitoring, CI/CD notification integration

### 3. CSV Data Processing Pipeline (`03_csv_data_pipeline.json`)
Accepts CSV data via webhook, cleans/normalizes it, and returns structured JSON.
- **Trigger:** Webhook (POST `/process-csv`)
- **Flow:** Receive CSV → Parse → Remove empty rows → Clean & normalize → Deduplicate → Build JSON output
- **Use case:** Data ETL, batch data cleaning

## Setup

### Start n8n

```bash
docker compose up -d
```

Access n8n UI: http://localhost:5678
- Username: `admin`
- Password: `admin123`

### Import Workflows

1. Open n8n UI → **Workflows** → **Import from File**
2. Select a JSON file from the `workflows/` directory
3. Activate the workflow

### Stop n8n

```bash
docker compose down
```

## Project Structure

```
n8n-automation-workflows/
├── docker-compose.yml        # n8n Docker deployment
├── workflows/
│   ├── 01_rss_news_aggregator.json     # RSS feed automation
│   ├── 02_github_webhook_monitor.json  # GitHub event routing
│   └── 03_csv_data_pipeline.json       # CSV → JSON ETL pipeline
└── README.md
```
