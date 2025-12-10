SNAP Policy Generosity Across U.S. States

This project analyzes differences in SNAP (Supplemental Nutrition Assistance Program) generosity across U.S. states using a combined dataset of economic, demographic, cost-of-living, and policy features. We engineer a state-level modeling dataset (51 rows) to explore how structural factors relate to SNAP participation, benefit levels, and program reach.

The work includes:

custom data engineering from 10+ heterogeneous sources

feature creation (benefits per person, SNAP participants per 1,000 residents, policy tiers)

classification modeling (Low / Moderate / High generosity classes)

statistical exploration of patterns and correlations

a fully reproducible pipeline in Python

Research Question

What economic, demographic, and policy characteristics are associated with more “generous” SNAP environments across states?

We define a SNAP Policy Class using state participation levels:

Low: < 33rd percentile

Moderate: 33–66th percentile

High: ≥ 66th percentile

This allows us to compare states with similar population sizes and different policy choices.

Data Engineering

We construct a unified dataset using the following sources:

ACS 2024: poverty rate, median household income, race shares

USDA SNAP: benefits + participant counts

BLS RPP: Food-at-Home grocery cost index

State policy indicators: minimum wage tier (low/medium/high), trifecta control

USDA SNAP regions

RUCC rural-urban classification

From these we derive:

benefits_per_person

participants_per_1000

grocery_cost_index

snap_policy_class (target variable)

Race % distributions (white, Black, Native, Asian, Pacific, 2-plus)

Final dataset: 51 states × 24 features.

Modeling

We evaluate several methods for multi-class classification:

Logistic Regression

k-Nearest Neighbors

Random Forest

Neural Network (MLP)

PCA + K-Means clustering (unsupervised)

Ridge regression for benefit-level modeling

All models use a consistent pipeline with:

StandardScaler for numeric features

OneHotEncoder for categorical features

ColumnTransformer for clean reproducibility

Key Findings (Summary)

From exploratory data analysis:

Higher poverty rates are strongly associated with higher SNAP participation per 1,000 residents.

Grocery cost index correlates strongly with median household income (0.88), suggesting cost-of-living pressures.

States with larger Asian and Pacific Islander populations show higher benefit levels per person, potentially reflecting geographic and cost-of-living patterns.

Minimum wage is not strongly predictive at the state level because many states cluster at the federal baseline ($7.25).

USDA SNAP regions show clear differences: Mid-Atlantic and Southwest have the highest participation; Mountain Plains the lowest.

This project is descriptive, not causal. We highlight patterns that may inform future empirical work.

Structure
/project-root
  ├─ data/             # raw and processed sources
  ├─ notebooks/        # Jupyter notebook (end-to-end analysis)
  ├─ final_master_dataset.csv
  ├─ report.pdf
  └─ README.md


(Not adding visuals; plots are embedded in the notebook.)

How To Reproduce

Clone the repo

Install dependencies:

pip install -r requirements.txt


Run the main notebook:

jupyter notebook notebooks/


The full pipeline loads raw data, builds the master dataset, runs modeling, and outputs findings.

Team

Shawn Ding

Grace George

Razan Habboub

Arnav Jain

Aeon Levy