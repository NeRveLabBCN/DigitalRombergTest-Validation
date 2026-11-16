# Digital Romberg's Test — Validation

This repository contains the dataset requirements and reproducible Python analyses used to validate the Romberg balance score reported in the associated scientific publication. The analyses evaluate cross-sectional performance, test–retest reliability, associations with clinical scales, and longitudinal responsiveness.

## Study Design

The validation analyses are performed using a test-level dataset in which the Romberg score has already been computed. Each row represents one Romberg test, including eyes-open (`.0`) and eyes-closed (`.1`) conditions.

The notebook includes the following analyses:

- **Cross-sectional performance:** discrimination between controls and patients, controls and mildly affected patients, and mild versus moderate/severe clinical groups.
- **Clinical classification:** score distributions across pathology groups and balance/ataxia severity categories.
- **Test–retest reliability:** comparison of repeated tests within the specified time interval.
- **Clinical correlations:** association of the digital score with clinical scales and questionnaires.
- **Longitudinal assessment:** evaluation of score trajectories according to clinically meaningful changes in R-ODS.
- **Score change vs. MICARS-SARA:** assessment of clinical scale changes associated with score changes of 25–100%.

Feature extraction, score generation, and model training are not included in this repository; the analyses start from a dataset containing the precomputed score.

## Repository Structure

The repository is organised into input data, reproducible analysis code, and statistical outputs.

### Data

The notebook requires the following input datasets:

- `test_data_romberg_retrained_scores.csv`: Test-level dataset containing the precomputed `SCORE`, test and patient identifiers, pathology, clinical classifications, elapsed days, retest information, and R-ODS centile.
- `smwt_db_mg.scales_quest.csv`: Clinical scales and questionnaires recorded at the session level, linked through `ID_SESSION`.

**Note:** The notebook's introductory documentation names the score dataset `test_data_romberg_retrained_scores.csv`, whereas the setup cell currently defines `test_data_with_scores.csv`. Check that the filename in `SCORES_FILE` matches the dataset provided. The clinical scales section also reads `smwt_db_mg.scales_quest.csv` directly.

### Scripts

- `Romberg_score_validation.ipynb`: Main Jupyter notebook containing data loading, sample description, statistical analyses, visualisations, and report generation. It includes:
  - ROC curves, AUC, and performance metrics at the Youden-optimal threshold.
  - Score boxplots and group comparisons using Mann–Whitney tests.
  - Test–retest analyses, including paired t-test, Cronbach's alpha, Pearson correlation, ICC, repeatability coefficient, and Bland–Altman plots.
  - Spearman correlations between the score and clinical scales.
  - Longitudinal classification based on the R-ODS centile MCID (8 points) and linear mixed-effects models.
  - Analysis of MICARS-SARA changes associated with score changes of 25–100%.

### Results

The notebook generates statistical reports, figures, and tables for review. Output files are saved to the directory specified by `OUTPUT_DIR`.

Expected outputs include:

- `SCORE_performance_report_test.pdf`: Summary report including sample demographics, features used, ROC curves and performance tables, score distributions, clinical correlations, and test–retest results.
- `boxplot_score_<group>.png`: Score distributions across pathology and clinical classification groups.
- `scatter_score.png`: Scatter plots comparing the score with clinical variables.
- `longitudinal_data_QUESTIONNAIRE_R-ODS_centile_8.csv`: Pairwise longitudinal data and clinical change classification based on R-ODS.
- `lme_trends_QUESTIONNAIRE_R-ODS_centile_8.pdf`: Linear mixed-effects model trajectories for R-ODS and the score by longitudinal trend group.
- `score_change_pairs_SCALE_MICARS-SARA_total.csv`: Visit pairs with score changes between 25% and 100%, including corresponding MICARS-SARA changes.

Additional correlation matrices, imputation logs, and figures are also generated. Some output filenames are left empty in the notebook and must be specified before execution.

## Reproducibility

Before running the notebook, configure `DATA_DIR` and `OUTPUT_DIR`, verify the input filenames, and complete any empty output paths. The notebook's analysis parameters include a maximum test–retest interval of 150 days and a 21-day window for retrieving the closest available clinical scale value.

