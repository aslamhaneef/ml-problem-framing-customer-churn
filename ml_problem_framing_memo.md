# ML Problem-Framing Memo — Customer Churn

## 1. Decision
The proposed use case is to support a customer-success workflow by identifying customers who may warrant proactive retention review.

The prediction should support human review. It should not, by itself, automatically cancel service, deny service, impose penalties, or make other adverse customer decisions.

## 2. Prediction target
**Target:** `churned`

- `1` = churned
- `0` = not churned

This is a binary classification problem.

## 3. Unit of observation
One row represents one customer.

## 4. Available fields
- `customer_id` — identifier; excluded from model features
- `tenure_months`
- `support_tickets`
- `monthly_spend_inr`
- `last_login_days`
- `plan_type`
- `churned` — target

## 5. Action window
The supplied dataset does not define when the features were captured relative to the churn outcome, nor does it define an operational retention-action window. A production implementation must establish a prediction-time cutoff and a documented period during which the prediction can be acted upon.

## 6. Non-ML baseline
A majority-class baseline predicts the most common class for every customer.

In this dataset:
- total observations: 12
- not churned: 7
- churned: 5
- majority class: 0
- majority-class accuracy: 0.583 (58.3%)

The baseline has zero churn recall because it never predicts the minority class.

## 7. ML baseline
An exploratory Logistic Regression pipeline is included in the notebook. Numerical features are standardized and `plan_type` is one-hot encoded. `customer_id` is excluded.

Because the dataset contains only 12 observations, model results are exploratory and should not be interpreted as production performance.

## 8. Error costs
**False positive:** a customer is flagged as likely to churn but does not churn. Potential consequences include unnecessary outreach, incentives, or staff time.

**False negative:** a customer is not flagged but later churns. Potential consequence is a missed retention opportunity.

The supplied materials do not provide monetary costs for either error, so no numerical cost ratio is invented here.

## 9. Human review and abstention
Predictions should be treated as decision support. Uncertain cases should be eligible for abstention or human review rather than forced automated action.

## 10. Monitoring and rollback
Monitor data quality, feature distributions, model performance, false-positive/false-negative rates, and drift. If data quality or validated performance becomes unacceptable, suspend automated use and revert to manual review or the documented non-ML baseline.

## 11. Key limitations
- The dataset has only 12 rows.
- The provenance, collection process, consent/licensing status, and sampling method are not documented in the supplied materials.
- Feature timestamps are not supplied, so temporal leakage cannot be fully assessed.
- The sample contains only three plan types and all five `Basic` observations are churned, while all `Standard` and `Pro` observations are not churned. This may be a sampling artifact or a constructed relationship and should not be assumed to generalize.
- Fairness analysis by protected group is not possible from the supplied fields because no explicit sensitive-group labels are provided.

## 12. Deployment conclusion
This dataset is suitable for demonstrating responsible problem framing and an exploratory baseline. It is not sufficient by itself to justify production deployment.
