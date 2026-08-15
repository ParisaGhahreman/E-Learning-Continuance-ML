# Data Sources and Availability

This document describes the provenance, role, availability, and redistribution status of the datasets used in this project.

The study initially examined three independent datasets related to students' continuance intention to use e-learning.

---

## Dataset B — Model Development Dataset

### Source Study

Xu, S., Wang, Y., & Luo, W. (2024).

**Hybrid SEM-ANN model for predicting undergraduates’ e-learning continuance intention based on perceived educational and emotional support.**

PLOS ONE, 19(12), e0308630.

Article DOI:

`10.1371/journal.pone.0308630`

### Official Raw Data

The original study publicly provides its participant-level data as:

**S1 Raw Data**

Official data DOI:

`10.1371/journal.pone.0308630.s002`

The original file is a CSV containing demographic variables and questionnaire responses for:

- Perceived Educational Support (PEdS)
- Perceived Emotional Support (PEmS)
- Perceived Usefulness (PU)
- Expectation Confirmation (CON)
- Satisfaction (SAT)
- Continuance Intention (CI)

### Sample Size

`N = 368`

### Role in the Present Study

Dataset B was used for:

- data-quality auditing,
- construct-score calculation,
- model development,
- hyperparameter tuning,
- cross-validation,
- internal testing,
- extended predictor analysis,
- final model fitting,
- and illustrative operationalization of the educational intervention framework.

### Expected Local File

For full reproduction, the raw CSV should be placed at:

```text
data/dataset_B/pone.0308630.s002.csv

---

Redistribution Status

The raw data are already publicly distributed by the original publisher.

Users are encouraged to obtain the original dataset from the official PLOS source using the DOI above to preserve provenance and ensure that the original publication remains the authoritative data source.

Dataset EFL — External Validation Dataset
Source Study

Xu, X., & Yang, C. (2026).

Explaining EFL students’ continuance intention to use e-learning through technology acceptance, expectation confirmation, and flow theory.

Scientific Reports, 16, 17462.

Article DOI:

10.1038/s41598-026-48311-x

Sample Size

N = 435

Constructs Available in the Original Study

The dataset contains constructs including:

Perceived Ease of Use (PEOU)
Perceived Usefulness (PU)
Expectation Confirmation (CON)
Satisfaction (SAT)
Perceived Enjoyment (PE)
Continuance Intention (CI)
Role in the Present Study

Dataset EFL was used exclusively for:

construct harmonization,
independent external validation,
and external-validation sensitivity analysis.

Dataset EFL was not used for:

model training,
model selection,
hyperparameter tuning,
or feature selection.

The final model developed using Dataset B was applied to Dataset EFL without retraining or fine-tuning.

Data Availability

The original Scientific Reports article states that the data supporting the study are available from the corresponding author upon request.

Therefore, the participant-level raw dataset is not redistributed through this public repository.

Expected Local File

After obtaining the data legitimately from the original source or corresponding author, the raw SPSS file should be placed in:

data/datasets_EFL/

The analysis used a local file with the following expected filename:

Raw Data_Investigating the Predictive Factors Influencing EFL Students' Continuance Intention to Use E-Learning.sav
Repository Policy

The .sav file is excluded from version control through .gitignore.

Participant-level processed files derived from Dataset EFL are also excluded from the public repository.

This allows the analytical workflow to be documented without redistributing data for which public redistribution permission has not been established.

Dataset C — Excluded Candidate Dataset
Source Study

Begum, N. F., & Venkatesan, D. (2026).

Understanding continuance intention towards e-learning platforms: a structural model based on expectation confirmation and individual innovativeness.

Frontiers in Education, 11, 1892980.

Article DOI:

10.3389/feduc.2026.1892980

Original Sample Size

N = 166

Constructs

The source study examined constructs including:

Expectation Confirmation
Perceived Usefulness
Satisfaction
Individual Innovativeness
Continuance Intention
Initial Intended Role

Dataset C was initially evaluated as a candidate dataset for external validation.

Data-Quality Finding

Audit of the data file available for the present project identified:

Total rows:                166
Unique complete rows:       43
Additional duplicate rows: 123
Rows belonging to
duplicate groups:           160

The additional duplicate-row proportion was approximately:

74.1%

Because the independence of the duplicated observations could not be established reliably, Dataset C was excluded before model development or external validation.

Important Interpretation

This exclusion applies only to the data file available for the present analysis.

It should not be interpreted as an assessment of the scientific validity of the original published study.

Redistribution

The raw Dataset C files are not required for reproducing the final predictive model because Dataset C was excluded before modeling.

Researchers interested in the original data should consult the source article and its associated Supplementary Material or data repository.

Cross-Dataset Construct Harmonization

The primary predictive analysis required constructs that were sufficiently comparable across Dataset B and Dataset EFL.

The common constructs retained were:

Expectation Confirmation (CON)
Satisfaction (SAT)
Continuance Intention (CI)

The primary model was therefore defined as:

Predictors: CON + SAT
Target: CI

Perceived Usefulness (PU) was not included as a shared predictor because its item content was not sufficiently aligned across the two source studies for the intended cross-dataset predictive transfer.

Derived Data

The analysis generates processed and derived datasets under:

data/processed/

Derived Dataset B files may be included when their redistribution is consistent with the source-data terms.

Participant-level files derived from Dataset EFL are intentionally excluded from the public repository.

Summary statistics, model-performance tables, non-participant-level analytical outputs, and figures are stored under:

outputs/tables/
outputs/figures/
Reproducibility Note

The repository contains the complete analytical code and notebook sequence.

Full reproduction of the external-validation analysis requires legitimate access to Dataset EFL.

A user who has obtained the required source files should place them in the documented directories and execute the notebooks in numerical order:

01_Data_Audit_and_Quality_Control_PATHS_FIXED_FINAL.ipynb
02_Construct_Harmonization.ipynb
03_Model_Development.ipynb
04_External_Validation.ipynb
05_Dataset_B_Extended_Predictor_Analysis_FIXED.ipynb
06_Results_Consolidation_for_Article.ipynb
07_Data_Driven_Intervention_Framework.ipynb
Data Citation

Users of the original datasets should cite the corresponding source publications rather than citing this repository as the creator of those datasets.

This repository should be cited for the analytical workflow, cross-dataset validation procedure, trained model, derived results, and educational decision-support framework.