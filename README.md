{\rtf1\ansi\ansicpg1252\cocoartf2868
\cocoatextscaling0\cocoaplatform0{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww11520\viewh8400\viewkind0
\pard\tx720\tx1440\tx2160\tx2880\tx3600\tx4320\tx5040\tx5760\tx6480\tx7200\tx7920\tx8640\pardirnatural\partightenfactor0

\f0\fs24 \cf0 # RBC MSBA Capstone (Team 3) \'97 Young Investor / Wealth Transfer Analytics\
\
## Project Overview\
This capstone focuses on RBC\'92s retention challenge during intergenerational wealth transfer. While RBC builds strong long-term relationships with high-net-worth primary account owners, those relationships may not naturally carry over to next-generation beneficiaries. Our goal is to identify and characterize beneficiary-linked / \'93behaviorally young\'94 investors, segment them into actionable personas, and translate findings into targeted engagement and education strategies.\
\
## Key Questions\
1. How large is the family-linked / wealth-transfer footprint in the account base?\
2. What behavioral signals differentiate family-linked vs. non-family accounts (transfer patterns, rollover vs. contribution behavior)?\
3. How should we define \'93young investors\'94 beyond age-only definitions?\
4. Can we segment the target population into interpretable personas (mixed numeric + categorical features)?\
5. What research-backed strategies and measurement approaches can RBC pilot to improve retention?\
\
## Data (NDA / Sponsor Confidentiality)\
This repository does **NOT** include any confidential sponsor raw data or merged Parquet outputs.\
See `docs/data-access.md` for:\
- What is shareable vs. restricted under NDA\
- How to place data locally or in S3 for reproduction\
- Expected input/output file paths\
\
## Repository Contents\
- `notebooks/`:\
  - `10_wealth_transfer_analysis.ipynb`: wealth-transfer signals + transfer delta-change summaries\
  - `20_behavioral_analysis.ipynb`: young investor definition + behavioral profiling\
  - `30_strategy_analysis.ipynb`: clustering (K-Prototypes) + strategy mapping\
  - `00_data_prep_stub.ipynb`: placeholder / notes for data preparation pipeline\
- `docs/`:\
  - `methodology.md`: end-to-end analytical approach\
  - `report_summary.md`: executive summary aligned with final report\
  - `poster_text.md`: poster text blocks (abstract/introduction/methods/results/conclusions)\
  - `data_dictionary.md`: merged dataset dictionary (grains, keys, caveats)\
  - `data-access.md`: NDA-safe data access instructions\
- `results/`:\
  - `figures/`: NDA-safe charts exported from notebooks (no IDs)\
  - `sample_outputs/`: NDA-safe aggregated tables (no PartyId/AccountId)\
\
## How to Run (high level)\
1. Create a Python environment and install dependencies:\
   - `pip install -r requirements.txt`\
2. Place sponsor data (raw or intermediate) **outside** this repo, per `docs/data-access.md`.\
3. Run notebooks in order:\
   1) `10_wealth_transfer_analysis.ipynb`\
   2) `20_behavioral_analysis.ipynb`\
   3) `30_strategy_analysis.ipynb`\
4. Export NDA-safe outputs to:\
   - `results/figures/`\
   - `results/sample_outputs/`\
\
## Contact\
Team 3 (MSBA Capstone)  \
Primary contact: Noah  \
(Replace with team email / names as appropriate)}