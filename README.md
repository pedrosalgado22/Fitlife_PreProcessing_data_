# FitLife — Preprocessing Smartwatch Data for User Segmentation

A data preprocessing project preparing FitLife's raw smartwatch activity and wellness data for user segmentation by building a clean, coherent, user-level Analytical-Based Table (ABT) and providing initial insights into user activity patterns and health behaviours.

**Course:** Data Preprocessing 2025/2026 — Nova IMS, Universidade Nova de Lisboa

---

## Project Objective

*Prepare FitLife's raw smartwatch data for advanced analytical methods by building a complete preprocessing pipeline — treating outliers, imputing missing values, verifying coherence, constructing a user-level Analytical-Based Table (ABT) and providing initial insights into user activity patterns and health behaviours through data visualisation.*

---

## Repository Contents

1. `Project Description.pdf` — course guidelines and project requirements
2. `Group_P_DP_Report.pdf` — final report documenting all preprocessing steps and interpretation
3. `Project_Data.csv` — raw transactional dataset provided by the professor
4. `FitLife_preprocessed_final.csv` — cleaned and preprocessed dataset exported from the notebook
5. `PPDProject.ipynb` — full preprocessing pipeline (exploration, outliers, missing values, coherence, export)
6. `LICENSE` — MIT License

---

## Data

- **Source:** FitLife smartwatch tracking systems (transactional database provided by the professor)
- **Scope:** User activities and wellness metrics across various types of exercises, reflecting overall performance and demographics
- **Variables (20):** Covering workout preferences, physical endurance, social information and vital data

| Variable | Description |
|---|---|
| `activity_id` | Unique activity record ID |
| `timestamp` | Timestamp of the activity (local time) |
| `user_id` | User identifier |
| `activity_type` | Type of activity |
| `duration_min` | Duration of the activity in minutes |
| `distance_km` | Distance covered in kilometres (NaN for non-distance activities or GPS dropout) |
| `calories` | Energy expenditure in kilocalories |
| `avg_hr_bpm` | Average heart rate during activity (bpm) |
| `max_hr_bpm` | Maximum heart rate during activity (bpm) |
| `rpe` | Perceived exertion on 1–10 scale |
| `age` | User age in years |
| `gender` | Self-reported gender |
| `height_cm` | User height in centimetres |
| `weight_kg` | User weight in kilograms |
| `bmi` | Body Mass Index |
| `education_level` | Highest education level attained |
| `profession` | Profession/occupation |
| `marital_status` | Marital status |
| `city` | City of residence (UK) |
| `device_model` | Smartwatch model |

---

## Methodology

1. **Initial Descriptive Analysis** — summary statistics for all numeric variables, identification of missing values (7,071 total) and early red flags (e.g., `max_hr_bpm` of 230, `rpe` exceeding the 1–10 scale)
2. **Categorical Standardisation** — unified inconsistent spellings in `education_level` (e.g., two different forms of "Bachelor's")
3. **Outlier Detection and Treatment** — boxplot analysis for all numeric variables followed by domain-specific trimming rules (`rpe` 1–10, `max_hr_bpm` ≤ 190, `avg_hr_bpm` ≤ 156, `calories` ≤ 905, `distance_km` ≤ 20, `duration_min` ≤ 91)
4. **Missing Value Imputation** — `distance_km` set to 0 for non-distance activities (swim, strength training, HIIT, row, yoga) and KNN-imputed for movement activities (run, walk, cycle, hike); `height_cm` and `weight_kg` recovered using the BMI formula; `profession` filled with "Unknown"; correlation checks to ensure imputation did not distort the data
5. **Coherence Checks** — user-level consistency (single values for age, gender, height, weight, BMI, education, profession, marital status, city, device model), physiological plausibility (heart rate, BMI, anthropometric ranges), logical validation (duration > 0, distance ≥ 0, calories ≥ 0, calorie efficiency), categorical validity and duplicate detection
6. **Analytical-Based Table (ABT) Construction** — aggregation from transactional to user-level in SAS Viya, producing a 45-variable ABT covering identifiers, demographics, activity volume, intensity, efficiency and diversity
7. **Multicollinearity Assessment** — correlation matrix on 15 core numeric behaviour metrics; correlations documented and highlighted, all variables retained per project guidelines
8. **Data Visualisations** — 3-page Power BI report with DAX measures and navigation buttons, validating that the cleaned and engineered variables behave as expected

Full detail in [`Group_P_DP_Report.pdf`](./Group_P_DP_Report.pdf).

---

## Key Findings

The dataset started with 20 variables and 7,071 missing values. After treating outliers, imputing missing values and applying coherence rules, the data was consolidated into a **45-variable user-level ABT** ready for clustering.

Multicollinearity was assessed on 15 core numeric features — volume/workload variables are positively correlated as expected, heart-rate variables correlate with each other, and rate/efficiency variables add complementary dimensions. All variables were retained; correlations were documented to guide downstream analysis.

The Power BI report confirms that the final ABT is coherent, interpretable and contains enough behavioural variability to justify segmentation — users differ meaningfully in engagement, intensity, efficiency and activity diversity.

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python 3 | Core preprocessing language |
| Jupyter Notebook | Interactive computing (VS Code + Google Colab) |
| `pandas` | Data manipulation |
| `numpy` | Numerical operations |
| `matplotlib` / `seaborn` | Visualisation |
| `scipy.stats` | Statistical testing |
| `statsmodels` | Statistical analysis |
| `feature_engine` | Outlier treatment |
| `scikit-learn` | KNN imputation, preprocessing |
| SAS Viya | ABT construction and variable engineering |
| Power BI | Data visualisations and DAX measures |
| Microsoft Excel | Data exporting, visualisation and data integrity |

---

## Report

Full methodology, results and interpretation of each step are in [`Group_P_DP_Report.pdf`](./Group_P_DP_Report.pdf).

---

## Authors

| Name | Student Number |
|---|---|
| Pedro Ramalho | 20231509 |
| Pedro Salgado | 20241703 |

---

## License

This project is licensed under the MIT License — see the [`LICENSE`](./LICENSE) file for details.

---

*Nova IMS — Universidade Nova de Lisboa | Data Preprocessing 2025/2026*
