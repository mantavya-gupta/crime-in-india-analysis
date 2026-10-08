# 🔍 Crime in India: Exploratory Data Analysis & Visualization

> A data-driven look at crime patterns across Indian States/UTs and districts using NCRB data.

**Team Members**

| Name | GitHub |
|------|--------|
| Mantavya Gupta | [@mantavya-gupta](https://github.com/mantavya-gupta) |
| Vinil Shah | [@vinilshah-source](https://github.com/vinilshah-source) |

**Repository:** `https://github.com/mantavya-gupta/crime-in-india-analysis 
                https://github.com/vinilshah-source/crime-in-india-analysis.git`
**Dataset:** [Crime in India (Kaggle, by Rajanand)](https://www.kaggle.com/datasets/rajanand/crime-in-india)

---

## 1. Project Definition

### Problem Statement
Crime statistics in India are published as large, dense tables that are hard to interpret. Policymakers, researchers and citizens cannot easily see **where** crime is concentrated, **how** it has changed over time, and **which** categories of crime are growing or declining.

### Objective
To clean, explore and visualize India's crime data (NCRB) so that patterns become clear and easy to interpret. The project aims to:

1. Analyse the **trend of crime over the years** at national and state level.
2. Identify **high-crime and low-crime States/UTs and districts**.
3. Compare **types of crime** (murder, rape, kidnapping, theft, dowry deaths, etc.).
4. Study **crimes against vulnerable groups** (women, children, SC/ST).
5. Present all findings through **clear, interactive visualizations**.

### Scope
- Descriptive and exploratory analysis (EDA) plus visualization.
- No claim of causation; the project reports patterns in the data only.

### Expected Deliverables
- Cleaned dataset and reproducible Jupyter notebooks
- A set of static and interactive visualizations
- A short insights report (in this README / `/reports`)
- (Optional) A Streamlit dashboard

---

## 2. Dataset & Use Case

### About the Dataset
The Kaggle dataset *Crime in India* is compiled from the **National Crime Records Bureau (NCRB)** and contains multiple CSV files with State/UT-wise and district-wise crime counts across several years (roughly 2001–2013). The files cover different themes such as:

- Crimes under the Indian Penal Code (IPC), district-wise
- Crimes against Scheduled Castes and Scheduled Tribes
- Crimes against women
- Crimes against children
- Other categories such as juveniles, victims, property stolen and recovered, etc.

> The exact file list and column names will be confirmed and documented in `docs/data_dictionary.md` after the first download and inspection.

Typical columns in the IPC district-wise file include: `STATE/UT`, `DISTRICT`, `YEAR`, `MURDER`, `ATTEMPT TO MURDER`, `RAPE`, `KIDNAPPING & ABDUCTION`, `DACOITY`, `ROBBERY`, `BURGLARY`, `THEFT`, `RIOTS`, `DOWRY DEATHS`, `TOTAL IPC CRIMES`, and others.

### Use Cases
| Use Case | Who Benefits |
|----------|--------------|
| Identify crime hotspots by State/District | Law enforcement, policy makers |
| Track long-term trends of specific crimes | Researchers, journalists |
| Understand crimes against women/children/SC-ST | NGOs, social-welfare departments |
| Support evidence-based resource allocation | Government planners |
| Build awareness through visual storytelling | General public, students |

### Data Preparation Plan
1. Load all required CSV files and inspect shape, dtypes, nulls, duplicates.
2. Standardize State/UT and district names (casing, spelling, merged/renamed states such as Andhra Pradesh/Telangana).
3. Remove aggregate rows (e.g., `TOTAL`) to avoid double counting.
4. Handle missing values and inconsistent column names across years.
5. Reshape data (wide → long) where needed for plotting.
6. Save the processed data in `data/processed/`.

### Known Limitations
- Data is reported/registered crime, so it reflects *reporting* as well as actual crime.
- Population figures are not included, so raw counts favour large states. If population data is added, it will be documented as an external source.
- District boundaries changed over the years, so district-level comparisons need care.

---

## 3. Planned Visualizations & Expected Outcomes

> The outcomes below are the questions each plot is designed to answer. Final findings will be filled in after analysis.

| # | Visualization | Library | What It Shows | Expected Outcome / Insight |
|---|---------------|---------|---------------|----------------------------|
| 1 | **Line chart**: total IPC crimes per year (India) | Matplotlib / Plotly | National trend over time | Whether overall crime is rising, falling or flat; identify spikes |
| 2 | **Horizontal bar chart**: Top 10 States/UTs by total crime | Seaborn | State ranking | Which states contribute most registered crime |
| 3 | **Heatmap**: State × Year crime counts | Seaborn | Intensity across states and years | Spot persistent hotspots and sudden changes |
| 4 | **Choropleth map** of India | Plotly / GeoPandas | Geographic spread of crime | Regional clusters (north, south, central, etc.) |
| 5 | **Stacked bar chart**: crime composition per year | Matplotlib | Share of crime types | Which categories dominate and how the mix evolves |
| 6 | **Multi-line chart**: Murder, Rape, Kidnapping, Dowry Deaths | Plotly | Trend comparison of serious crimes | Which serious crime grows fastest |
| 7 | **Bar/line charts**: crimes against women & children | Seaborn / Plotly | Trends for vulnerable groups | Direction and states most affected |
| 8 | **Grouped bar chart**: crimes against SC vs ST | Matplotlib | Comparison between groups | Relative scale and state concentration |
| 9 | **Box plot / violin plot**: district-wise distribution per state | Seaborn | Spread and outliers | Districts with unusually high crime within a state |
| 10 | **Correlation heatmap**: between crime types | Seaborn | Relationship between categories | Crime types that tend to occur together |
| 11 | **Treemap / sunburst**: State → District contribution | Plotly | Hierarchical share | Which districts drive a state's total |
| 12 | **Interactive dashboard** (optional) | Streamlit | Filter by year, state, crime type | Easy exploration for non-technical users |

### Planned Key Questions
- Which State/UT has the highest registered crime, and has it changed over time?
- Which crime categories have grown most between the first and last year of the data?
- Are crimes against women/children concentrated in specific regions?
- Which districts are consistent outliers within their state?

---

## 4. Tools & Python Libraries

| Category | Tools |
|----------|-------|
| Language | Python 3.10+ |
| Data handling | `pandas`, `numpy` |
| Static visualization | `matplotlib`, `seaborn` |
| Interactive visualization | `plotly`, `plotly.express` |
| Geospatial / maps | `geopandas`, `plotly` (India GeoJSON) |
| Dashboard (optional) | `streamlit` |
| Environment | Jupyter Notebook / JupyterLab, VS Code |
| Data source access | Kaggle website / `kaggle` CLI |
| Version control & collaboration | Git, GitHub (branches + pull requests) |
| Documentation | Markdown |

Install dependencies:
```bash
pip install -r requirements.txt
```

---

## 5. Repository Structure

```
crime-in-india-analysis/
├── README.md                  # Project proposal & documentation
├── requirements.txt
├── .gitignore
├── data/
│   ├── raw/                   # Original Kaggle CSVs (not modified)
│   └── processed/             # Cleaned datasets
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_eda.ipynb
│   └── 03_visualizations.ipynb
├── src/                       # Reusable helper functions
├── visuals/                   # Exported charts (PNG/HTML)
├── docs/
│   └── data_dictionary.md
└── reports/
    └── insights.md
```

---

## 6. Project Timeline

| Phase | Tasks | Owner |
|-------|-------|-------|
| Week 1 | Repo setup, proposal, dataset download & inspection | Both |
| Week 2 | Data cleaning and preprocessing | Mantavya |
| Week 3 | EDA and trend/state-level plots (1–5) | Mantavya |
| Week 3 | Vulnerable-group, district and correlation plots (6–11) | [Teammate] |
| Week 4 | Map, dashboard (optional), insights report, final documentation | Both |

---

## 7. Team Collaboration & Git Workflow

- Both members commit from **their own GitHub accounts** to the same repository.
- Branch naming: `feature/<short-name>` (e.g., `feature/data-cleaning`, `feature/choropleth-map`).
- Changes are merged into `main` through **pull requests** reviewed by the other member.
- Commit message style: `type: short description` (e.g., `feat: add state-year heatmap`, `docs: update data dictionary`).

---

## 8. References

- Kaggle dataset: https://www.kaggle.com/datasets/rajanand/crime-in-india
- National Crime Records Bureau (NCRB): https://ncrb.gov.in
- Pandas, Matplotlib, Seaborn, Plotly and GeoPandas official documentation

---

## 9. License & Acknowledgements
Data courtesy of NCRB via Kaggle user *Rajanand*. This project is for educational purposes.
