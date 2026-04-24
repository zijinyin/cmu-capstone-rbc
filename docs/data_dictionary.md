# Merged Data Dictionary (NDA-safe)

This dictionary describes the merged/intermediate datasets used for analysis. These datasets are sponsor-confidential and are not stored in this repository; the purpose of this document is to clarify grain/keys and intended usage.

---

## 1) Identity_All.parquet
**What it is**  
Party profiles + relationship edges (Party × relationships).

**Typical fields**
- Party profile: PartyId, PartyType, ClientIndicator, PartyStatus, and sparse profile attributes
- Relationship edge fields: pr_RelatedPartyId, pr_Roles, etc.

**What it enables**
- Family/trust network mapping (“who is connected and how”)
- Enrichment of account analysis via party joins

**Common caveats**
- Row multiplication is expected (Party × edges)
- Roles often require standardization (multi-valued text)

---

## 2) Broadridge_Core_All.parquet
**What it is**  
Internal account backbone: BroadridgeAccount merged with BroadridgeAccountRole, optionally enriched with role party attributes.

**Grain / keys**
- Grain: one row per FinancialAccountId per role mapping (accounts can have multiple roles → multiple rows)
- Key fields: FinancialAccountId, PrimaryOwnerPartyId, bar_PartyId, bar_FinancialAccountRole

**What it enables**
- Identify who is associated with an account and in what capacity (owner/beneficiary/TOD/etc.)
- Define beneficiary-linked structures
- Main join spine to attach Identity, Activity, CAL, and external enhancements

**Common caveats**
- Role labels require mapping rules
- PrimaryOwnerPartyId ≠ role party (bar_PartyId) in general

---

## 3) Broadridge_Activity_All.parquet
**What it is**  
Account-level historical snapshot table combining ContributionHistory and DistributionHistory with a FULL OUTER JOIN on (FinancialAccountId, DeltaDate).

**Grain / keys**
- Grain: one row per (FinancialAccountId, DeltaDate)
- Key fields: FinancialAccountId, DeltaDate

**What it enables**
- Time-series/behavior proxies: inflow/outflow intensity, CYTD/PYTD-style measures
- Construction of time-window features (e.g., last 30/90/180-day totals, trends, volatility proxies)

**Common caveats**
- Many fields may be NULL depending on coverage/definitions
- Not transaction-level; snapshot-style summaries

---

## 4) CAL_All.parquet
**What it is**  
CAL (credit/lending-like) domain enhancement bridged to Broadridge accounts via an association table.

**Grain / keys**
- Grain: one row per BroadridgeFinancialAccountId ↔ CALFinancialAccountNumber mapping
- Key fields: cal_BroadridgeFinancialAccountId, cal_CALFinancialAccountNumber, cal_PrimaryOwnerPartyId

**What it enables**
- Identify which Broadridge accounts have CAL linkages
- Add liquidity/credit context (balances/limits/available credit-like fields)

**Common caveats**
- One-to-many mappings may exist; aggregate before joining wide to avoid row explosion

---

## 5) HeldAway_Long.parquet
**What it is**  
Standardized long table aligning multiple held-away external account types into a shared schema.

**Grain / keys**
- Grain: one row per held-away external account record
- Common keys: PrimaryOwnerPartyId, ExternalType, RBCHeldAccountId, FinancialAccountNumber

**What it enables**
- Coverage checks by type
- Base for building party-level aggregates

**Common caveats**
- Joining directly into wide tables can multiply rows; aggregate first

---

## 6) HeldAway_Party.parquet
**What it is**  
Party-level aggregated features derived from HeldAway_Long.

**Grain / keys**
- Grain: one row per PrimaryOwnerPartyId
- Key: PrimaryOwnerPartyId

**Example derived features**
- Counts/flags by external type (n_ha529, has_ha_retirement, etc.)
- Distinct external account counts
- Summed value proxies where available

**Common caveats**
- NULL can mean “no matched records” (coverage), not necessarily true zero

---

## 7) Yodlee_Party.parquet
**What it is**  
Party-level aggregated external account visibility based on Yodlee linkage.

**Grain / keys**
- Grain: one row per PrimaryOwnerPartyId

**Example derived features**
- External coverage counts (rows, distinct accounts)
- Aggregated external balance/value proxies
- Recency indicators

**Common caveats**
- Missing linkage can look like “no external accounts”

---

## 8) Internal_Wide_All.parquet
**What it is**  
Internal integrated wide table: Identity + Broadridge Core + Activity + CAL.

**Intended purpose**
- Exploration and feature selection across domains without rebuilding joins

**Why it becomes large**
- Multiple one-to-many joins compound:
  - account roles × party relationships × activity snapshots × CAL links

**Common caveats**
- Not recommended as a direct training dataset without setting target grain + aggregation/dedup
- Column suffixes (_2, _3) from name collisions reduce clarity unless documented

---

## 9) Wide_All.parquet
**What it is**  
Wide internal backbone enriched with external features:
- HeldAway_Party + Yodlee_Party joined via PrimaryOwnerPartyId

**Intended purpose**
- Exploration/feature selection and downstream modeling after careful dedup/aggregation