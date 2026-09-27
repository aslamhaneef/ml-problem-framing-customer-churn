# Risk Register — Customer Churn ML

| ID | Risk | Likelihood / evidence | Potential impact | Mitigation / control | Monitoring / trigger |
|---|---|---|---|---|---|
| R1 | Extremely small dataset | 12 observations | Unstable estimates; poor generalization | Collect substantially more representative data | Reassess before production |
| R2 | Unknown provenance | Source/ownership not supplied | Compliance, privacy, or licensing problems | Verify provenance, ownership, consent and license | Block production use until verified |
| R3 | Sampling bias | Sampling method not documented | Model may not represent real customers | Document sampling and validate on representative data | Compare incoming population to training data |
| R4 | Temporal leakage | Feature timestamps absent | Inflated validation performance | Define feature availability and prediction-time cutoff | Audit feature timestamps |
| R5 | False negative | Churner predicted as non-churner | Missed retention opportunity | Monitor recall; review errors | Track false-negative rate |
| R6 | False positive | Non-churner predicted as churner | Unnecessary outreach/incentive cost | Monitor precision; quantify intervention cost | Track false-positive rate |
| R7 | Plan-type shortcut | All Basic rows churn; all Standard/Pro rows do not | Model may learn a sample-specific shortcut | Sensitivity analysis without `plan_type`; validate on larger data | Compare performance across future cohorts |
| R8 | Privacy / excessive data use | Customer-level records | Unauthorized exposure or misuse | Data minimization, access control, approved use | Access and data-use audits |
| R9 | Proxy effects | No sensitive labels available | Potential unequal error rates may go undetected | Conduct lawful subgroup analysis when data is available | Monitor subgroup error rates |
| R10 | Automation risk | Predictions could be over-trusted | Inappropriate customer actions | Human review; no automatic adverse decisions | Review intervention workflow |
| R11 | Model drift | Future customer behavior may change | Performance degradation | Monitor feature and outcome drift; retrain only after validation | Define performance thresholds |
| R12 | Rollback failure | No operational rollback defined | Continued use of degraded model | Revert to manual review / non-ML baseline | Test rollback procedure |

## Proposed deployment guardrails

1. Do not treat the current 12-row dataset as production evidence.
2. Do not use `customer_id` as a predictive feature.
3. Establish a prediction-time cutoff before deployment.
4. Keep human review in the retention workflow.
5. Define acceptable false-positive and false-negative rates using actual business costs before setting an operating threshold.
6. Suspend automated use when data-quality, drift, or validated-performance conditions breach approved limits.
