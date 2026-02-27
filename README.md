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

* **Tool:** [nr-fetch-entities](https://github.com/JimHagan/nr-fetch-entities)
* **Purpose:** Programmatically extract a complete inventory of entities, including detailed tag information and metadata that is often difficult to export in bulk via the UI.
* **Best Used For:** Governance audits, ensuring tagging compliance (e.g., `Environment`, `Owner`, `Team`), and preparing data for external CMDB synchronization.

> **Pro Tip:** This CLI is a great companion to the [New Relic Entity Explorer](https://docs.newrelic.com/docs/new-relic-solutions/new-relic-one/core-concepts/new-relic-explorer-view-performance-across-apps-services-hosts/), providing the raw data needed for custom reporting that the UI cannot export.

### Useful AI Prompts
Copy and paste this prompt into an LLM (like ChatGPT, Claude, or Gemini) along with your tool output:
> "Please review the `entities_[accountid].txt` file and generate a breakdown of the counts of various entity types. In addition, use tags and metadata to find the most common tagging schema. Identify inconsistencies in naming and also evaluate the completeness of critical tags. For example, if there is a 'team' tag, give me a statistical breakdown of its overall completeness by entity. In addition, for entity types with 'nr.slo*' attributes, give me an overall compliance rate and identify any recommendations for improvements in the naming and configuration of those."

---


## 2. Alert Analyzer

A mature observability practice is defined by high-signal, low-noise alerting. The Alert Quality tools help identify redundant conditions and optimization opportunities.

* **Tool:** [nr-alert-analyzer](https://github.com/JimHagan/nr-alert-analyzer)
* **Purpose:** Analyzes existing alert conditions to identify redundancies, inefficiencies, and "noisy" configurations that lead to alert fatigue.
* **Best Used For:** Alert rationalization projects and improving the Signal-to-Noise Ratio (SNR) of your monitoring.

> **Companion Resources:** Use this tool alongside the [Alert Quality Management Dashboard](https://onenr.io/0MR29lo7pwY) and the [AQM App](https://onenr.io/02wdylpboRE) to drive a data-driven approach to incident management.

### Useful AI Prompts
Copy and paste this prompt into an LLM along with your tool output:
> "Evaluate the `incident_summary.txt` files and provide some insights as to the overall 'flappiness' of these alerts. Indicate where there are opportunities for naming improvements and identify scenarios where the same general condition is present in multiple policies. Also, looking at the 'Incidents By Day' section, give me a sense if there are any temporal patterns by days in this sample. Finally, evaluate the 'RELATED ENTITY ANALYSIS' section to see if there are any unusual patterns by entity."

---

## 3. Telemetry Ingest Analysis

Managing data at scale requires visibility into attribute diversity and ingest volume. This two-part solution helps you sample raw data and perform deep cardinality analysis.

### Telemetry Sample Extractor UI
* **Source:** [nr-telemetry-sample-extractor](https://github.com/JimHagan/nr-telemetry-sample-extractor)
* **Capabilities:** A visual interface to setup a sample extraction porcess for analysis.  It was created with Logs in mind, but can work with other MELT types. It is particularly effective for high-diversity log data where you need a representative raw sample.
* **Export:** Supports JSON and CSV formats for downstream processing.

### Telemetry Attribute Analyzer (CLI)
* **Source:** [nr-telemetry-analyzer](https://github.com/JimHagan/nr-telemetry-analyzer)
* **Capabilities:** A high-performance CLI program that processes CSV/JSON telemetry data to output summaries of:
    * **Attribute Cardinality:** Identify "high-cardinality" attributes that impact costs and performance.
    * **Data Volume:** Pinpoint exactly which attributes or services are driving ingest.
    * **Anomaly Analysis:** Detect unexpected spikes or patterns in data structure.

> **Companion Resources:** These tools provide the "why" behind the "what" found in the [Data Ingest Baseline Dashboard](https://onenr.io/0BQ19gmVlQx) and the [Data Ingest Breakdown Dashboard](https://onenr.io/0gR79Xl70Qo).

### Useful AI Prompts
Copy and paste this prompt into an LLM along with your `output.MD` file:
> "As an expert-level Site Reliability Engineer (SRE) and FinOps (Cloud Cost) analyst, your job is to analyze a statistical summary from a log sample and provide a natural language summary. First, describe the infrastructure and application stack you can infer from the attributes. Second, identify specific, actionable anomalies related to cost, performance, or security. Cite the log evidence (e.g., messages, attributes) from the summary in your analysis. Format your response in clean markdown."

---

## Getting Started

Because the **New Relic Data Toolkit** is a loosely coupled suite, you can implement the tools individually based on your current needs. 

1.  **Clone the relevant repository** from the links above.
2.  **Review the local README** in each repo for specific installation requirements (e.g., Python, Node.js, or Docker) and authentication steps.
3.  **Configure your New Relic API Keys** (usually requires a User API Key or Ingest Key depending on the tool).

## Disclaimer

This toolkit was created as a personal research project to aid in undertanding of the structure of New Relic telemetry.  It should not be used in a production environments.  All tools are readonly and should only be used for research purposes on your own New Relic account.  This toolkit is not a New Relic product.
