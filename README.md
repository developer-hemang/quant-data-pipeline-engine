# Quant Data Pipeline Engine

> A production-oriented Python financial market data pipeline for ingesting, validating, cleaning, transforming, and storing OHLC/market data for quantitative research, backtesting, analytics, and machine learning.

[![Python](https://img.shields.io/badge/Python-3.x-blue)](https://www.python.org/)
[![Status](https://img.shields.io/badge/Status-In%20Development-orange)](#project-status)
[![Storage](https://img.shields.io/badge/Storage-Parquet-green)](#storage)
[![Data Source](https://img.shields.io/badge/Data%20Source-Angel%20One-orange)](#data-source)

---

## 📌 Overview

**Quant Data Pipeline Engine** is an extensible financial data engineering project designed to build a reliable data foundation for quantitative finance, algorithmic trading research, backtesting, analytics, and machine learning.

The pipeline transforms raw market data from external providers into:

```text
Raw Market Data
      ↓
Ingestion
      ↓
Validation
      ↓
Cleaning
      ↓
Normalization
      ↓
Transformation
      ↓
Feature Engineering
      ↓
Curated / ML-Ready Data
```

The initial implementation focuses on **NIFTY 50 OHLC data using the Angel One Smart API**.

The architecture is intentionally designed to support multiple instruments, data providers, exchanges, asset classes, and timeframes in the future.

---

# 🎯 Project Goals

The primary goals are to build a reusable and scalable financial market data pipeline that provides:

* Reliable market-data ingestion
* Strong data-quality validation
* Clean and standardized OHLC/market data
* Reproducible data transformations
* Parquet-based analytical storage
* Feature engineering for quantitative research
* ML-ready datasets
* Backtesting-ready historical datasets
* Extensible data-provider architecture
* Cloud-ready storage architecture

---

# 🏗️ Data Pipeline Architecture

```text
                         DATA SOURCES
                              │
                ┌─────────────┴─────────────┐
                │                           │
          Angel One API              Future Providers
                │
                ▼
        ┌───────────────────┐
        │     INGESTION     │
        │                   │
        │ API Client        │
        │ Retry             │
        │ Timeout           │
        │ Rate Limiting     │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │  BRONZE / RAW     │
        │                   │
        │ Immutable Source  │
        │ Data              │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │    VALIDATION     │
        │                   │
        │ Schema            │
        │ OHLC Integrity    │
        │ Duplicates        │
        │ Timestamps        │
        │ Missing Data      │
        └─────────┬─────────┘
                  │
            ┌─────┴─────┐
            │           │
          VALID       INVALID
            │           │
            ▼           ▼
        CLEANING    QUARANTINE
            │
            ▼
        ┌───────────────────┐
        │ SILVER / CLEAN    │
        │                   │
        │ Canonical OHLC    │
        │ Standardized Data │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │  TRANSFORMATION   │
        │                   │
        │ Returns           │
        │ Aggregations      │
        │ Rolling Metrics   │
        │ Derived Data      │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │ FEATURE ENGINEER. │
        │                   │
        │ Price Features    │
        │ Trend Features    │
        │ Momentum          │
        │ Volatility        │
        │ Volume            │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │ GOLD / CURATED    │
        │                   │
        │ Research Ready    │
        │ ML Ready          │
        └─────────┬─────────┘
                  │
          ┌───────┼────────┐
          ▼       ▼        ▼
     Backtesting   ML   Analytics
```

---

# 🥉 Bronze → 🥈 Silver → 🥇 Gold

The pipeline follows a layered data architecture.

## 🥉 Bronze — Raw Market Data

The Bronze layer preserves source data with minimal processing.

### Purpose

* Preserve original source data
* Maintain data lineage
* Enable pipeline reprocessing
* Support debugging
* Preserve source-level information

```text
Angel One API
      ↓
Raw Response
      ↓
Bronze Parquet
```

---

## 🥈 Silver — Clean & Standardized Market Data

The Silver layer contains validated, cleaned, normalized, and standardized market data.

### Purpose

* Consistent schema
* Valid OHLC records
* Duplicate-free data
* Correct timestamps
* Standardized instruments
* Research-ready market data

```text
Bronze
  ↓
Validation
  ↓
Cleaning
  ↓
Normalization
  ↓
Silver
```

---

## 🥇 Gold — Curated & Feature-Engineered Data

The Gold layer contains transformed and feature-engineered datasets.

### Purpose

* Quantitative research
* Machine learning
* Backtesting
* Analytics
* Strategy research

```text
Silver
   ↓
Transformation
   ↓
Feature Engineering
   ↓
Gold
```

---

# 📊 Current Data Source

### Angel One Smart API

Current implementation:

```text
Provider:      Angel One Smart API
Instrument:    NIFTY 50
Data Type:     OHLC / Market Data
Language:      Python
Storage:       Parquet
Processing:    Pandas / PyArrow
```

The provider layer is designed to be replaceable so that future data sources can be added without rewriting the core pipeline.

### Planned Data Sources

* [ ] Additional market-data providers
* [ ] NSE data sources
* [ ] Commodity market data
* [ ] Global market data
* [ ] Economic data
* [ ] News / event data

---

# 📈 Supported Instruments

### Current

* [x] NIFTY 50

### Planned

* [ ] BANK NIFTY
* [ ] NIFTY stocks
* [ ] Other NSE instruments
* [ ] Commodities
* [ ] Global indices
* [ ] Futures
* [ ] Options
* [ ] Multiple asset classes

The pipeline is designed around an **instrument abstraction** rather than NIFTY-specific logic.

---

# 🛠️ Technology Stack

| Category              | Technology                   |
| --------------------- | ---------------------------- |
| Programming Language  | Python                       |
| Data Processing       | Pandas                       |
| Columnar Processing   | PyArrow                      |
| Storage Format        | Apache Parquet               |
| Current Data Provider | Angel One Smart API          |
| Testing               | pytest                       |
| Configuration         | YAML / Environment Variables |
| Version Control       | Git / GitHub                 |
| Future Cloud Storage  | AWS S3                       |
| Future Metadata Store | PostgreSQL                   |

---

# 📋 Development Roadmap

## 1. Project Foundation

* [x] Define project scope
* [x] Define general-purpose pipeline architecture
* [x] Define Bronze / Silver / Gold architecture
* [x] Select Python
* [x] Select Parquet
* [x] Select initial data provider
* [x] Select NIFTY 50 as initial instrument
* [ ] Create Python package structure
* [ ] Configuration management
* [ ] Environment configuration
* [ ] Structured logging
* [ ] Documentation

---

# 2. Data Source & Provider Layer

* [x] Define provider abstraction
* [ ] Implement Angel One authentication
* [ ] Implement OHLC API client
* [ ] API response parsing
* [ ] Request timeout handling
* [ ] Retry mechanism
* [ ] Exponential backoff
* [ ] Rate-limit handling
* [ ] API error handling
* [ ] Provider-specific normalization
* [ ] Provider health checks
* [ ] Multiple-provider support

---

# 3. Data Ingestion

* [ ] Historical data ingestion
* [ ] Incremental ingestion
* [ ] Date-range ingestion
* [ ] Instrument-based ingestion
* [ ] Timeframe-based ingestion
* [ ] Backfill support
* [ ] Idempotent ingestion
* [ ] Duplicate-safe ingestion
* [ ] Ingestion metadata
* [ ] Pipeline run ID
* [ ] Ingestion statistics
* [ ] Data freshness tracking

---

# 4. Bronze / Raw Data Layer

* [ ] Define raw schema
* [ ] Store source data
* [ ] Store ingestion timestamp
* [ ] Store provider information
* [ ] Store pipeline run ID
* [ ] Store raw data as Parquet
* [ ] Implement partitioning
* [ ] Preserve immutable source data
* [ ] Implement data lineage

---

# 5. Data Validation

## Schema Validation

* [ ] Required-column validation
* [ ] Datatype validation
* [ ] Column-name validation
* [ ] Null-value validation
* [ ] Schema versioning

## OHLC Validation

* [ ] `High >= Open`
* [ ] `High >= Close`
* [ ] `Low <= Open`
* [ ] `Low <= Close`
* [ ] `High >= Low`
* [ ] Positive price validation
* [ ] Volume validation

## Time-Series Validation

* [ ] Timestamp validation
* [ ] Timezone validation
* [ ] Chronological ordering
* [ ] Duplicate timestamp detection
* [ ] Missing candle detection
* [ ] Unexpected interval detection

## Market Calendar Validation

* [ ] Trading-session validation
* [ ] Market holiday handling
* [ ] Market open/close validation
* [ ] Special-session handling

---

# 6. Data Cleaning

* [ ] Remove duplicate records
* [ ] Standardize column names
* [ ] Convert datatypes
* [ ] Normalize timestamps
* [ ] Sort time-series data
* [ ] Handle missing values
* [ ] Handle invalid records
* [ ] Normalize symbols
* [ ] Normalize exchange identifiers
* [ ] Create canonical market-data schema

---

# 7. Quarantine Layer

Invalid data should be isolated rather than silently discarded.

* [ ] Create quarantine storage
* [ ] Store rejected records
* [ ] Store rejection reason
* [ ] Store validation failure
* [ ] Track rejected record count
* [ ] Generate quarantine report

Example:

```text
Invalid Record
      ↓
Validation Failure
      ↓
Quarantine
      ↓
Reason: INVALID_OHLC
```

---

# 8. Silver / Clean Data Layer

* [ ] Define canonical OHLC schema
* [ ] Store cleaned market data
* [ ] Standardize timestamps
* [ ] Store instrument metadata
* [ ] Store timeframe metadata
* [ ] Partition Parquet datasets
* [ ] Implement incremental updates
* [ ] Implement dataset versioning

### Canonical OHLC Schema

```text
timestamp
instrument_id
symbol
exchange
timeframe
open
high
low
close
volume
source
ingested_at
```

---

# 9. Data Transformation

* [ ] Calculate price returns
* [ ] Calculate log returns
* [ ] Calculate price range
* [ ] Calculate percentage changes
* [ ] Resample timeframes
* [ ] Aggregate OHLC data
* [ ] Calculate rolling statistics
* [ ] Calculate volatility metrics
* [ ] Create derived market metrics

---

# 10. Feature Engineering

Feature engineering converts clean market data into variables suitable for quantitative research and machine learning.

## Price Features

* [ ] Returns
* [ ] Log returns
* [ ] Price change
* [ ] Percentage change
* [ ] Candle body
* [ ] Upper wick
* [ ] Lower wick
* [ ] Candle range

## Trend Features

* [ ] SMA
* [ ] EMA
* [ ] Moving averages
* [ ] Trend indicators

## Momentum Features

* [ ] RSI
* [ ] MACD
* [ ] Momentum
* [ ] Rate of Change

## Volatility Features

* [ ] Rolling standard deviation
* [ ] ATR
* [ ] Historical volatility
* [ ] Rolling range

## Volume Features

* [ ] Volume change
* [ ] Rolling volume
* [ ] Volume ratio
* [ ] Volume-based indicators

## Future Features

* [ ] Market regime features
* [ ] Cross-sectional features
* [ ] Multi-instrument features
* [ ] Economic features
* [ ] News-derived features

---

# 11. Label Generation

Labels are kept separate from features to reduce the risk of data leakage.

* [ ] Define prediction targets
* [ ] Future-return labels
* [ ] Classification targets
* [ ] Regression targets
* [ ] Multi-horizon targets
* [ ] Feature/label alignment
* [ ] Look-ahead-bias checks

Example:

```text
Features at T
      ↓
Prediction
      ↓
Target at T + N
```

---

# 12. Data Quality & Observability

* [ ] Row-count validation
* [ ] Duplicate validation
* [ ] Missing-data validation
* [ ] OHLC integrity validation
* [ ] Timestamp validation
* [ ] Completeness checks
* [ ] Data freshness checks
* [ ] Source consistency checks
* [ ] Data-quality score
* [ ] Data-quality reports
* [ ] Structured logging
* [ ] Pipeline execution metrics
* [ ] Error tracking

Example pipeline report:

```text
Records Received : 18,720
Valid Records    : 18,710
Rejected Records : 10
Duplicates       : 0
Missing Candles  : 2
Pipeline Status  : WARNING
```

---

# 13. Storage

## Current

* [x] Parquet
* [ ] Local filesystem data lake
* [ ] Partitioned Parquet datasets

## Planned

* [ ] AWS S3
* [ ] S3 Bronze layer
* [ ] S3 Silver layer
* [ ] S3 Gold layer
* [ ] PostgreSQL metadata store
* [ ] Dataset versioning
* [ ] Data catalog

---

# 14. PostgreSQL Metadata Layer

PostgreSQL is planned primarily for metadata and pipeline management rather than storing the entire historical market-data dataset.

* [ ] Instrument metadata
* [ ] Exchange metadata
* [ ] Data-source metadata
* [ ] Pipeline runs
* [ ] Ingestion jobs
* [ ] Data-quality results
* [ ] Dataset metadata
* [ ] Feature metadata

---

# 15. Pipeline Orchestration

* [ ] Pipeline runner
* [ ] Full pipeline execution
* [ ] Individual pipeline stages
* [ ] Pipeline configuration
* [ ] Pipeline run tracking
* [ ] Failure handling
* [ ] Pipeline retries
* [ ] Pipeline status reporting

Target:

```bash
python scripts/run_pipeline.py
```

Expected flow:

```text
Ingestion
    ↓
Bronze
    ↓
Validation
    ↓
Cleaning
    ↓
Silver
    ↓
Transformation
    ↓
Feature Engineering
    ↓
Quality Checks
    ↓
Gold
```

---

# 16. Testing

* [ ] Unit tests
* [ ] Ingestion tests
* [ ] Validation tests
* [ ] Cleaning tests
* [ ] Transformation tests
* [ ] Feature tests
* [ ] Storage tests
* [ ] Integration tests
* [ ] End-to-end pipeline test
* [ ] Edge-case testing

---

# 17. AWS Cloud Architecture

Future architecture:

```text
Data Provider
      ↓
Python Data Pipeline
      ↓
AWS S3
      ↓
Parquet Data Lake
      ↓
Analytics / ML / Backtesting
```

Planned:

* [ ] AWS S3 integration
* [ ] S3 Bronze layer
* [ ] S3 Silver layer
* [ ] S3 Gold layer
* [ ] IAM configuration
* [ ] Cloud-based configuration
* [ ] Cloud logging
* [ ] Scheduled execution
* [ ] Cloud monitoring

---

# 18. Machine Learning Data Pipeline

Future ML workflow:

```text
Market Data
     ↓
Clean Data
     ↓
Feature Engineering
     ↓
Feature Dataset
     ↓
Label Generation
     ↓
Time-Series Split
     ↓
ML Model
```

Planned:

* [ ] ML feature dataset generation
* [ ] Target generation
* [ ] Time-series train/validation/test splitting
* [ ] Data-leakage prevention
* [ ] Feature versioning
* [ ] Dataset versioning
* [ ] ML-ready Parquet datasets

---

# 19. Backtesting Integration

Future architecture:

```text
Gold Dataset
      ↓
Historical Data Loader
      ↓
Backtesting Engine
      ↓
Trading Strategy
      ↓
Performance Analysis
```

Planned:

* [ ] Historical dataset interface
* [ ] Strategy data interface
* [ ] Time-series data loader
* [ ] Transaction-cost support
* [ ] Slippage support
* [ ] Performance metrics
* [ ] Backtesting reports

---

# 📁 Planned Project Structure

```text
quant-data-pipeline-engine/
│
├── README.md
├── pyproject.toml
├── .env.example
├── .gitignore
│
├── config/
│   ├── settings.yaml
│   └── instruments.yaml
│
├── src/
│   └── quant_data_pipeline/
│       │
│       ├── ingestion/
│       │   ├── base.py
│       │   └── angel_one.py
│       │
│       ├── validation/
│       │   ├── schema.py
│       │   ├── ohlc.py
│       │   └── quality.py
│       │
│       ├── cleaning/
│       │   └── market_data.py
│       │
│       ├── transformation/
│       │   ├── returns.py
│       │   └── aggregation.py
│       │
│       ├── features/
│       │   ├── technical.py
│       │   ├── volatility.py
│       │   └── volume.py
│       │
│       ├── storage/
│       │   ├── parquet.py
│       │   └── s3.py
│       │
│       ├── pipeline/
│       │   └── runner.py
│       │
│       └── utils/
│           ├── logging.py
│           └── time.py
│
├── tests/
├── scripts/
├── notebooks/
│
└── data/
    ├── bronze/
    ├── silver/
    ├── gold/
    └── quarantine/
```

---

# 🔐 Security

Never commit credentials or secrets to GitHub.

Use environment variables for sensitive configuration:

```text
ANGEL_ONE_API_KEY=
ANGEL_ONE_CLIENT_ID=
ANGEL_ONE_PASSWORD=
ANGEL_ONE_TOTP=
```

Commit only:

```text
.env.example
```

Never commit:

```text
.env
```

or production credentials.

---

# ⚠️ Market Data Disclaimer

This project provides financial data pipeline software and does not provide investment advice.

Market data obtained through third-party providers may be subject to provider, exchange, licensing, and redistribution restrictions.

Users are responsible for complying with the applicable terms and conditions of their chosen data providers.

Third-party market data should not be assumed to be freely redistributable under this project's source-code terms.

---

# 📌 Project Status

**Status: 🚧 Active Development**

### Current Implementation

```text
Angel One Smart API
        ↓
NIFTY 50
        ↓
OHLC Data
        ↓
Python
        ↓
Validation
        ↓
Cleaning
        ↓
Parquet Storage
```

### Current Focus

The initial development phase focuses on building a reliable and reusable **NIFTY 50 market-data pipeline** while keeping the architecture general enough to support multiple financial instruments and data providers.

---

# 🗺️ Development Milestones

## Phase 1 — Foundation

* [x] Project scope
* [x] Repository setup
* [x] Pipeline architecture
* [x] Bronze / Silver / Gold design
* [x] Python selected
* [x] Parquet selected
* [x] Angel One selected as initial provider
* [x] NIFTY 50 selected as initial instrument
* [ ] Package structure
* [ ] Configuration system

## Phase 2 — Core Data Pipeline

* [ ] Angel One ingestion
* [ ] Bronze/raw storage
* [ ] Data validation
* [ ] Data cleaning
* [ ] Quarantine layer
* [ ] Silver dataset
* [ ] Data-quality checks

## Phase 3 — Transformation & Features

* [ ] Data transformations
* [ ] Returns
* [ ] Rolling statistics
* [ ] Technical indicators
* [ ] Volatility features
* [ ] Volume features
* [ ] ML feature dataset

## Phase 4 — Production Improvements

* [ ] Incremental ingestion
* [ ] Backfill support
* [ ] Idempotency
* [ ] Structured logging
* [ ] Automated testing
* [ ] Monitoring
* [ ] Pipeline orchestration

## Phase 5 — Cloud

* [ ] AWS S3
* [ ] S3 data lake
* [ ] PostgreSQL metadata
* [ ] Scheduled pipeline execution
* [ ] Cloud monitoring

## Phase 6 — Quant & ML

* [ ] Backtesting integration
* [ ] ML dataset generation
* [ ] Time-series validation
* [ ] Feature versioning
* [ ] Label generation
* [ ] Model-ready datasets

---

# 📚 Key Concepts Covered

This project is designed around practical implementation of:

**Python · Pandas · PyArrow · Apache Parquet · Data Engineering · Financial Data · Market Data · OHLC · OHLCV · Time-Series Data · Data Validation · Data Cleaning · Data Transformation · Feature Engineering · Quantitative Finance · Algorithmic Trading · Backtesting · Machine Learning · AWS S3 · Data Lake Architecture**

---

# 🎓 Learning Objectives

This project is being developed as a practical engineering project to strengthen knowledge of:

* Python
* Pandas
* Time-series data processing
* Financial market data
* Data engineering
* Data validation
* Data cleaning
* Data transformation
* Parquet data storage
* Feature engineering
* Quantitative research
* Machine learning data preparation
* Cloud data architecture
* Production software engineering

---

# 🚀 Long-Term Vision

The long-term goal is to evolve the project from a NIFTY 50 market-data pipeline into a reusable financial data platform.

```text
                    Financial Data Platform
                              │
             ┌────────────────┼────────────────┐
             │                │                │
         Market Data     Economic Data     News Data
             │                │                │
             └────────────────┼────────────────┘
                              │
                       Data Pipeline
                              │
                 ┌────────────┴────────────┐
                 │                         │
            Quant Research               ML
                 │                         │
            Backtesting              Prediction
                 │                         │
                 └────────────┬────────────┘
                              │
                       Trading Systems
```

---

# 👨‍💻 Author

**Hemang Dave**

Building practical systems at the intersection of:

**Software Engineering × Financial Data × Quantitative Research × AI/ML**

---

## ⭐ Project Progress

The checklist above is intentionally maintained as a living roadmap.

As new components are implemented, completed tasks will be marked with:

```text
- [x]
```

and remaining tasks with:

```text
- [ ]
```

The roadmap will evolve as the architecture expands from a NIFTY 50 data pipeline toward a generalized quantitative financial data platform.
