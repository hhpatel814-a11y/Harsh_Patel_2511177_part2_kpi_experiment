# Part 2: KPI Framework, Business Experiment Analysis & Decision Recommendation

**Student:** Harsh Patel  
**Repository:** `harshpatel_studentid_part2_kpi_experiment`  
**Course:** Business Analytics with Generative & Agentic AI  

---

## Business Context

A subscription-based digital product company ran a controlled experiment to evaluate whether a redesigned onboarding and activation campaign improves user conversion. Users were randomly assigned to either the **Control group** (legacy onboarding) or the **Treatment group** (new campaign experience). Leadership requires a data-backed decision on whether to scale the Treatment to all users.

---

## Dataset Description

| Attribute | Detail |
|---|---|
| File | `data/campaign_experiment_data.xlsx` |
| Records (raw) | 1,408 rows |
| Columns | 16 |
| Time Period | January – May 2025 |

**Key Columns:**

| Column | Type | Description |
|---|---|---|
| user_id | String | Unique user identifier |
| signup_date | Date | Date of user registration |
| experiment_group | Categorical | Control or Treatment |
| region | Categorical | Geographic region |
| device_type | Categorical | Mobile, Desktop, Tablet |
| traffic_source | Categorical | Organic, Paid, Direct, Referral |
| plan_type | Categorical | Basic, Pro, Premium |
| visited_landing_page | Binary (0/1) | Whether user visited landing page |
| started_trial | Binary (0/1) | Whether user started a free trial |
| completed_onboarding | Binary (0/1) | Whether user finished onboarding |
| converted_to_paid | Binary (0/1) | Whether user converted to a paid plan |
| revenue_30d | Float | Revenue generated in first 30 days (USD) |
| support_tickets_30d | Integer | Number of support tickets raised |
| refund_requested | Binary (0/1) | Whether user requested a refund |
| days_to_convert | Float | Days from signup to conversion (NaN for non-converters) |
| engagement_score | Float | Platform engagement score (0–100) |

---

## Data Quality Findings & Handling

| Check | Finding | Resolution |
|---|---|---|
| Duplicate user_id records | 8 exact duplicates found | Removed; retained first occurrence |
| Missing device_type | 18 nulls | Imputed as 'Unknown' category |
| Missing traffic_source | 24 nulls | Imputed as 'Unknown' category |
| Missing engagement_score | 14 nulls | Replaced with group-level median |
| Missing days_to_convert | 1,336 nulls | Expected (non-converters); excluded from average calculation only |
| Invalid binary values | None found | All binary columns contained only 0 and 1 |
| Revenue outliers (>99th pct) | Threshold: ~$280 | Flagged but retained; no evidence of data entry errors |
| Segment distribution balance | Reasonable across groups | Control = 693 users, Treatment = 715 users |

Full documentation is in `analysis/experiment_analysis.xlsx` → *Data_Quality_Report* sheet.

---

## North Star Metric

**Selected North Star: Paid Conversion Rate**

Paid conversion rate is the definitive measure of whether the campaign is achieving its commercial objective. It is the point in the user journey where value exchange is confirmed — the user has decided the product is worth paying for. All upstream funnel metrics (landing page visits, trial starts, onboarding completions) are necessary preconditions but not sufficient outcomes. All downstream metrics (revenue, refunds, engagement) are consequences of whether and how well conversion happened.

**Risks of blind optimization:** Aggressive conversion tactics can create low-quality conversions that refund quickly, inflate support burden, or harm engagement — hence the guardrail metrics.

---

## KPI Tree Summary

```
                    ⭐ NORTH STAR
               Paid Conversion Rate
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
  Activation       Revenue           User Experience
 Funnel Depth      Quality           & Retention
        │               │               │
   ┌────┴────┐    ┌─────┴────┐    ┌─────┴────┐
   ▼    ▼    ▼    ▼     ▼    ▼    ▼     ▼    ▼
  LP  Trial Onb  RevU RevC Ref↓  Eng  DtC↓  Tick↓
```

