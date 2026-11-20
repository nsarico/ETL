# ETL Pipelines

Modular, idempotent Extract-Transform-Load (ETL) pipelines responsible for ingesting raw data from upstream sources, validating schemas, and landing structured datasets into the warehouse staging layer.

## Overview

This repository handles the ingestion and pre-warehouse processing boundary of the data platform:
- **Extract:** Pulls batch and incremental data from external APIs, RSS/web feeds, and file drops.
- **Validate & Normalize:** Enforces schema contracts, standardizes timestamps/encodings, and deduplicates incoming records.
- **Load:** Writes partitioned Parquet/JSON payloads to object storage or loads directly into raw/staging warehouse tables with watermark tracking.

## Repository Structure

```text
├── config/                 # Source definitions, schedules, and connection templates
├── pipelines/              # Domain-specific ETL jobs
│   └── <source_name>/
│       ├── extract.py      # Source connectors & incremental watermark logic
│       ├── transform.py    # Cleaning, normalization & schema enforcement
│       └── load.py         # Target sink writers (object storage / staging DB)
├── shared/                 # Reusable utilities (logging, retries, schema validators)
├── tests/                  # Unit and integration tests with sample payloads
├── .env.example            # Required environment variables template
├── pyproject.toml          # Dependencies and linter/test configuration
└── README.md
