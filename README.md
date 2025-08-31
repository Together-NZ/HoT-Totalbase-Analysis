# HoT Total Base Analysis (Part 1) — README

## Overview

Part 1 (Total Base) of House of Travel’s customer analytics. The pipeline prepares a clean customer–transactions dataset, applies SPiD-style profile hygiene, engineers features, and builds value + behavioural segments for audience activation.
Part 2 (Leisure Base) will extend this with leisure-specific nuances.

## Key Files

* `hot-totabase-analysis.ipynb` — main pipeline (ingest → hygiene → features → segments → exports).
* `docs/HoT_TotalBase_Handover_Documentation_Part1.docx` — detailed handover (logic, rules, nuances).

## Data Inputs (examples)

* **GCS bucket:** `hot-together-dropbox`
* **Customer extracts:** `HOT_SFMC_Customer_Incremental_YYYY-MM-DD.csv` (pipe-delimited, `latin1`)
* **Transactional extracts:** `HOT_SFMC_Transactional_Incremental_*.csv` (pipe-delimited, `latin1`)

## Prerequisites

* Python **3.10+**
* Packages: `pandas`, `numpy`, `google-cloud-storage` *(optional for docs: `python-docx`)*
* GCP access: **Application Default Credentials (ADC)** with read access to the GCS bucket

```bash
# Authenticate if needed
gcloud auth application-default login
```

## Quick Start

1. Clone the repo and open in VS Code/Jupyter.
2. Set GCP credentials (ADC) and verify access to the GCS bucket.
3. Update input file names/paths in the script if newer extracts are available.
4. Run the pipeline:

   ```bash
   python hot-totabase-analysis.ipynb
   ```
5. Review outputs (default path in script: `./downloads/hot-segments-total-base` — update for your environment).

## Outputs

* Merged & cleaned customer–transactions dataset with engineered features.
* Customer value tiers: **HVC** (top 20%), **MVC** (next 30%), **LVC** (bottom 50%).
* Behavioural/life-stage segments: Air Only, Luxury Seeker, Yolo Solo, Young Explorer, Younger/Older Family, Sinks & Dinks, Empty Nester.
* Per-segment indexing workbooks (XLSX/CSV) for Sales/CRM.

## Notes

* Exclude **corporate/SME** travellers from leisure segments: `LinkedToCompany == 1`.
* SPiD hygiene (dedupe/merge priorities) and vendor lists are summarised in the handover doc.
