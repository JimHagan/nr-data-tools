# New Relic Data Toolkit

The **New Relic Data Toolkit** is a collection of specialized, loosely coupled tools designed to help organizations assess, optimize, and scale their observability practices. By analyzing entity metadata, alert configurations, and telemetry ingest patterns, this toolkit provides a comprehensive view of your New Relic ecosystem beyond standard out-of-the-box dashboards.

## Overview

Modern observability requires more than just collecting data; it requires high-quality metadata, efficient alerting, and optimized data ingest. This toolkit is divided into three functional areas:

1.  **[Entity & Metadata Extraction](#1-entity--metadata-extraction)** – Audit your infrastructure and services.
2.  **[Alert Quality Analysis](#2-alert-quality)** – Reduce noise and improve incident response.
3.  **[Telemetry Ingest Analysis](#3-telemetry-ingest-analysis)** – Understand data volume and attribute cardinality.

---

## 1. Entity & Metadata Extraction

Understanding exactly what is being monitored across multiple accounts is the foundation of observability maturity. This tool provides a deep dive into the tags and metadata associated with your entities.

* **Tool:** [NR Entity Fetcher](https://github.com/JimHagan/fetch_entities)
* **Purpose:** Programmatically extract a complete inventory of entities, including detailed tag information and metadata that is often difficult to export in bulk via the UI.
* **Best Used For:** Governance audits, ensuring tagging compliance (e.g., `Environment`, `Owner`, `Team`), and preparing data for external CMDB synchronization.

> **Pro Tip:** This CLI is a great companion to the [New Relic Entity Explorer](https://docs.newrelic.com/docs/new-relic-solutions/new-relic-one/core-concepts/new-relic-explorer-view-performance-across-apps-services-hosts/), providing the raw data needed for custom reporting that the UI cannot export.

---

## 2. Alert Quality

A mature observability practice is defined by high-signal, low-noise alerting. The Alert Quality tools help identify redundant conditions and optimization opportunities.

* **Tool:** [NR Alert Analyzer](https://github.com/JimHagan/nr-alert-analyzer)
* **Purpose:** Analyzes existing alert conditions to identify redundancies, inefficiencies, and "noisy" configurations that lead to alert fatigue.
* **Best Used For:** Alert rationalization projects and improving the Signal-to-Noise Ratio (SNR) of your monitoring.

> **Companion Resources:** Use this tool alongside the [Alert Quality Management Dashboard](https://onenr.io/0MR29lo7pwY) and the [AQM App](https://onenr.io/02wdylpboRE) to drive a data-driven approach to incident management.

---

## 3. Telemetry Ingest Analysis

Managing data at scale requires visibility into attribute diversity and ingest volume. This two-part solution helps you sample raw data and perform deep cardinality analysis.

### Telemetry Analyzer UI
* **Source:** [NR Telemetry Sampler UI](https://github.com/JimHagan/nr-telemetry-analyzer-UI)
* **Capabilities:** A visual interface to define sampling strategies for logs and events. It is particularly effective for high-diversity data where you need a representative raw sample without manual NRQL exporting.
* **Export:** Supports JSON and CSV formats for downstream processing.

### Telemetry Attribute Analyzer (CLI)
* **Source:** [NR Telemetry Analyzer](https://github.com/JimHagan/telemetry-attribute-analyzer)