*(LP = Landing Page Visit Rate, Onb = Onboarding Completion Rate,*  
*RevU = Avg Revenue/User, RevC = Avg Revenue/Converter, Ref = Refund Rate,*  
*Eng = Engagement Score, DtC = Days to Convert, Tick = Support Ticket Rate)*

**Guardrail Metrics:** Refund Rate (< 5%), Support Ticket Rate (< 10%), Avg Days to Convert (no material increase)

See `outputs/kpi_tree.png` for the full visual.

---

## Experiment Analysis Approach

1. **Data ingestion & cleaning** — removed duplicates, imputed missing values, validated binary columns
2. **Group-level metric computation** — calculated all 11 required metrics for Control and Treatment
3. **Segment-level breakdowns** — Region, Device Type, Traffic Source (3 segment dimensions)
4. **Delta calculation** — absolute difference (Treatment − Control) for every metric
5. **Statistical testing** — One-tailed two-proportion Z-Test on Paid Conversion Rate

All analysis outputs are in `analysis/experiment_analysis.xlsx` and `outputs/experiment_summary.xlsx`.

---

## Hypothesis Test Summary

| Element | Value |
|---|---|
| Test type | One-tailed two-proportion Z-Test |
| Null hypothesis | Conversion rate (Treatment) ≤ Conversion rate (Control) |
| Alternate hypothesis | Conversion rate (Treatment) > Conversion rate (Control) |
| Significance level | α = 0.05 |
| Z-Statistic | 3.2640 |
| P-Value (one-tailed) | 0.0005 |
| 95% CI for lift | [+1.48pp, +6.17pp] |
| Decision | **Reject H₀** — statistically significant improvement confirmed |

Full test documentation: `analysis/hypothesis_test_notes.md`

---

## Guardrail Metrics Considered

| Guardrail | Control | Treatment | Status |
|---|---|---|---|
| Refund Rate | 4.33% | 4.34% | ✅ Safe — below 5% threshold |
| Support Ticket Rate | 38.96% | 38.88% | ✅ Safe — no increase |
| Avg Days to Convert | 15.9 days | 14.1 days | ✅ Safe — faster, not slower |
| Avg Rev / Converted User | $125.23 | $117.83 | ⚠️ Monitor — mild decline |

---

## Final Recommendation

**Phased Launch** — Roll out the Treatment experience to Mobile users and Organic/Direct traffic segments first, then expand after 3–4 weeks of post-launch monitoring. The statistical evidence for a real conversion lift is compelling (p = 0.0005), no guardrail is breached, and the segment data suggests the strongest lift is concentrated in mobile and organic traffic.

Full reasoning: `outputs/recommendation_memo.md`

---

## Assumptions and Limitations

- Users were assumed to be randomly and independently assigned to groups
- Missing device and traffic data were imputed conservatively; sensitivity to this assumption was not tested
- Novelty effects (short-term inflated engagement with new experiences) were not explicitly controlled
- Segment-level conclusions are directional due to smaller subsample sizes
- The analysis window is 30 days; longer-term retention effects are unknown

---

## Screenshots Included

| File | Contents |
|---|---|
| `screenshots/summary_metrics.png` | Control vs Treatment comparison table for all 11 core metrics |
| `screenshots/hypothesis_test_output.png` | Z-test result panel with all inputs, outputs, and verdict |
| `screenshots/kpi_tree_preview.png` | KPI tree visualization preview |

---

## Repository Structure

```
part2_kpi_experiment/
├── data/
│   └── campaign_experiment_data.xlsx      ← Raw experiment dataset
├── analysis/
│   ├── experiment_analysis.xlsx           ← Cleaned data + data quality report
│   └── hypothesis_test_notes.md           ← Full hypothesis test documentation
├── outputs/
│   ├── kpi_tree.png                       ← KPI tree visualization (high-res)
│   ├── experiment_summary.xlsx            ← Metric comparison + segment breakdowns
│   └── recommendation_memo.md             ← Executive decision memo
├── screenshots/
│   ├── summary_metrics.png                ← Core metrics table screenshot
│   ├── hypothesis_test_output.png         ← Hypothesis test output screenshot
│   └── kpi_tree_preview.png               ← KPI tree preview screenshot
└── README.md                              ← This file
```
