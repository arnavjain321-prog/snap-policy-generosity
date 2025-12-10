# Modeling SNAP Policy Generosity Across U.S. States

This project analyzes differences in **SNAP (Supplemental Nutrition Assistance Program)** generosity across U.S. states. Using a combined dataset of economic, demographic, cost-of-living, and policy variables, we explore how structural factors relate to SNAP participation, benefit levels, and program reach.

The final modeling dataset includes **51 state observations** with engineered features such as:
- benefits per person
- SNAP participants per 1,000 residents
- demographic composition
- cost-of-living indicators
- policy tiers

The notebook contains:
- data engineering across heterogeneous sources
- feature creation and transformation
- multi-class classification models
- statistical exploration of key relationships
- a reproducible ML pipeline in Python

---

## Research Question

**What economic, demographic, and policy characteristics are associated with more “generous” SNAP environments across states?**

To model generosity, we define a **SNAP Policy Class** based on state participation levels:

- **Low**: < 33rd percentile  
- **Moderate**: 33–66th percentile  
- **High**: ≥ 66th percentile  

This allows comparisons across states with different populations and policy structures.

---

## Data Engineering

The dataset integrates the following sources:

- **ACS 2024**: poverty rate, median household income, race shares  
- **USDA SNAP**: benefits per state + participant counts  
- **BLS RPP**: Food-at-Home grocery cost index  
- **State policy indicators**: minimum wage tier (low/medium/high), trifecta control  
- **USDA SNAP regions**  
- **RUCC** rural-urban classifications  

Derived features include:

- `benefits_per_person`
- `participants_per_1000`
- `grocery_cost_index`
- `snap_policy_class` (target variable)
- race share features

Final dataset: **51 rows × 24 features**.

---

## Modeling Approach

Several models are evaluated for **multi-class classification**:

- Logistic Regression  
- k-Nearest Neighbors  
- Random Forest  
- Neural Network (MLP)  
- PCA + K-Means (unsupervised)  
- Ridge regression for benefit-level modeling  

All models use a **consistent pipeline** with:

- `StandardScaler` for numeric features  
- `OneHotEncoder` for categorical features  
- `ColumnTransformer` for reproducibility  

---

## Key Findings

From exploratory analysis:

- Higher **poverty rates** are strongly associated with higher SNAP participation per 1,000 residents.  
- The **grocery cost index** is highly correlated with **median household income** (0.88), reflecting cost-of-living pressures.  
- States with larger **Asian and Pacific Islander populations** show higher benefits per person; likely geographic and cost-of-living effects.  
- **Minimum wage** is not strongly predictive; many states share the same federal baseline ($7.25).  
- Regional patterns are clear:  
  - **Mid-Atlantic** and **Southwest** have the highest participation  
  - **Mountain Plains** has the lowest  

This is a **descriptive** analysis, not causal. Results highlight patterns that may guide future applied research.

---

## Repository Structure

project-root/
│
├─ data/              
│   └─ final_master_dataset.csv
│
├─ notebooks/         
│   └─ report.ipynb
│
├─ report.pdf         
├─ requirements.txt   
└─ README.md


(Visualizations are embedded directly in the notebook.)

---

## How to Reproduce

```bash
# clone the repo
git clone https://github.com/arnavjain321-prog/snap-policy-generosity.git
cd snap-policy-generosity

# install dependencies
pip install -r requirements.txt

# run the notebook
jupyter notebook notebooks/report.ipynb
Acknowledgements

This project builds on a collaborative class project completed with:

Shawn Ding

Grace George

Razan Habboub

Aeon Levy
