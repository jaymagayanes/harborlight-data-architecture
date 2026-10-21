# Harborlight Media — Data Architecture

A reference data-platform architecture for **Harborlight Media**, a fictional streaming media company. The design illustrates how subscription, advertising and viewing data can move from operational sources into trusted datasets for reporting and downstream use.

> **Note:** Harborlight Media is fictional. All volumes, service levels and performance figures shown on the site are illustrative design targets, not measurements from a production system.

## Explore the site

**[Open the live architecture website](https://jaymagayanes.github.io/harborlight-data-architecture/)**

The site is organised into five sections:

- **Overview** — the platform's purpose, core design choices and an end-to-end view of a record's journey.
- **Ingestion** — approaches for bringing data in from files, APIs and streaming events.
- **Data model** — the warehouse modelling approach, including facts, dimensions and performance considerations.
- **Quality and monitoring** — validation checks, failure handling and alerting concepts.
- **AI-assisted workflow** — a controlled workflow for drafting SQL with AI assistance and validating the result before use.

## Architecture at a glance

The reference design brings together four broad source types and supports both batch and streaming patterns.

1. **Land raw data.** Files, API extracts and event data are retained in an S3 raw landing area.
2. **Validate incoming data.** Schema, completeness and volume checks identify unexpected or incomplete data; invalid records can be quarantined.
3. **Stage and clean.** ETL jobs standardise types and remove duplicates before data is promoted.
4. **Model core entities.** Shared business rules shape facts and dimensions so downstream consumers use consistent definitions.
5. **Serve trusted data.** Data marts support finance, advertising and growth reporting, while monitoring helps teams detect failed or late loads.

Batch processing and streaming are designed to coexist: daily reporting can use reconciled data, while operational views can use fresher event data. The target figures on the site (including approximately 40 million events per day, a 15-minute live-data delay and 99.5% on-time daily loads) are **design targets only**.

## Technology in the design

| Area | Technology / approach |
| --- | --- |
| Ingestion and validation | Python ETL jobs and API clients |
| Raw landing zone | AWS S3 |
| Streaming events | Kafka |
| Warehouse | Microsoft SQL Server, with partitions and columnstore considerations |
| Reporting | Tableau |
| AI-assisted development | SQL drafting supported by a validation checklist |

These technologies describe the proposed architecture, not a claim that a production implementation has been deployed.

## Repository contents

- `index.html` — overview page
- `ingestion.html` — ingestion patterns
- `model.html` — warehouse model
- `quality.html` — quality checks and monitoring
- `ai-workflow.html` — AI-assisted SQL workflow
- `style.css` — shared site styles
- `images/` — architecture and data-model diagrams

## Run locally

No build step is required for the static site.

1. Clone or download this repository.
2. Open `index.html` in a browser.

For a more consistent local browsing experience, serve the folder with any simple static HTTP server. The live site is published through GitHub Pages.

## Design principles

- Keep raw inputs available so downstream datasets can be rebuilt after fixes.
- Separate staging, core modelling and reporting marts.
- Use batch and streaming patterns where each makes sense.
- Treat quality checks and alerting as part of the data pipeline, not as afterthoughts.
- Use AI as an assistant rather than an authority: review and validate generated SQL before relying on it.

## Disclaimer

This is a portfolio reference design for learning and discussion. Harborlight Media is fictional, and the architecture, technology choices and performance targets are illustrative. This repository does not represent a live media company's internal systems or production metrics.
