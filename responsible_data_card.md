# Responsible Data Card

## Dataset purpose
This dataset may support exploratory customer-churn prediction and a retention-support workflow.

The prediction should support customer-success review. It must not independently make adverse customer decisions.

## Provenance and permission
The supplied materials do not document the original data source, collection process, ownership, consent, or licensing conditions.

These details must be verified before production use. The supplied dataset should not be treated as evidence of consent or production authorization.

## Population and representation
The dataset contains 12 customer observations.

The sampling procedure, customer population, geographic coverage, collection period, and representativeness are not documented. Therefore, performance cannot be assumed to generalize to the broader customer population.

The target distribution is:
- Not churned: 7 (58.3%)
- Churned: 5 (41.7%)

Plan-type distribution and churn rate in this sample:
           count  sum  mean
plan_type                  
Basic          5    5   1.0
Pro            3    0   0.0
Standard       4    0   0.0

## Features and target
| Field | Role | Notes |
|---|---|---|
| `customer_id` | Identifier | Exclude from model features |
| `tenure_months` | Feature | Numeric |
| `support_tickets` | Feature | Numeric |
| `monthly_spend_inr` | Feature | Numeric |
| `last_login_days` | Feature | Numeric |
| `plan_type` | Feature | Categorical; one-hot encode |
| `churned` | Target | 1 = churned, 0 = not churned |

Potential leakage cannot be fully assessed because feature collection timestamps are not included. In particular, a production pipeline must guarantee that every feature is available before the prediction-time cutoff.

No explicit sensitive attributes are present in the supplied columns. This does not establish that the features are free of sensitive proxies.

## Quality checks
- Rows: 12
- Columns: 7
- Missing values: 0
- Duplicate rows: 0
- Target classes: 0 and 1
- Identifier uniqueness: 12 unique IDs
- Numerical ranges are documented in the notebook.
- The dataset is extremely small.
- A single train/test split would be unstable; the notebook uses leave-one-out cross-validation for exploratory comparison.

## Risks and safeguards
| Risk | Safeguard |
|---|---|
| Small sample / poor generalization | Collect substantially more representative data before deployment |
| Unknown provenance or permission | Verify source, ownership, consent and licensing |
| Sampling bias | Document sampling and validate on representative future data |
| Temporal leakage | Define a prediction-time cutoff and feature availability rules |
| False negatives | Track recall and review missed churn cases |
| False positives | Track precision and intervention burden/cost |
| Privacy | Minimize data, restrict access and apply applicable privacy controls |
| Proxy effects | Assess subgroup outcomes when appropriate group data is lawfully available |
| Automation risk | Human review; no automatic adverse action |
| Model drift | Monitor data/performance drift and define rollback triggers |

## Intended evaluation
**Non-ML baseline:** majority-class predictor.

**Exploratory ML baseline:** Logistic Regression with standardized numeric features and one-hot encoded `plan_type`.

**Performance measures:** accuracy, precision, recall, F1, confusion matrix, and ROC-AUC where appropriate.

**Calibration:** probability quality should be assessed on a substantially larger validation set before operational use; the supplied 12-row dataset is too small for a reliable calibration conclusion.

**Fairness:** subgroup evaluation is not possible from the supplied fields because no explicit sensitive-group labels are provided. If lawful and appropriate subgroup data becomes available, assess error rates and calibration across relevant groups.

**Error analysis:** inspect false positives and false negatives and document likely operational consequences.

## Important limitation
The data card documents what can be established from the supplied files. It does not invent missing provenance, consent, licensing, timestamps, or business costs.
