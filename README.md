# Predicting Students’ E-Learning Continuance Intention Using Machine Learning

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21944837.svg)](https://doi.org/10.5281/zenodo.21944837)

**Archived release DOI:** `10.5281/zenodo.21944837`

## Cross-Dataset Validation and a Data-Driven Educational Intervention Framework

This repository contains the complete analytical workflow for the study:

**“Predicting Students’ E-Learning Continuance Intention Using Machine Learning: Cross-Dataset Validation and a Data-Driven Educational Intervention Framework.”**

The project investigates whether students’ continuance intention to use e-learning can be predicted using a compact and interpretable machine-learning model and whether the resulting model can retain predictive performance when applied to an independent dataset without retraining.

The study also develops a data-driven educational intervention framework that converts predicted continuance intention into decision-support signals while preserving human oversight and avoiding causal interpretation of predictive relationships.

---

## Study Overview

Three independent datasets related to e-learning continuance intention were initially examined.

### Dataset B — Model Development

Dataset B contains **368 responses** and was used exclusively for model development and internal evaluation.

The original study measured:

- Perceived Educational Support (PEdS)
- Perceived Emotional Support (PEmS)
- Perceived Usefulness (PU)
- Expectation Confirmation (CON)
- Satisfaction (SAT)
- Continuance Intention (CI)

The primary cross-dataset predictive model uses:

```text
Predictors: CON + SAT
Target: CI
```

---

## Dataset EFL — External Validation
Dataset EFL contains 435 responses and was used exclusively for external validation.

The dataset was not used for:

model training,
hyperparameter tuning,
model selection,
or feature selection.

The final model trained on Dataset B was applied directly to Dataset EFL without retraining or fine-tuning.

The raw participant-level EFL dataset is not redistributed in this public repository.

Researchers wishing to reproduce the external validation must obtain the dataset from the original study or its corresponding authors and place the raw .sav file in:

`data/datasets_EFL/`

Additional information about data provenance and availability is provided in:

`docs/DATA_SOURCES.md`
### Dataset C — Excluded Candidate Dataset
A third dataset containing 166 records was evaluated as a candidate external dataset.

Quality-control analysis identified:

43 unique complete rows
123 additional duplicated rows
74.1% additional duplicate records

Because the available file contained extensive duplication and the independence of duplicated observations could not be established, Dataset C was excluded before model development or validation.

This exclusion concerns only the data file available for the present analysis and should not be interpreted as an assessment of the validity of the original published study.

## Construct Harmonization
Cross-dataset validation required conceptually comparable predictors and outcomes.

Three common constructs were harmonized between Dataset B and Dataset EFL:

Expectation Confirmation (CON)
Satisfaction (SAT)
Continuance Intention (CI)

Composite scores were calculated as the mean of the corresponding three questionnaire items.

Standardized Mean Differences between datasets were:

Construct	SMD
CON	0.027
SAT	0.125
CI	0.108

The harmonization procedure was intended to support practical predictive transfer and should not be interpreted as formal proof of measurement invariance.

## Machine-Learning Models
Five regression algorithms were evaluated:

Linear Regression
K-Nearest Neighbors Regression
Decision Tree Regression
Random Forest Regression
Gradient Boosting Regression

Model selection was based on 5-fold cross-validation RMSE calculated only on the Dataset B training data.

The internal test set was not used for model selection.

### Selected Model
Linear Regression achieved the lowest mean cross-validation RMSE:

CV MAE  = 0.3174
CV RMSE = 0.4721
CV R²   = 0.6067

The final model was therefore selected before evaluation on the internal test set.

### Internal Test Performance
MAE  = 0.3254
RMSE = 0.5315
R²   = 0.5941

The final model was subsequently fitted on all 368 Dataset B observations before external validation.

Final model coefficients:

Intercept = 0.8899
CON       = 0.1917
SAT       = 0.5930

These coefficients represent predictive associations and should not be interpreted as causal effects.

## External Validation
The frozen final model was applied directly to all 435 Dataset EFL observations.

External-validation performance:

MAE  = 0.2235
RMSE = 0.3573
R²   = 0.5705

Because the variability of CI differs between Dataset B and Dataset EFL, absolute error metrics should not be interpreted as direct evidence that external performance is better than internal performance.

The relatively stable R² provides evidence of predictive transportability between the two datasets examined in this study.

### Sensitivity Analysis
External validation was repeated under two additional data-quality scenarios.

Scenario	N	MAE	RMSE	R²
Primary external validation	435	0.2235	0.3573	0.5705
Remove High-Risk responses	352	0.2677	0.3964	0.5495
Clean Only	264	0.2966	0.4241	0.5622

The results indicate that external predictive performance was not solely dependent on responses carrying the evaluated quality flags.

## Extended Predictor Analysis
Dataset B also contains:

PU
PEdS
PEmS

Five predictor sets were compared across the five machine-learning algorithms using repeated 5-fold cross-validation.

The analysis showed that adding PU, PEdS, and PEmS did not produce a stable and meaningful predictive improvement across model families.

Therefore, the simpler cross-dataset model:

CON + SAT → CI

was retained.

## Data-Driven Educational Intervention Framework
The final predictive model was incorporated into a decision-support framework.

The framework follows the sequence:

Student E-Learning Data
        ↓
CON + SAT
        ↓
Final Prediction Model
        ↓
Predicted Continuance Intention
        ↓
Intervention Priority
        ↓
Signal Profile
        ↓
Suggested Educational Action
        ↓
Human Review
        ↓
Follow-up and Reassessment
        ↓
Monitoring Cycle

Three relative intervention-priority levels were defined:

High Priority
Moderate Priority
Routine Monitoring

Signal profiles were based on relative levels of CON and SAT.

The thresholds used in the study were derived from the Dataset B distribution and are sample-specific.

They should not be interpreted as universal, diagnostic, clinical, or psychometric cut-offs.

The framework is intended as a human-in-the-loop decision-support system.

Predictive signals are not interpreted as evidence of causal effects, and suggested educational actions require contextual human review and future empirical evaluation.

## Repository Structure

```text
E_Learning_Continuance_ML/
│
├── data/
│   ├── dataset_B/
│   ├── datasets_EFL/
│   ├── excluded_datasets/
│   └── processed/
│
├── notebooks/
│   ├── 01_Data_Audit_and_Quality_Control_PATHS_FIXED_FINAL.ipynb
│   ├── 02_Construct_Harmonization.ipynb
│   ├── 03_Model_Development.ipynb
│   ├── 04_External_Validation.ipynb
│   ├── 05_Dataset_B_Extended_Predictor_Analysis_FIXED.ipynb
│   ├── 06_Results_Consolidation_for_Article.ipynb
│   └── 07_Data_Driven_Intervention_Framework.ipynb
│
├── models/
│   ├── Final_Linear_Regression_Model.joblib
│   └── Final_Model_Metadata.json
│
├── outputs/
│   ├── figures/
│   └── tables/
│
├── docs/
│
├── README.md
├── requirements.txt
├── `CITATION.cff`
├── `LICENSE`
└── .gitignore
```

## Notebook Workflow
The notebooks should be executed in numerical order.

### 01 — Data Audit and Quality Control
Performs:

missing-data checks,
response-pattern diagnostics,
straight-lining detection,
completion-time diagnostics,
duplicate-record analysis,
quality-flag creation.
### 02 — Construct Harmonization
Performs:

CON, SAT, and CI composite-score calculation,
cross-dataset construct comparison,
Standardized Mean Difference analysis,
correlation comparison,
Fisher’s z tests,
creation of model-ready datasets.
### 03 — Model Development
Performs:

Dataset B train/test splitting,
model tuning,
cross-validation,
algorithm comparison,
final model selection,
internal testing,
final model fitting and serialization.
### 04 — External Validation
Performs:

frozen-model application to Dataset EFL,
independent external validation,
data-quality sensitivity analyses.
### 05 — Extended Predictor Analysis
Evaluates the incremental predictive value of:

PU
PEdS
PEmS

across multiple model families.

### 06 — Results Consolidation
Consolidates the principal analytical outputs into:

`outputs/tables/Article_Master_Results.xlsx`
### 07 — Data-Driven Intervention Framework
Produces:

predicted CI-based priority levels,
CON/SAT signal profiles,
suggested decision-support actions,
intervention-framework tables,
intervention-framework figure.
## Reproducibility
The notebooks use portable project-root detection and do not depend on an absolute local path.

Key random operations use:

`random_state = 42`

where applicable.

The external-validation dataset is deliberately separated from model training and tuning.

## Data Availability
Some source datasets are subject to their original publication and distribution conditions.

Participant-level Dataset EFL files are not redistributed in this repository.

Instructions and source information for obtaining the required datasets are documented in:

`docs/DATA_SOURCES.md`
## Code Availability
The analytical code, trained model, derived non-restricted outputs, figures, and reproducibility notebooks are provided in this repository.

Repository URL:

https://github.com/ParisaGhahreman/E-Learning-Continuance-ML

Archived release DOI:

https://doi.org/10.5281/zenodo.21944837

## Citation
Citation information will be provided through:

`CITATION.cff`

after publication of the first archived release.

## License
The analytical code in this repository will be released under the license specified in:

`LICENSE`

Dataset files remain subject to the terms and conditions of their original sources.

## Disclaimer
This repository contains predictive analyses and a proposed educational decision-support framework.

The model does not establish causal relationships between Expectation Confirmation, Satisfaction, and Continuance Intention.

Intervention recommendations should not be implemented as fully automated decisions and require appropriate human review, contextual assessment, privacy protection, and empirical validation.
