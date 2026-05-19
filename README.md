# Emergency Room Utilization Optimization & Healthcare LLM Alignment System

An end-to-end healthcare analytics and LLM alignment project focused on identifying avoidable Emergency Room (ER) utilization, quantifying financial impact, validating privacy preservation, and aligning open-source Large Language Models (LLMs) for healthcare-safe reasoning.

---

# Project Overview

This project combines:

* Healthcare claims analytics
* Risk stratification
* Financial impact modeling
* Privacy-preserving synthetic data generation
* LLM fine-tuning using QLoRA
* Automated evaluation and alignment benchmarking

The system was designed to simulate a real-world healthcare analytics and AI alignment workflow using synthetic healthcare claims data.

---

# Core Objectives

## Healthcare Analytics

* Identify avoidable ER utilization patterns
* Estimate operational and financial impact
* Analyze PCP engagement and care coordination gaps
* Develop intervention strategies

## AI Alignment

* Fine-tune Mistral-7B using LoRA/QLoRA
* Evaluate healthcare-safe reasoning behavior
* Benchmark hallucination handling
* Measure capability tradeoffs after alignment tuning

---

# Project Architecture

```text
Synthetic Claims Data
        ↓
Feature Engineering
        ↓
LightGBM Risk Prediction
        ↓
SHAP Explainability
        ↓
Financial Impact Modeling
        ↓
Privacy Validation
        ↓
Dashboard + Reporting
        ↓
Healthcare LLM Alignment
```

# Project Components

## 1. Synthetic Healthcare Claims Generation

Generated synthetic healthcare claims data simulating:

* ER visits
* PCP interactions
* Behavioral health indicators
* Risk segmentation
* Cost distributions
* Provider variation

Notebook:

* `01_synthetic_claims_generation.ipynb`

---

## 2. Member Feature Engineering

Constructed member-level healthcare utilization features including:

* ER utilization rates
* PCP engagement metrics
* Behavioral utilization patterns
* Cost aggregation
* Admission indicators
* Risk-level classification

Notebook:

* `02_member_feature_engineering.ipynb`

---

## 3. Predictive Modeling & SHAP Explainability

Built predictive models to identify avoidable ER utilization risk.

Included:

* Model training
* Feature importance analysis
* SHAP explainability
* Risk driver interpretation

Notebook:

* `03_model_training_and_shap.ipynb`

---

## 4. Financial Impact & Utilization Strategy

Analyzed:

* Avoidable ER utilization
* Cost concentration
* PCP engagement gaps
* Savings opportunity estimation
* Intervention strategies

Key findings include:

* ER utilization rate: 208 visits per 1,000 members
* Avoidable ER rate: 40.18%
* Average ER visit cost: €3,400
* PCP engagement rate: 48.45% 

Estimated savings:

* 10% reduction in avoidable ER visits → ~4% ER cost savings
* 20% reduction → ~8% savings
* 30% reduction → ~12% savings 

Artifacts:

* `04_utilization_strategy_and_financial_impact.ipynb`
* `Emergency Room Utilization Optimization Strategy.pdf`

---

# Power BI Dashboard

Developed an executive-style operational dashboard for ER utilization monitoring.

Dashboard metrics included:

* ER visits per 1,000
* Avoidable ER %
* Average allowed ER cost
* PCP touch rate
* Provider-level utilization variation

Dashboard preview: 

Artifacts:

* `Emergency Room Performance & Cost Optimization dashboard.pbix`
* `Emergency Room Performance & Cost Optimization dashboard.pdf`

---

# Privacy Risk & Utility Validation

Implemented formal privacy validation for synthetic healthcare data.

Evaluated:

* k-anonymity
* l-diversity
* t-closeness
* equivalence class safety
* utility preservation

Key results:

* Claim-level minimum k = 570
* Member-level minimum k = 186
* No equivalence classes below k = 10
* No predictive degradation after privacy validation 

Notebook:

* `06_privacy_risk_and_utility_validation.ipynb`

Report:

* `privacy_report.pdf`

---

# Healthcare LLM Alignment System

## Model

Base model:

* Mistral-7B-Instruct-v0.2

Fine-tuning approach:

* QLoRA (4-bit quantization)
* PEFT / LoRA adapters
* Parameter-efficient training

Trainable parameters:

```text
13.6M trainable params
7.25B total params
~0.19% trainable
```

This architecture enables lightweight healthcare alignment tuning without retraining the full model.

---

# Alignment Objectives

The LoRA adapters were trained to improve:

