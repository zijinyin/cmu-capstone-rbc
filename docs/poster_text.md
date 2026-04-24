# Poster Text (Final)

## ABSTRACT — Objective
This capstone project aims to identify and understand young investor personas beyond traditional demographics using behavioral and financial data, in order to enable personalized education strategies and strengthen long-term client retention for RBC Capital Markets.

## ABSTRACT — Key Focus Areas
- Segment young investors based on source of wealth (earned vs. inherited)
- Compare behavioral differences across risk tolerance, investment objectives, and time horizon
- Identify statistically significant differences between groups using data-driven analysis
- Develop investor personas that reflect financial behavior and decision-making patterns
- Quantify how these differences impact engagement and advisory strategy opportunities

## INTRODUCTION
Intergenerational wealth transfer is reshaping the advisor–client relationship. Beneficiaries and other next-gen household members are often connected to accounts through inheritance or beneficiary designations, but they may not be well understood by firms and may engage differently from primary account owners. For RBC, improving visibility into this population can help strengthen long-term advisory relationships, prioritize education initiatives, and reduce attrition risk as wealth transitions across generations.

To support this, we consolidated multiple internal datasets into an analysis-ready structure that links people, accounts, and account roles, enabling us to identify beneficiaries and their relationship to account owners. This integrated dataset with account attributes and account activity summaries provides a consistent foundation for baseline profiling, segmentation, and identifying behavioral patterns that may indicate engagement gaps and opportunities for targeted outreach.

## METHODS AND MATERIALS — Materials
This study uses proprietary investor data from RBC Capital Markets, consolidated from multiple internal sources including Broadridge Core, Broadridge Activity, account role mappings, CAL, and Identity. Analysis was conducted in Python.

## METHODS AND MATERIALS — Methods
Family relationships were mapped using relationship-to-owner fields (retaining Child and Parent signals) to isolate intergenerational transfer context. Transfer amounts were computed using a delta-change approach (last snapshot per account per year) to avoid inflating cumulative fields. Young investors were identified through a two-condition definition combining age, recency of account opening, and conservative risk profile. Behavioral segmentation used K-Prototypes clustering (k=4) on mixed numerical and categorical features.

## RESULTS (high-level)
We observed meaningful behavioral differences between earned and inherited wealth groups and identified distinct personas through clustering. Family-linked accounts show transfer-type inflows but more passive subsequent activity, motivating targeted onboarding and engagement strategies during the transfer window.

## DISCUSSION (high-level)
The data suggests a gap between independent and family-linked investors: non-family account holders show more proactive retirement behavior, while family-linked beneficiaries tend to receive transfers passively. This reinforces the need for earlier engagement, education, and structured onboarding for beneficiaries.

## CONCLUSIONS
Intergenerational wealth transfer is a retention-critical moment. Segment-specific strategies, combined with proactive onboarding and measurement, can help RBC retain next-generation relationships and reduce asset outflow risk.