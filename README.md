# Causality-Informed Models for Multidrug-Resistant Organism Prediction  
### Enabling Effective ICU Antibiotic Stewardship

## 📌 Overview
Antimicrobial resistance, particularly caused by multidrug-resistant organisms (MDROs), poses a critical challenge to global healthcare systems. Early and reliable prediction of MDRO infections is essential for improving ICU antibiotic stewardship and patient outcomes.

This repository presents a **causality-informed prediction framework** that integrates:
- Causal discovery for feature selection
- Temporal modeling of ICU clinical data
- Machine learning and deep learning models

Our approach identifies structurally meaningful predictors instead of relying on spurious correlations.

---

## 🎯 Objectives
This study aims to:

1. **Identify causality-informed predictors** of MDRO infections  
   - Using causal discovery methods to uncover stable clinical drivers

2. **Evaluate predictive performance**  
   - Compare traditional ML and deep learning models  
   - Validate across two real-world ICU datasets

---

## 🗂️ Datasets

We use two publicly available ICU datasets:

- **MIMIC-IV (v3.1)**  
- **MIMIC-III (v1.4)** (non-overlapping subset)

### Inclusion Criteria
- Adult patients (≥18 years)
- ICU stay > 24 hours
- At least one microbiological culture
- Only the first ICU admission per hospital stay

---

## 🦠 MDRO Definition

MDRO is defined as:
> Non-susceptibility to at least one agent in **≥3 antimicrobial categories**

We focus on 5 major pathogen groups:
- *Staphylococcus aureus* (including MRSA)
- *Acinetobacter spp.*
- *Enterococcus spp.*
- *Enterobacteriaceae*
- *Pseudomonas aeruginosa*

---

## 🧠 Methodology

### 1. Causality-Informed Feature Selection

#### 🔹 Temporal Data Processing
To align time-series data with static outcomes:
- First 24h ICU data is summarized into:
  - Median
  - Last observed value
  - Cumulative sum

#### 🔹 Causal Discovery Methods
We use two complementary approaches:
- **DAG-GNN** → captures nonlinear causal relationships  
- **FCI** → accounts for latent confounders  

To improve robustness:
- Each method is run **5 times**
- Only edges appearing in **≥3 runs** are retained

#### 🔹 Edge Types
- `A → B` : Potential causal relationship  
- `A ↔ B` : Latent confounding (hidden common cause)

#### 🔹 Markov Boundary (MB)
We select features based on the **Markov Boundary of MDRO**, which includes:
- Direct causes
- Direct effects
- Causes of effects

✅ The MB theoretically contains **all necessary predictive information**

---

### 2. Prediction Models

We evaluate two categories of models:

#### 📊 Traditional Machine Learning
- Logistic Regression (LR)
- Random Forest (RF)
- XGBoost

#### 🔁 Deep Learning (Temporal Models)
- Bi-LSTM
- Bi-GRU

---

## 📈 Results

- **32 causality-informed features** identified across 5 MDRO types  
- Best model: **Bi-GRU**

### Key Finding:
> Models using causality-informed features perform as well as or better than full feature sets, while reducing noise and spurious correlations.

