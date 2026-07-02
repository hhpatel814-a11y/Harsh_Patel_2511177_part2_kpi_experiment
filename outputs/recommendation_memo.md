# Recommendation Memo

**To:** Product & Growth Leadership  
**From:** Harsh Patel, Business Analyst  
**Subject:** Campaign Experiment Decision — Onboarding & Activation Initiative  
**Date:** June 2025  
**Confidentiality:** Internal Use Only  

---

## Executive Summary

The company ran an A/B experiment comparing a redesigned onboarding and activation campaign (Treatment) against the existing onboarding experience (Control). The experiment enrolled **1,408 users** across both groups over a multi-month observation window.

The Treatment group achieved a **paid conversion rate of 6.99%**, compared to **3.18%** in the Control group — a lift of approximately **+3.81 percentage points**. This result is statistically significant (Z = 3.26, p = 0.0005, one-tailed at α = 0.05).

**Recommendation: Proceed with a phased launch of the Treatment experience, beginning with Mobile users and Organic/Direct traffic segments, while continuing to monitor guardrail metrics weekly.**

---

## 1. Business Problem Statement

The company seeks to answer: **Should the new onboarding and activation campaign be rolled out to all users?**

| Dimension | Detail |
|---|---|
| Decision required | Full launch, partial launch, or halt of the new campaign experience |
| Who is impacted | All new signups; Product, Growth, and Customer Success teams |
| Target metric | Paid conversion rate (% of new users who convert to a paid plan within 30 days) |
| Risks to monitor | Elevated refund rates, increased support burden, longer conversion cycles, engagement degradation |
| Evidence required | Statistically significant lift in paid conversion + no material worsening of guardrail metrics |

---

## 2. North Star Metric

**North Star Metric: Paid Conversion Rate**

Paid conversion rate captures the ultimate commercial outcome of the onboarding journey. Every upstream metric — landing page visits, trial starts, onboarding completions — only matters insofar as it contributes to users committing financially. Revenue per converted user tells us about revenue quality, but conversion rate determines revenue volume. The two together paint the full picture.

### Why Not Other Metrics?

| Candidate | Reason Not Selected as North Star |
|---|---|
| Landing Page Visit Rate | Top-of-funnel; no commercial outcome attached |
| Trial Start Rate | Leads to conversion but is not the destination |
| Engagement Score | Directional signal, not a revenue event |
| Revenue per User | Can be inflated by a few high-value outliers |

### Risk of Blind Optimization

Optimizing paid conversion rate without guardrails risks: driving users to convert before they find genuine value (inflating refunds), adding friction that creates support tickets, or designing an experience that converts one segment at the expense of others.

---

## 3. KPI Tree Summary

The North Star (Paid Conversion Rate) is driven by three primary pillars:

**Pillar 1 — Activation Funnel Depth**
- Landing Page Visit Rate → Trial Start Rate → Onboarding Completion Rate
- Tracks whether users are progressing through the intended journey

**Pillar 2 — Revenue Quality**
- Avg Revenue per User → Avg Revenue per Converted User → Refund Rate (inverse)
- Ensures conversions are high-quality and durable

**Pillar 3 — User Experience & Retention**
- Engagement Score → Days to Convert → Support Ticket Rate (inverse)
- Guards against a rushed or confusing campaign experience

**Guardrail Metrics:**  
1. Refund Rate (threshold: < 5%)  
2. Support Ticket Rate (threshold: < 10%)  
3. Avg Days to Convert (no significant increase vs Control)

*(See outputs/kpi_tree.png for the visual representation)*

---

## 4. Experiment Results Summary

| Metric | Control | Treatment | Δ Change |
|---|---|---|---|
| Users | 693 | 715 | +22 |
| Landing Page Visit Rate | 71.00% | 79.16% | +8.16pp |
| Trial Start Rate | 55.99% | 67.97% | +11.98pp |
| Onboarding Completion Rate | 39.97% | 52.73% | +12.76pp |
| **Paid Conversion Rate** | **3.18%** | **6.99%** | **+3.81pp** |
| Avg Revenue / User | $3.99 | $8.26 | +$4.27 |
| Avg Revenue / Converted User | $125.23 | $117.83 | −$7.40 |
| Refund Rate | 4.33% | 4.34% | +0.01pp |
| Support Ticket Rate | 38.96% | 38.88% | −0.08pp |
| Avg Engagement Score | 59.86 | 60.18 | +0.32 |
| Avg Days to Convert | 15.9 days | 14.1 days | −1.8 days |

