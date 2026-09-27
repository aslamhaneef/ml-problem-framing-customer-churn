# ML Problem Framing & Responsible Data Card — Customer Churn

This folder contains the complete internship-task submission based on the supplied customer churn dataset and responsible-data-card template.

## Files

- `01_churn_baseline.ipynb` — data checks, non-ML baseline, exploratory Logistic Regression, LOOCV evaluation, sensitivity check and responsible-ML interpretation.
- `ml_problem_framing_memo.md` — decision, target, observation unit, action window, baseline, error costs and deployment limitations.
- `responsible_data_card.md` — completed data card covering purpose, provenance, representation, features, quality, risks and evaluation.
- `risk_register.md` — risk register with mitigations, monitoring and rollback controls.
- `churn_analysis_summary.csv` — compact summary of key dataset checks.
- `customer-churn-training.csv` — supplied training data.

## Dataset facts

- Rows: 12
- Columns: 7
- Missing values: 0
- Duplicate rows: 0
- Not churned: 7
- Churned: 5
- Majority-class accuracy: 58.3%

## How to use the notebook

1. Keep `01_churn_baseline.ipynb` and `customer-churn-training.csv` in the same folder.
2. Open the notebook in Jupyter Notebook, JupyterLab, VS Code, or Google Colab.
3. Run all cells from top to bottom.
4. Review the outputs and keep the responsible-ML limitation statements.

## Submission note

The dataset is extremely small. The exploratory model results are intentionally presented as a demonstration, not as evidence that a production churn model is ready for deployment.
