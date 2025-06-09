# Bayesian Network for Predicting Maternal-Health Risk

**Author:** Fatima Essa  
**Project type:** End-to-end, interpretable probabilistic model in healthcare  
**Tech stack:** Python 3.10 · pgmpy · scikit-learn · pandas · networkx · matplotlib

> “Meaningful AI” in action: our model spots high-risk pregnancies with  
> **93 % precision and 0.94 AUC**, giving clinicians an interpretable tool  
> to intervene early and save lives.  

---

## 1. Problem Statement
Maternal mortality remains a global concern.  We ask:

**How can a transparent, probabilistic model identify mothers at greatest risk during pregnancy, childbirth and postpartum—using only routinely-captured vital signs?**

---

## 2. Data
* **Source:** Kaggle “Maternal Health Risk Data Set”  
  (IoT-based collection across hospitals & clinics).  
* **Features:** Age, SystolicBP, DiastolicBP, Blood-Sugar, Heart-Rate, RiskLevel.  
* **Pre-processing:**  
  * Remove HR outliers, impute missing values (mean / mode)  
  * Standardise numeric features  
  * Stratified 80 / 20 train-test split to keep RiskLevel distribution. :contentReference[oaicite:1]{index=1}  

---

## 3. Methodology
| Step | Technique | Lib / Algo |
|------|-----------|------------|
| **Structure learning** | HillClimbSearch + BIC | `pgmpy` |
| **Parameter learning** | Maximum-Likelihood Estimation | `pgmpy` |
| **Hyper-parameter** | `max_indegree` sweep (1 – 5) | grid search |
| **Evaluation** | Confusion matrix, Precision/Recall, F1, ROC-AUC, Log-Loss | `sklearn` |

The final DAG exposes causal links (e.g., Blood-Pressure → RiskLevel) and supports **what-if queries**.

---

## 4. Results
| Class | Precision | Recall | AUC | Log-Loss |
|-------|-----------|--------|-----|----------|
| High-Risk | **0.93** | 0.78 | **0.94** | 0.25 |
| Mid-Risk | 0.62 | 0.27 | 0.69 | 0.56 |
| Low-Risk | 0.56 | **0.89** | 0.73 | 0.51 |
| **Overall** | – | – | **0.79** | 0.72 |

The model prioritises **catching high-risk cases**—critical in obstetrics.
