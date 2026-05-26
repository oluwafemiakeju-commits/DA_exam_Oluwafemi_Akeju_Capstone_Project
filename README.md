# 🚗 Fleet Maintenance Analytics — CS1: Exploratory & Inferential Analytics

> **Data Analytics 1 — Take-Home Examination | April 2026**
> Lagos Business School · EMBA-31 Programme · Prof Bongo Adi

---

## 📋 Overview

This repository contains the complete, reproducible analytical work submitted for **Case Study 1 (CS1) — Exploratory & Inferential Analytics** of the Data Analytics 1 Take-Home Examination at Lagos Business School.

The study addresses a real operational question faced at **KK Leasing Limited**, a third-party vehicle leasing and logistics company based in Lagos, Nigeria:

> *What are the principal drivers of fleet maintenance cost at KK Leasing, and how can they be predicted and controlled to protect asset profitability?*

The analysis draws on **6,986 line-item maintenance records** spanning **153 vehicles** and **11 months** (January–November 2023), extracted from the company's **Instanta ERP system**.

---

## 👤 Author

| Field | Detail |
|---|---|
| **Name** | Akeju, Oluwafemi Olusoji |
| **Role** | Chief Operating Officer, KK Leasing Limited |
| **Programme** | Executive MBA (EMBA-31) |
| **Institution** | Lagos Business School |
| **Assessment** | Data Analytics 1 — CS1 Take-Home Examination, April 2026 |
| **GitHub** | [@oluwafemiakeju-commits](https://github.com/oluwafemiakeju-commits) |

---

## 🌐 Live Published Report

The rendered HTML report is published on RPubs and can be accessed at:

**👉 [https://rpubs.com/oluwafemiakeju/kk-leasing-fleet-analytics-cs1](https://rpubs.com/oluwafemiakeju/kk-leasing-fleet-analytics-cs1)**

---

## 📁 Repository Structure

```
📦 DA_exam_Oluwafemi_Akeju_Capstone_Project/
 │
 ├── 📂 files/                                      ← Main project folder
 │    ├── 📄 KKLeasing_CS1_Analytics.qmd            ← Quarto source document (main submission)
 │    └── 📊 Take_Home_Exam_Data_-_Final.xlsx        ← Primary dataset (2 sheets, 153 vehicles)
 │
 ├── 📄 Exam Files.Rproj                            ← RStudio project file
 ├── 🗂️  .RData                                     ← R workspace (auto-saved session data)
 ├── 🗂️  .Rhistory                                  ← R console session history
 └── 📄 README.md                                   ← This file
```

> ⚠️ **Important for reproducibility:** When rendering the `.qmd`, ensure `KKLeasing_CS1_Analytics.qmd` and `Take_Home_Exam_Data_-_Final.xlsx` are in the **same directory**. Open the project via `Exam Files.Rproj` so RStudio sets the correct working directory automatically.

---

## 📊 Dataset Description

The primary dataset is **`Take_Home_Exam_Data_-_Final.xlsx`** (inside the `files/` folder), containing two sheets:

### Sheet 1 — Maintenance Record (6,986 rows × 14 columns)

| Variable | Type | Description |
|---|---|---|
| `#` | Integer | Row index |
| `Maintenance No` | Integer | Unique work order identifier |
| `Item No` | Integer | Line item number within a work order |
| `Posted Date` | Date | Date maintenance was approved and posted |
| `Month` | Categorical | Month of posting (Jan–Nov 2023) |
| `Cost Category` | Categorical | **Parts Cost** or **Labour** |
| `Vehicle Make` | Categorical | Brand of vehicle (9 makes) |
| `Vehicle Reg No` | Categorical | Anonymised registration plate |
| `Maintenance Category` | Categorical | Type of repair (22 categories) |
| `Client` | Categorical | Anonymised client code (Client 001–006) |
| `Workshop` | Categorical | Workshop that performed the repair |
| `Item Description` | Text | Description of part or labour item |
| `Quantity` | Numeric | Quantity of item consumed |
| `Approved Amount` | Numeric (₦) | **Primary outcome variable** — cost per line item |

### Sheet 2 — Vehicle Details (153 rows × 7 columns)

| Variable | Type | Description |
|---|---|---|
| `Vehicle Reg No` | Categorical | Join key to Sheet 1 |
| `Vehicle Make` | Categorical | Brand of vehicle |
| `Age (Years)` | Integer | Vehicle age at time of analysis |
| `Budget (₦)` | Numeric | Allocated maintenance budget for the period |
| `Distance Covered (km)` | Numeric | Total km driven during the period |
| `Maintenance Cost` | Numeric (₦) | Total maintenance cost for the period |
| `Cost/Km` | Numeric (₦/km) | Derived cost-efficiency metric |

**Data provenance:** Extracted from KK Leasing Limited's Instanta ERP system, January–November 2023. Client names anonymised to generic codes (Client 001–006). Management approval obtained prior to use. No personally identifiable information is included.

---

## 🔬 Analytical Techniques Applied

| # | Technique | Textbook Reference | Business Question Addressed |
|---|---|---|---|
| 1 | **Exploratory Data Analysis (EDA)** | Ch. 4 | What does the cost landscape look like? Where are the outliers and data quality issues? |
| 2 | **Data Visualisation** | Ch. 5 | What patterns emerge across categories, vehicle makes, months, and workshops? |
| 3 | **Hypothesis Testing** (ANOVA) | Ch. 6 | Do costs differ significantly by maintenance category and by vehicle make? |
| 4 | **Correlation Analysis** | Ch. 8 | How strongly are vehicle age, budget, distance, and total cost related? |
| 5 | **Linear Regression** (OLS) | Ch. 9 | Can total maintenance cost be predicted from vehicle characteristics? |

All techniques are implemented in **both R and Python** within panel-tabset code blocks in the Quarto document.

---

## 🛠️ How to Reproduce This Analysis

### Prerequisites

| Tool | Version | Download |
|---|---|---|
| R | ≥ 4.3 | https://www.r-project.org |
| RStudio | ≥ 2023.09 | https://posit.co/downloads |
| Quarto | ≥ 1.4 | https://quarto.org |
| Python | ≥ 3.10 | https://www.python.org |

### Step 1 — Clone the Repository

```bash
git clone https://github.com/oluwafemiakeju-commits/DA_exam_Oluwafemi_Akeju_Capstone_Project.git
cd DA_exam_Oluwafemi_Akeju_Capstone_Project
```

### Step 2 — Install R Packages

Run this once in your R console:

```r
install.packages(c(
  "readxl", "tidyverse", "ggplot2", "scales", "corrplot",
  "ggcorrplot", "knitr", "kableExtra", "moments", "car",
  "broom", "ggpubr", "patchwork", "RColorBrewer", "viridis",
  "ggrepel", "emmeans", "lmtest", "nortest", "psych",
  "reticulate"
))
```

### Step 3 — Install Python Packages

The project uses `reticulate` to run Python chunks inside Quarto. Install the required Python packages via R:

```r
reticulate::py_install(c(
  "pandas",
  "numpy",
  "matplotlib",
  "seaborn",
  "scipy",
  "scikit-learn",
  "statsmodels",
  "openpyxl"
))
```

Or directly from your terminal:

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn statsmodels openpyxl
```

### Step 4 — Open the RStudio Project

Double-click **`Exam Files.Rproj`** to open the project in RStudio. This automatically sets the working directory correctly so all file paths resolve without modification.

### Step 5 — Render the Quarto Document

Navigate to `files/KKLeasing_CS1_Analytics.qmd`, then:

- In RStudio: press **`Ctrl + Shift + K`** (Render)
- Or from the terminal:

```bash
cd files
quarto render KKLeasing_CS1_Analytics.qmd
```

This produces a fully self-contained HTML file.

### Step 6 — Publish to RPubs *(for reference)*

In the RStudio Viewer pane, click the blue **Publish** button → select **RPubs** → log in → use slug `kk-leasing-fleet-analytics-cs1` → click **Publish**.

---

## 📈 Key Findings Summary

| Finding | Detail |
|---|---|
| **Total spend (Jan–Nov 2023)** | ₦93.3 million across 153 vehicles |
| **Top cost category** | Tyre Purchase — ₦18.2m (19.5% of total spend) |
| **Second largest category** | Routine Maintenance — ₦12.4m (13.3%) |
| **Peak spend months** | May, June, July, August (mid-year surge) |
| **Dominant vehicle make** | Toyota — 55% of fleet, 70% of total spend |
| **Age–cost correlation** | Pearson r = 0.57 · Spearman ρ = 0.70 |
| **ANOVA — by maintenance category** | F >> 1, p < 0.001 — categories differ significantly in cost |
| **ANOVA — by vehicle make** | F > 11, p < 0.001 — make significantly affects per-event cost |
| **Regression model fit** | Adjusted R² ≈ 0.54 |
| **Age effect (regression)** | Each +1 year of vehicle age → ~8% higher maintenance cost |
| **GAC vs Toyota** | GAC vehicles cost ~33% less than Toyota equivalents |
| **Lexus vs Toyota** | Lexus vehicles cost ~32% more than Toyota equivalents |
| **Workshop cost differential** | In-house workshops are cheaper than third-party for most categories |

---

## 🎯 Strategic Recommendation

> KK Leasing should implement a **Vehicle Lifecycle Governance Policy** with three pillars:
>
> 1. **Hard fleet age ceiling of 10 years** — supported by the regression age coefficient showing compounding cost increases after year 8
> 2. **Category-differentiated maintenance budget** — with elevated provisioning for Tyre Purchase and Engine events, supported by ANOVA and EDA findings
> 3. **Strategic expansion of in-house workshop capacity** — to capture the cost differential currently flowing to third-party vendors

These three interventions, applied together, are estimated to reduce total annual maintenance expenditure by **15–25%** while improving SLA reliability.

---

## 📚 References & Citation

**To cite this repository:**
```
Akeju, O. O. (2026). Fleet maintenance analytics — CS1 Exploratory & Inferential 
Analytics [GitHub repository]. 
https://github.com/oluwafemiakeju-commits/DA_exam_Oluwafemi_Akeju_Capstone_Project
```

**Course textbook (required citation):**
```
Adi, B. (2026). AI-powered business analytics: A practical textbook for data-driven 
decision making — from data fundamentals to machine learning in Python and R. 
Lagos Business School / markanalytics.online. https://markanalytics.online
```

---

## ⚖️ Data Privacy Statement

All client names in this dataset have been anonymised to generic codes (Client 001–006). Vehicle registration numbers contain no personally identifiable information. This repository is published for academic purposes only, with written management approval from KK Leasing Limited. Raw financial data that the company treats as confidential has not been published.

---

## 🤖 AI Usage Disclosure

Claude (Anthropic) was used to assist with R and Python code syntax, `ggcorrplot`/`kableExtra`/`statsmodels` function calls, and Quarto document formatting. All analytical decisions, business interpretations, technique selections, strategic recommendations, and data collection were conducted independently by the author. A full AI usage disclosure statement is included in the Appendix of the submitted Quarto document.

---

*Lagos Business School · Data Analytics 1 · EMBA-31 · April 2026*
