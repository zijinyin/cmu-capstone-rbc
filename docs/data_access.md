# Data Access & NDA Notes (Sponsor Confidential)

## Important
This repository does **NOT** contain sponsor-provided raw data, intermediate merged data, or any row-level extracts.
Do not upload confidential RBC sponsor data to GitHub unless:
1) Sponsor explicitly permits, AND
2) The repository is private, AND
3) Your program’s NDA rules allow it.

## What is NOT in this repo
Examples of restricted files (do not commit):
- Raw CSVs (e.g., BroadridgeAccount.csv, Party.csv, CALAccount.csv, HA*.csv)
- Any Parquet outputs (e.g., Broadridge_Core_All.parquet, Identity_All.parquet, Wide_All.parquet)
- Any table containing PartyId / FinancialAccountId at row level
- Any exports containing client/advisor interaction content

## What IS allowed in this repo
- Notebooks and source code (with no embedded sensitive outputs)
- Documentation (methodology, data dictionary, poster/report text)
- NDA-safe aggregated outputs (counts, means, cluster summaries) with no IDs
- NDA-safe plots (no raw records, no identifiable values)

## Local data placement (recommended)
Store data outside the repo, for example:
- `../rbc_data/raw/`          (sponsor raw CSVs, restricted)
- `../rbc_data/intermediate/` (intermediate Parquet, restricted)
- `../rbc_data/outputs/`      (merged / wide Parquet, restricted)

Notebooks should be configured to read from `../rbc_data/...` paths.

## S3 data placement (optional, for AWS workflow)
If using S3, recommended prefixes:
- `s3://<bucket>/raw/`
- `s3://<bucket>/intermediate/`
- `s3://<bucket>/outputs/`

If you see AccessDenied errors when reading S3 objects, confirm:
- Your notebook execution role has `s3:ListBucket` + `s3:GetObject` on the prefix
- Bucket policy does not explicitly deny access

## Output policy
Only export NDA-safe outputs into this repo:
- `results/figures/*.png` (aggregated visuals)
- `results/sample_outputs/*.csv` (aggregated summaries only; no IDs)

## Requesting data access
Access to sponsor data should be requested via the sponsor / program channels.
(Insert sponsor contact / internal process here.)