# Methodology (End-to-End)

## 1) Scope
We focus on intergenerational wealth transfer and retention risk by identifying family-linked / beneficiary-linked accounts and characterizing next-generation investors. The analytical goal is to move beyond an age-only definition and identify “behaviorally young” investors who are newly onboarded or still in a conservative early-stage profile.

## 2) Data sources and keys
We consolidate internal and external account views:
- Internal: Broadridge Core (account master + roles), Broadridge Activity (snapshots), CAL (credit/liquidity context), Identity (party profiles + relationship edges)
- External: held-away accounts (529 / annuity-insurance / retirement) and Yodlee aggregated accounts

Primary keys and grains:
- Party-level: PartyId / PrimaryOwnerPartyId
- Account-level: FinancialAccountId
- Time-level snapshots: DeltaDate (account × date)

## 3) Family-link / wealth-transfer signals
We map family relationships using the RelationToAccountOwner field (retaining Child and Parent designations) to identify family-linked accounts and isolate potential wealth-transfer context.

## 4) Transfer measurement (Delta-change method)
To avoid inflating cumulative activity fields, we compute transfer amounts using a delta-change approach:
- Use last snapshot per account-year
- Derive annual transfer totals and direct rollover totals
This enables year-over-year comparisons and helps detect transfer “windows” where activity concentrates.

## 5) Young investor definition (two-condition approach)
We define “young investors” using both age and behavioral onboarding signals:
- Condition 1: age under a young threshold (≈33) and account opened within the last five years
- Condition 2: age 33–65, account opened within the last five years, and Low Risk tolerance
Condition 2 captures “behaviorally young” investors who are newly established and conservative, closer to early-stage profiles than mature advisory relationships.

## 6) Segmentation (K-Prototypes, k=4)
We use K-Prototypes clustering because our feature set includes mixed numeric and categorical variables. Representative features include:
- Numeric: age, income / net worth proxies, etc. (as available)
- Categorical: risk tolerance, investment objectives, time horizon, wealth source (earned vs inherited)
We select k=4 to create interpretable personas suitable for strategy design.

## 7) Strategy translation and measurement
We translate segment findings into research-based engagement and education strategies:
- Define segment-specific messaging and onboarding paths
- Prioritize high-risk / high-value transfer accounts for outreach
- Recommend measurement (KPIs and pilot design) to validate impact and iterate