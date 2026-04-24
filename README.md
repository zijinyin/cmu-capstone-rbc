# RBC MSBA Capstone (Team 3) — Young Investor / Wealth Transfer Analytics

## Project Overview
This capstone focuses on RBC’s retention challenge during intergenerational wealth transfer. While RBC builds strong long-term relationships with high-net-worth primary account owners, those relationships may not naturally carry over to next-generation beneficiaries. Our goal is to identify and characterize beneficiary-linked / “behaviorally young” investors, segment them into actionable personas, and translate findings into targeted engagement and education strategies.

## Key Questions
1. How large is the family-linked / wealth-transfer footprint in the account base?
2. What behavioral signals differentiate family-linked vs. non-family accounts (transfer patterns, rollover vs. contribution behavior)?
3. How should we define “young investors” beyond age-only definitions?
4. Can we segment the target population into interpretable personas (mixed numeric + categorical features)?
5. What research-backed strategies and measurement approaches can RBC pilot to improve retention?

## Data (NDA / Sponsor Confidentiality)
This repository does **NOT** include any confidential sponsor raw data or merged Parquet outputs.
See `docs/data-access.md` for:
- What is shareable vs. restricted under NDA
- How to place data locally or in S3 for reproduction
- Expected input/output file paths

## Repository Contents
- `notebooks/`:
  - `10_wealth_transfer_analysis.ipynb`: wealth-transfer signals + transfer delta-change summaries
  - `20_behavioral_analysis.ipynb`: young investor definition + behavioral profiling
  - `30_strategy_analysis.ipynb`: clustering (K-Prototypes) + strategy mapping
  - `00_data_prep_stub.ipynb`: placeholder / notes for data preparation pipeline
- `docs/`:
  - `methodology.md`: end-to-end analytical approach
  - `report_summary.md`: executive summary aligned with final report
  - `poster_text.md`: poster text blocks (abstract/introduction/methods/results/conclusions)
  - `data_dictionary.md`: merged dataset dictionary (grains, keys, caveats)
  - `data-access.md`: NDA-safe data access instructions
- `results/`:
  - `figures/`: NDA-safe charts exported from notebooks (no IDs)
  - `sample_outputs/`: NDA-safe aggregated tables (no PartyId/AccountId)

## How to Run (high level)
1. Create a Python environment and install dependencies:
   - `pip install -r requirements.txt`
2. Place sponsor data (raw or intermediate) **outside** this repo, per `docs/data-access.md`.
3. Run notebooks in order:
   1) `10_wealth_transfer_analysis.ipynb`
   2) `20_behavioral_analysis.ipynb`
   3) `30_strategy_analysis.ipynb`
4. Export NDA-safe outputs to:
   - `results/figures/`
   - `results/sample_outputs/`

## Contact
Team 3 (MSBA Capstone)  
Primary contact: Noah  
(Replace with team email / names as appropriate)