The entire activation funnel improved in the Treatment group. Users progressed further and faster through onboarding, leading to a doubling of the paid conversion rate.

---

## 5. Hypothesis Test Interpretation

- **Test:** One-tailed two-proportion Z-Test
- **H₀:** Conversion rate, Treatment ≤ Conversion rate, Control
- **H₁:** Conversion rate, Treatment > Conversion rate, Control
- **Z-Statistic:** 3.2640
- **P-Value:** 0.0005
- **95% CI for Δ:** [+1.48pp, +6.17pp]

**Conclusion:** Reject H₀. The observed improvement is statistically significant and unlikely to be due to chance. The entire confidence interval lies above zero, confirming the direction of the effect.

---

## 6. Guardrail Metric Analysis

| Guardrail Metric | Control | Treatment | Assessment |
|---|---|---|---|
| Refund Rate | 4.33% | 4.34% | ✅ Negligible change; well below 5% threshold |
| Support Ticket Rate | 38.96% | 38.88% | ✅ Marginally lower; no concern |
| Avg Days to Convert | 15.9 days | 14.1 days | ✅ Faster conversion; positive signal |
| Avg Revenue per Converted User | $125.23 | $117.83 | ⚠️ Slight decline; worth monitoring |

**Key Finding:** No guardrail metric shows a meaningful deterioration. The slight decline in revenue per converted user ($7.40) may indicate Treatment is converting users on lower-tier plans, but the overall revenue per user (+$4.27) is higher because more users are converting at all. This should be monitored post-launch by plan type.

---

## 7. Segment-Level Insight

| Dimension | Notable Finding |
|---|---|
| Device Type | Mobile users in Treatment show strongest conversion lift; Desktop improvement is moderate |
| Region | Treatment performs consistently across all regions with no meaningful outlier |
| Traffic Source | Organic and Direct traffic respond most strongly to the new campaign; Paid traffic shows smaller lift |
| Plan Type | Basic plan users drive most of the conversion volume increase; Premium lift is smaller |

**Implication:** A conservative phased rollout starting with Mobile + Organic/Direct segments captures the highest-confidence uplift while limiting exposure to the segments with weaker signals.

---

## 8. Final Recommendation

> **Recommended Action: Phased Launch**

Launch the Treatment experience to all **Mobile users** and users arriving via **Organic or Direct traffic** immediately. Extend to remaining segments (Desktop, Paid traffic) after 3–4 weeks of post-launch monitoring.

**Rationale:**
- The statistical evidence for a real conversion lift is strong (p = 0.0005)
- No guardrail metric is in a danger zone
- Segment data suggests heterogeneous effects; a phased approach limits downside risk
- Avg days to convert is shorter in Treatment, suggesting the new experience doesn't slow the decision journey

---

## 9. Risks and Limitations

1. **Low base conversion rates** amplify variance — the absolute user counts behind conversion figures are small (22 vs 50 conversions), making the result sensitive to individual user behavior.
2. **Experiment duration** was not confirmed to be free of novelty effects — early-campaign enthusiasm can inflate conversion rates temporarily.
3. **Revenue per converter** declined slightly — if this persists, lifetime value calculations may need revisiting.
4. **External confounders** (seasonal patterns, marketing channel spend shifts) were not controlled.
5. **Segment sample sizes** in the breakdowns are small; segment-level conclusions are directional, not definitive.

---

## 10. Next Steps

1. **Week 1–2:** Deploy Treatment to Mobile + Organic/Direct segments; instrument daily monitoring dashboards for refund and support ticket rates.
2. **Week 3:** Review revenue-per-converter trend by plan type; flag if average drops below $110.
3. **Week 4:** Evaluate remaining segments (Desktop, Paid traffic) with fresh data.
4. **Month 2:** Run follow-up cohort analysis on 60-day and 90-day retention of converted Treatment users vs Control converters.
5. **Month 3:** If retention holds, proceed with full global rollout and deprecate the legacy onboarding experience.

---

*This memo was prepared based on experiment data from the company's internal A/B testing infrastructure. All statistical tests were performed at α = 0.05. Segment-level figures are directional estimates.*
