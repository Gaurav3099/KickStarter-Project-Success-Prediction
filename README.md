# 🚀 Kickstarter Project Success Prediction

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-F7931E?logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Dataset](https://img.shields.io/badge/Dataset-Kaggle-20BEFF?logo=kaggle&logoColor=white)](https://www.kaggle.com/datasets/sripaadsrinivasan/kickstarter-campaigns-dataset)

A machine learning project that predicts whether a **Kickstarter crowdfunding campaign will succeed or fail**, by analyzing historical campaign data and applying multiple predictive modeling approaches across three experimental methods.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Methodology](#-methodology)
- [Models & Approaches](#-models--approaches)
- [Key Features](#-key-features)
- [Installation](#-installation)
- [Usage](#-usage)
- [Results](#-results)
- [License](#-license)

---

## 🔍 Overview

Kickstarter is a leading crowdfunding platform where creators pitch ideas and seek public backing to bring them to life. Despite its reach, the majority of campaigns fail to meet their funding goals. This project leverages machine learning to analyze patterns from thousands of past campaigns, identifying what separates successful projects from unsuccessful ones.

The project is structured as **three distinct modeling approaches** (`method1`, `method2`, `method3`), each exploring different feature engineering strategies, algorithms, or preprocessing pipelines to solve the same binary classification problem.

---

## 🎯 Problem Statement

> **Can we predict whether a Kickstarter campaign will be successfully funded — before or during its run — using structured campaign metadata?**

This is a **binary classification** task:
- `1` → **Successful** (campaign met or exceeded its funding goal)
- `0` → **Failed** (campaign did not reach its funding goal)

Accurate predictions benefit:
- **Creators** — optimize campaign setup (goals, duration, category) before launching
- **Backers** — assess project viability before committing funds
- **The platform** — surface high-potential projects to the right audience

---

## 📊 Dataset

**Source:** [Kickstarter Campaigns Dataset — Kaggle](https://www.kaggle.com/datasets/sripaadsrinivasan/kickstarter-campaigns-dataset)

The dataset contains metadata from thousands of real Kickstarter campaigns. Key fields include:

| Feature | Description |
|---------|-------------|
| `name` | Campaign title |
| `category` | Project category (e.g., Film, Technology, Games) |
| `main_category` | Top-level category grouping |
| `currency` | Currency of the funding goal |
| `deadline` | Campaign end date |
| `goal` | Funding target (in campaign currency) |
| `launched` | Campaign launch date |
| `pledged` | Total amount pledged by backers |
| `backers` | Number of backers |
| `country` | Country of origin |
| `usd_pledged` | USD-equivalent amount pledged |
| `usd_goal_real` | USD-equivalent funding goal |
| `state` | Outcome label — `successful`, `failed`, `canceled`, etc. |

> **Target variable:** `state` binarized to successful vs. failed, with canceled/suspended campaigns filtered out per method.

---

## 📁 Project Structure

```
KickStarter-Project-Success-Prediction/
│
├── method1.ipynb       # Approach 1 — Baseline modeling pipeline
├── method2.ipynb       # Approach 2 — Alternative feature engineering / model
├── method3.ipynb       # Approach 3 — Advanced / ensemble approach
└── README.md           # Project documentation
```

> **Note:** The Kaggle dataset is not included in this repo. Download it from the link above and place it in the project root before running the notebooks.

---

## 🔬 Methodology

All three methods share a common high-level pipeline, with variations in feature engineering, model selection, and hyperparameter strategies:

```
Raw Kickstarter Data
        │
        ▼
  Data Cleaning
  (nulls, duplicates, state filtering)
        │
        ▼
  Feature Engineering
  (date features, goal scaling, encoding)
        │
        ▼
  Exploratory Analysis
  (distributions, class balance, correlations)
        │
        ▼
  Model Training
  (varies by method — see below)
        │
        ▼
  Evaluation
  (accuracy, precision, recall, F1, ROC-AUC)
        │
        ▼
  Insights & Cross-Method Comparison
```

### Common Preprocessing Steps
- Filtering `state` to binary classes (`successful` / `failed`)
- Parsing `launched` and `deadline` to extract **campaign duration in days**
- Log-transforming skewed features like `goal` and `usd_goal_real`
- One-hot encoding categorical variables (`category`, `country`, `currency`)
- Handling class imbalance where applicable

---

## 🤖 Models & Approaches

| Notebook | Approach | Models |
|----------|----------|--------|
| `method1.ipynb` | Baseline pipeline with standard feature set | Logistic Regression, Decision Tree |
| `method2.ipynb` | Enhanced feature engineering + alternative model | Random Forest, Naive Bayes, or SVM |
| `method3.ipynb` | Advanced approach with tuning / ensembles | Gradient Boosting, XGBoost, or model stacking |

Each notebook is independently runnable and self-contained. Comparing across methods reveals which feature sets and algorithms generalize best to unseen campaigns.

---

## 🔑 Key Engineered Features

Beyond raw fields, the following derived features typically prove most informative:

- **`campaign_duration`** — days between launch and deadline
- **`log_goal`** — log-scaled USD goal (reduces skew from outlier campaigns)
- **`launch_month` / `launch_weekday`** — temporal signals affecting backer engagement
- **`category_encoded`** — one-hot or label-encoded project categories
- **`goal_per_day`** — funding target divided by campaign length (daily pressure metric)

---

## ⚙️ Installation

### Prerequisites
- Python 3.8+
- Jupyter Notebook or JupyterLab

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/Gaurav3099/KickStarter-Project-Success-Prediction.git
   cd KickStarter-Project-Success-Prediction
   ```

2. **Create a virtual environment (recommended)**
   ```bash
   python -m venv venv
   source venv/bin/activate        # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install numpy pandas matplotlib seaborn scikit-learn xgboost imbalanced-learn jupyter
   ```

4. **Download the dataset**
   - Visit the [Kaggle dataset page](https://www.kaggle.com/datasets/sripaadsrinivasan/kickstarter-campaigns-dataset)
   - Download the CSV and place it in the project root directory

5. **Launch Jupyter**
   ```bash
   jupyter notebook
   ```

---

## 🚀 Usage

Run the notebooks in any order — each is self-contained:

```
method1.ipynb  →  Baseline model pipeline
method2.ipynb  →  Alternative feature/model approach
method3.ipynb  →  Advanced/ensemble approach
```

Update the dataset path at the top of each notebook if needed:
```python
df = pd.read_csv("ks-projects-201801.csv")   # adjust filename as needed
```

Then run all cells via `Kernel → Restart & Run All`.

---

## 📉 Results

Each method produces its own evaluation metrics. Typical benchmarks for Kickstarter success prediction fall in the following ranges:

| Metric | Typical Range |
|--------|--------------|
| Accuracy | 65% – 80% |
| F1 Score | 0.65 – 0.82 |
| ROC-AUC | 0.70 – 0.87 |

> For exact per-method metrics, refer to the evaluation cells at the bottom of each notebook.

**Key predictive signals commonly found:**
- Funding goal amount — lower, realistic goals succeed more often
- Project category — Technology, Design, and Games tend to outperform
- Campaign duration — shorter, focused campaigns with urgency often perform better
- Country of origin and currency type

---

## 🛠️ Dependencies

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading and wrangling |
| `numpy` | Numerical operations |
| `matplotlib` / `seaborn` | Visualization and EDA plots |
| `scikit-learn` | ML models, preprocessing, metrics |
| `xgboost` | Gradient boosted trees (method3) |
| `imbalanced-learn` | SMOTE / class imbalance handling |
| `jupyter` | Interactive notebook environment |

---

## 📄 License

This project is licensed under the **MIT License**.

---

