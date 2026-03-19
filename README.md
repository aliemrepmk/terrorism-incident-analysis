# Predicting and Classifying Terrorism Incidents

> *Ali Emre Pamuk · Faruk Kaplan · Mert Altekin*

This project leverages machine learning techniques to analyze, predict, and classify global terrorism incidents using Python and Scikit-Learn. The goal is to transition security analytics from a **reactive** to a **proactive** stance by building models capable of predicting attack patterns and execution outcomes.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Problem Definition](#problem-definition)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Methodology](#methodology)
  - [Data Preprocessing](#data-preprocessing)
  - [Algorithms Evaluated](#algorithms-evaluated)
- [Results](#results)
  - [Attack Outcome Prediction](#attack-outcome-prediction-binary-classification)
  - [Attack Type Classification](#attack-type-classification-multi-class)
- [Future Work](#future-work)
- [Getting Started](#getting-started)

---

## Project Overview

Terrorism poses significant challenges to global security. Traditional security measures are often reactive, relying on post-incident analysis. By leveraging data analysis and machine learning, this project aims to:

- **Predict** whether a terrorism incident will be executed or foiled (binary classification)
- **Classify** the type of attack based on incident features (multi-class classification)

These insights can help security forces allocate resources more effectively and provide early warnings for high-risk scenarios.

---

## Problem Definition

Security forces face a critical data-processing bottleneck: large volumes of incident records spanning weapon types, geographic locations, and target profiles make it extremely difficult to identify patterns manually. Key challenges include:

- **High-dimensionality**: The GTD contains hundreds of features per incident.
- **Class imbalance**: Some attack types (e.g., Hijacking) are vastly underrepresented compared to others (e.g., Bombing/Explosion).
- **Temporal patterns**: Attack trends evolve over decades, making static models less reliable.

---

## Dataset

The analysis is based on the **Global Terrorism Database (GTD)**, maintained by the National Consortium for the Study of Terrorism and Responses to Terrorism (START).

| Property | Details |
|---|---|
| **Source** | START — University of Maryland |
| **Coverage** | 1970 – 2017 |
| **Total Incidents** | 180,000+ terrorist attacks |
| **Scope** | Domestic & international incidents worldwide |
| **Access** | Open-source |

The GTD provides systematic data on each incident including attack type, weapons used, target type, location, group responsible, and execution/foiled outcome.

---

## Project Structure

```
Predicting-Terrorism-Incidents/
│
├── attack_types.ipynb           # Multi-class classification of attack types
├── attack_outcome_prediction.ipynb  # Binary classification of attack outcome (executed vs. foiled)
├── Project-Presentation.pptx   # Slide deck summarizing objectives, methods & findings
├── requirements.txt             # Python dependencies
└── README.md
```

- **`attack_types.ipynb`** — Trains and evaluates multiple classifiers to predict the *category* of a terrorist attack (e.g., Bombing, Armed Assault, Assassination).
- **`attack_outcome_prediction.ipynb`** — Trains and evaluates models to predict whether a planned attack will be executed or foiled, framed as a binary classification problem.

---

## Methodology

### Data Preprocessing

Raw GTD data required extensive cleaning and transformation before model training:

1. **Handling Missing Values** — Imputation strategies applied to fill gaps in critical feature columns.
2. **Feature Engineering** — New derived features created to capture temporal trends and regional groupings.
3. **Categorical Encoding** — Nominal variables (e.g., country, attack type, weapon type) encoded using label/one-hot encoding.
4. **Feature Scaling** — Numerical features normalized/standardized to improve convergence for distance- and gradient-based models.

### Algorithms Evaluated

Both classification tasks benchmarked the following algorithms:

| Algorithm | Notes |
|---|---|
| **Logistic Regression** | Strong baseline; best performer for binary task |
| **Support Vector Machine (SVM)** | Effective for high-dimensional spaces |
| **Bernoulli Naive Bayes** | Fast probabilistic classifier; weakest overall |
| **k-Nearest Neighbors (kNN)** | Non-parametric, sensitive to feature scaling |
| **Decision Tree** | Interpretable; prone to overfitting |
| **Random Forest** | Ensemble method; top performer for multi-class task |
| **XGBoost** | Gradient-boosted ensemble; close to Random Forest on multi-class |
| **Artificial Neural Network (MLP)** | Multi-layer perceptron; captures non-linear patterns |

---

## Results

### Attack Outcome Prediction (Binary Classification)

Predicting whether a terrorism incident will be executed or foiled.

| Metric | Score |
|---|---|
| **Best Algorithm** | Logistic Regression |
| **Accuracy** | 89.4% |
| **Precision** | 90.1% |
| **Recall** | 98.7% |
| **F1-Score** | 94.2% |

> **Key Insight**: The high recall (98.7%) means the model is very effective at identifying attacks that were executed — a critical property for a real-world security application where false negatives are costly.

### Attack Type Classification (Multi-class)

Predicting which category of attack will be carried out.

| Algorithm | Accuracy |
|---|---|
| **Random Forest** | ~86% (Best) |
| **XGBoost** | ~85% |
| **SVM** | 83.2% |
| **Logistic Regression** | ~82% |
| **Bernoulli Naive Bayes** | 80.0% |

**Key observations:**
- Models performed **exceptionally well** on high-frequency classes like *Bombing/Explosion*.
- Performance dropped on **minority classes** such as *Hijacking* due to severe data imbalance.
- Random Forest and XGBoost outperformed all other methods, demonstrating the strength of ensemble approaches for this multi-class problem.

---

## Future Work

Several directions have been identified to improve model performance and real-world applicability:

1. **External Data Integration** — Incorporating socioeconomic indicators (GDP, poverty rates, political stability) and geopolitical context to improve predictive power.
2. **Natural Language Processing (NLP)** — Applying sentiment analysis and text mining to incident summary narratives for richer feature extraction.
3. **Real-Time Deployment** — Developing an interactive prediction and visualization dashboard for security analysts to support resource allocation decisions.
4. **Class Imbalance Techniques** — Exploring SMOTE, class-weighted losses, and other oversampling methods to improve recall on minority attack types.

---

## Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook or JupyterLab

### Installation

**1. Clone the repository:**
```bash
git clone https://github.com/aliemrepmk/terrorism-incident-analysis.git
cd terrorism-incident-analysis
```

**2. Set up a virtual environment (recommended):**
```bash
python -m venv env
source env/bin/activate      # On Windows: env\Scripts\activate
```

**3. Install the required packages:**
```bash
pip install -r requirements.txt
```

**4. Launch Jupyter Notebook:**
```bash
jupyter notebook
```

**5.** Open **`attack_types.ipynb`** to explore the attack type classification analysis, or **`attack_outcome_prediction.ipynb`** to explore the attack outcome prediction analysis.

---

## License

This project uses the **Global Terrorism Database (GTD)**, which is open-source and freely available for academic research. Please cite START/University of Maryland when referencing the dataset.

---