🧪 QSAR Melting Point Prediction with Interpretable & Causal Machine Learning

This repository contains the full pipeline for predicting melting point (Tm) of organic molecules using stacked machine learning, combined with:

Model interpretability (SHAP)

Robustness validation (impossibility & perturbation testing)

Statistical validation (A/B testing, effect sizes)

Causal inference (CausalML meta-learners)

This project goes beyond typical QSAR ML by not only predicting melting point accurately, but also explaining, validating, and stress-testing the model scientifically.

This work is prepared for research preprint publication on OSF.
 

🎯 Objectives

Predict molecular melting point (Tm) using chemical descriptors

Avoid black-box QSAR by adding interpretability

Test if the model behaves logically under impossible inputs

Identify causal relationships between descriptors and Tm

Statistically validate descriptor influence using A/B testing


🧬 Dataset

The dataset is Feeature Engineered with organic molecules with computed descriptors:

- LogP

- Molecular Weight (MolWt)

- TPSA

- NumHDonors / NumHAcceptors

- RingCount

- NumAromaticRings / NumAliphaticRings

- NumRotatableBonds

- FractionCSP3

- Other RDKit descriptors

🚀 Pipeline Overview

1️⃣ Preprocessing

Descriptor cleaning

Missing value handling

Feature scaling

Train/Test split

2️⃣ Base Models

Linear Regression

ElasticNet

Random Forest

SVR

XGBoost

LightGBM

3️⃣ Stacked Ensemble

Base model predictions are used as meta-features for a final regressor.

Why?
Stacking consistently outperformed individual models in R², MAE, and MSE.


🔍 Model Interpretability (SHAP)

We use SHAP with LightGBM to understand:

Global feature importance

Descriptor interactions

Descriptor influence direction on Tm

Outputs:

SHAP summary plot

Beeswarm plot

Dependence plots



🧪 Impossibility Testing

Descriptors are randomly scrambled to create chemically impossible molecules.

If the model still predicts well → overfitting
If error explodes → model learned real chemical patterns

Result:

MAE on scrambled descriptors: 143.18
Fraction flagged as impossible: 5.07%


This validates model robustness.


🌪 Extreme Perturbation Testing

Descriptors are pushed to unrealistic extremes to test model stability.

This checks:

Sensitivity

Logical behavior

Descriptor boundaries


🧠 Causal Inference (CausalML)

For top descriptors:

Convert descriptor into binary treatment (above/below median)

Estimate Average Treatment Effect (ATE) on melting point

Identify descriptors that causally influence Tm, not just correlate

Output:

ATE bar plots

Feature causal ranking


📊 A/B Statistical Testing

For key descriptors, we perform:

Two-sample t-tests

p-values

Cohen’s d (effect size)

Example findings:

Descriptor	t-stat	p-value	Cohen's d
RingCount	-18.81	0.0000	1.063
NumAromaticRings	-21.62	0.0000	0.931
MolWt	-19.67	0.0000	0.853
TPSA	-15.82	0.0000	0.686
FractionCSP3	15.79	0.0000	-0.690

This statistically supports SHAP and causal findings.


🔬 Scientific Contributions

This project combines in a single QSAR study:

- Stacked ML

- SHAP interpretability

- Impossibility testing

- Extreme perturbation testing

- Causal inference

- Statistical hypothesis testing

This level of validation is rare in QSAR machine learning research.

⚠️ Disclaimer

This project is for research and educational purposes only.
Predictions must not be used in real-world chemical decision-making without laboratory validation.

📜 License

MIT License
