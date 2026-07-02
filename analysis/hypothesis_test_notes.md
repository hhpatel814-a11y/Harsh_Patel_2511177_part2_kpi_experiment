# Hypothesis Test Documentation

**Analyst:** Harsh Patel  
**Experiment:** Onboarding & Activation Campaign — Control vs Treatment  
**Date of Analysis:** June 2025  

---

## 1. Metric Selected for Testing

**Paid Conversion Rate** — the proportion of users in each group who completed a paid subscription within the first 30 days of signup.

### Why This Metric?

Paid conversion is the single most direct signal of whether the new campaign is achieving its commercial purpose. It captures the end outcome of the entire activation funnel: a user who has visited the landing page, started a trial, completed onboarding, and ultimately committed financially. All other metrics either lead into it (funnel steps) or guard against side effects from optimizing it (guardrails).

---

## 2. Hypothesis Statements

| Element | Statement |
|---|---|
| **Null Hypothesis (H₀)** | The paid conversion rate in the Treatment group is less than or equal to the paid conversion rate in the Control group. p_treatment ≤ p_control |
| **Alternate Hypothesis (H₁)** | The paid conversion rate in the Treatment group is strictly greater than the paid conversion rate in the Control group. p_treatment > p_control |

---

## 3. Test Configuration

| Parameter | Value |
|---|---|
| **Test Type** | Two-proportion Z-Test |
| **Tail** | One-tailed (right-tailed) — we are testing for improvement, not merely difference |
| **Significance Level (α)** | 0.05 |
| **Confidence Level** | 95% |
| **Sample Size — Control** | 693 users |
| **Sample Size — Treatment** | 715 users |

### Justification for One-Tailed Test

The business question is directional: does the new campaign increase conversion? A two-tailed test would be appropriate if we were equally concerned about a decrease. Since the experiment objective is specifically improvement, a one-tailed test is the correct formulation. This also avoids inflating the rejection threshold unnecessarily.

---

## 4. Test Inputs & Calculations

| Input | Control | Treatment |
|---|---|---|
| Number of Users (n) | 693 | 715 |
| Converted Users | 22 | 50 |
| Observed Conversion Rate | 3.18% | 6.99% |
| Pooled Proportion (p̂) | 0.0508 | ← shared |
| Standard Error (SE) | 0.0117 | ← shared |

**Formulas Applied:**

```
Pooled proportion:  p̂ = (x_ctrl + x_trt) / (n_ctrl + n_trt)
Standard Error:     SE = sqrt(p̂ × (1 − p̂) × (1/n_ctrl + 1/n_trt))
Z-statistic:        Z  = (p_trt − p_ctrl) / SE
P-value (one-tail): P  = 1 − Φ(Z)
```

---

## 5. Test Output

| Output | Value |
|---|---|
| **Z-Statistic** | **3.2640** |
| **P-Value (one-tailed)** | **0.0005** |
| **95% Confidence Interval for Δ** | [0.0148, 0.0617] |
| **Observed Lift (Δ)** | +3.81 percentage points |

---

## 6. Decision Rule & Interpretation

**Decision Rule:** Reject H₀ if p-value < α (0.05)

**Result:** p-value = 0.0005 < 0.05 → **Reject H₀**

### Business Interpretation

The statistical evidence is strong. The Treatment group's paid conversion rate (6.99%) is meaningfully higher than the Control group's rate (3.18%). With a Z-score of 3.26 and a p-value of 0.0005, the probability of observing this large a difference by random chance alone — assuming no real treatment effect — is approximately 0.05%. This is well below the 5% threshold we set before running the test.

The 95% confidence interval [1.48%, 6.17%] is entirely positive, meaning we can be confident the treatment effect is real and in the right direction, not merely a statistical artefact.

**However**, statistical significance alone is not sufficient grounds for a full launch recommendation. Guardrail metrics must also be evaluated before a final decision is made (see Recommendation Memo).

---

## 7. Caveats & Limitations

- Overall conversion rates are low (< 7%) meaning the absolute number of converted users is small (22 vs 50), which increases the influence of individual-level variance.
- The experiment duration and external factors (seasonality, marketing spend changes) were not controlled for in this analysis.
- Segment-level conversion differences (e.g., by region or device) may mask heterogeneous treatment effects — a finding that warrants deeper investigation.
