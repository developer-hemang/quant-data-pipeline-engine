# Quant Data Pipeline Engine

> A Python-based financial market data pipeline for ingesting, validating, cleaning, transforming, and storing market data for quantitative research, analytics, backtesting, and machine learning.

**Status:** 🚧 In Development

**Current Instrument:** NIFTY 50 INDEX
**Current Data Source:** Angel One Smart API
**Storage:** Apache Parquet
**Language:** Python

---

## 📌 Overview

`quant-data-pipeline-engine` is an extensible financial data pipeline project designed to convert raw market data into clean, validated, and research-ready datasets.

The initial implementation focuses on **NIFTY 50 INDEX OHLC data** using the **Angel One Smart API**.

The architecture will gradually evolve to support multiple instruments and data providers.

```text
Angel One API
      ↓
   Ingestion
      ↓
  Raw Data
      ↓
 Validation
      ↓
  Cleaning
      ↓
Transformation
      ↓
Feature Engineering
      ↓
Research / ML / Backtesting
```

---

## 🎯 Goals

* Build a reliable financial market data pipeline
* Practice real-world data engineering with Python
* Validate and clean financial time-series data
* Store market data efficiently using Parquet
* Build reusable pipeline components
* Prepare datasets for quantitative research and ML
* Gradually support multiple instruments and data providers

---

## 🛠️ Technology Stack

| Category        | Technology          |
| --------------- | ------------------- |
| Language        | Python              |
| Data Processing | Pandas              |
| Data Storage    | Apache Parquet      |
| Columnar Engine | PyArrow             |
| Data Source     | Angel One Smart API |
| Testing         | pytest              |
| Version Control | Git / GitHub        |
| Future Storage  | AWS S3              |

---

## 📋 Development Roadmap

### Project Foundation

* [x] Project scope
* [x] Initial pipeline architecture
* [x] NIFTY 50 as initial instrument
* [x] Angel One as initial data source
* [x] Python
* [x] Parquet
* [ ] Project configuration
* [ ] Logging

### Data Ingestion

* [ ] Angel One API integration
* [ ] OHLC data ingestion
* [ ] Historical data ingestion
* [ ] Error handling
* [ ] Retry mechanism
* [ ] Incremental ingestion

### Data Validation

* [ ] Schema validation
* [ ] OHLC validation
* [ ] Duplicate detection
* [ ] Timestamp validation
* [ ] Missing-data checks

### Data Cleaning

* [ ] Remove duplicates
* [ ] Standardize columns
* [ ] Normalize timestamps
* [ ] Handle missing data
* [ ] Canonical OHLC schema

### Data Transformation

* [ ] Returns
* [ ] Log returns
* [ ] Rolling statistics
* [ ] Resampling
* [ ] Volatility metrics

### Feature Engineering

* [ ] Price features
* [ ] Trend features
* [ ] Momentum features
* [ ] Volatility features
* [ ] Volume features

### Testing & Quality

* [ ] Unit tests
* [ ] Data-quality checks
* [ ] Integration tests
* [ ] End-to-end pipeline test

### Future

* [ ] Multiple instruments
* [ ] Multiple data providers
* [ ] AWS S3
* [ ] Data-quality monitoring
* [ ] ML-ready datasets
* [ ] Backtesting integration

---

## 📁 Current Project Structure

```text
quant-data-pipeline-engine/
│
├── README.md
├── pyproject.toml
├── .gitignore
├── .env.example
│
├── src/
│   └── quant_data_pipeline/
│       └── ingestion/
│
├── tests/
│
└── data/
    └── bronze/
```

> The project structure will evolve as new pipeline stages are implemented.

---

## 🔐 Security

Never commit API credentials or secrets to GitHub.

Use environment variables for sensitive configuration.

```text
.env.example  → commit
.env          → do not commit
```

---

## ⚠️ Disclaimer

This project is intended for financial data engineering, research, and educational purposes.

Market data from third-party providers may be subject to their respective terms, licensing, and redistribution restrictions.

This project does not provide investment advice.

---

## 📈 Project Status

**🚧 Active Development**

The project is being developed incrementally, starting with NIFTY 50 market-data ingestion and gradually expanding into a generalized quantitative financial data pipeline.

---

## 👨‍💻 Author

**Hemang Dave**

**Software Engineering × Financial Data × Quantitative Research × AI/ML**