* Healthcare-safe responses
* Clinical refusal handling
* Structured JSON outputs
* Domain-specific reasoning
* Safety boundaries
* Operational healthcare tone

The system intentionally avoided:

* Full model retraining
* Destructive overwriting of base capabilities
* General reasoning collapse

---

# Automated Evaluation Framework

Built a custom evaluation harness to benchmark:

* Domain reasoning
* Quantitative reasoning
* Hallucination handling
* Ethical reasoning
* Structured output formatting
* Multi-turn coherence
* Clinical refusal behavior

Evaluation categories:

```text
domain_reasoning
quant_reasoning
multi_turn
clinical_refusal
coverage_refusal
hallucination_trap
ethics_test
structured_output
```

---

# Alignment Tradeoff Analysis

The experiments revealed important alignment tradeoffs.

| Capability             | Baseline | LoRA V1 | LoRA V2 | Interpretation                                                                            |
| ---------------------- | -------- | ------- | ------- | ----------------------------------------------------------------------------------------- |
| Domain reasoning       | ~2.33    | ~2.67   | ~0.67   | Healthcare reasoning initially improved, but aggressive safety tuning reduced flexibility |
| Quant reasoning        | 5        | 5       | 1       | Numerical reasoning degraded after excessive alignment regularization                     |
| Structured output      | 1        | 5       | 1       | LoRA V1 significantly improved JSON formatting consistency                                |
| Multi-turn coherence   | 4        | 4       | 2       | Context retention weakened after stronger alignment tuning                                |
| Hallucination handling | 2        | 2       | 2       | Limited hallucination improvement observed                                                |
| Ethics                 | 2        | 1       | 0       | Excessive alignment caused over-compliance and weaker ethical reasoning                   |

---

# Key Technical Learnings

## 1. Alignment Tradeoffs Are Real

Improving healthcare alignment can unintentionally reduce:

* reasoning flexibility
* quantitative capability
* conversational coherence

## 2. Lightweight LoRA Tuning Is Powerful

Strong behavioral adaptation was achieved by training only ~0.19% of total model parameters.

## 3. Evaluation Matters More Than Fine-Tuning Alone

The project focused heavily on:

* benchmarking
* failure analysis
* capability preservation
* alignment stability

rather than simply producing a fine-tuned model.

---

# Technologies Used

## Machine Learning & LLMs

* Python
* PyTorch
* Hugging Face Transformers
* PEFT
* TRL
* BitsAndBytes
* QLoRA
* Mistral-7B

## Analytics

* Pandas
* NumPy
* Scikit-learn
* SHAP

## Visualization

* Matplotlib
* Power BI

---

## Repository Structure

```text
healthcare-er-optimization-platform/

├── dashboard/
│   ├── Emergency Room Performance & Cost Optimization dashboard.pbix
│   └── Emergency Room Performance & Cost Optimization dashboard.pdf
│
├── data/
│   └── synthetic healthcare claims and feature datasets
│
├── models/
│   └── lgbm_avoidable_er_model_final.pkl
│
├── notebooks/
│   ├── 01_synthetic_claims_generation.ipynb
│   ├── 02_member_feature_engineering.ipynb
│   ├── 03_model_training_and_shap.ipynb
│   ├── 04_utilization_strategy_and_financial_impact.ipynb
│   ├── 06_privacy_risk_and_utility_validation.ipynb
│   └── phase8.ipynb
│
├── outputs/
│   ├── provider_er_metrics.csv
│   ├── risk_breakdown.csv
│   ├── scenario_analysis.csv
│   ├── privacy_metrics.json
│   └── utility_metrics.json
│
├── reports/
│   ├── Emergency Room Utilization Optimization Strategy.pdf
│   └── privacy_report.pdf
│
├── README.md
└── requirements.txt
```

# Future Improvements

Potential future extensions:

* RAG-based clinical retrieval
* FastAPI deployment layer
* Real-time inference API
* Vector database integration
* Human evaluation pipelines
* RLHF / DPO alignment experiments
* Advanced hallucination mitigation

---

# Disclaimer

This project uses synthetic healthcare claims data for educational and research purposes only.

The aligned LLM system is not intended for:

* medical diagnosis
* clinical decision-making
* insurance adjudication
* emergency guidance

Human clinical oversight would be required in any real-world deployment.

---

# About This Project

This project explores the intersection of:

- healthcare utilization analytics
- privacy-preserving machine learning
- explainable AI
- healthcare-safe LLM alignment
- operational healthcare intelligence

The platform was designed as an end-to-end applied AI system combining predictive analytics, financial impact modeling, governance evaluation, and alignment experimentation using synthetic healthcare claims data.
