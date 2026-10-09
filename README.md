# Crime in India: Exploring NCRB Data

We're looking at how crime shows up in India's official records, across states, districts and years, using NCRB data. The goal is simple: take tables that are painful to read and turn them into charts people can actually understand.

## Team

| Name | GitHub |
|---|---|
| Mantavya Gupta | [@mantavya-gupta](https://github.com/mantavya-gupta) |
| Vinil Shah | [@vinilshah-source](https://github.com/vinilshah-source) |

**Repositories**
- https://github.com/mantavya-gupta/crime-in-india-analysis
- https://github.com/vinilshah-source/crime-in-india-analysis

**Dataset:** Crime in India on Kaggle, uploaded by Rajanand

---

## 1. Project Definition

### The problem

NCRB publishes crime numbers as huge tables. They're accurate, but hard to read. If you're a researcher, a journalist or just a curious citizen, it's tough to tell where crime is concentrated, how it has moved over the years, or which types of crime are going up and which are going down.

### What we want to do

Clean the NCRB data, explore it, and visualize it so the patterns are easy to see. In practice that means:

1. Looking at how crime has changed over time, both nationally and state by state.
2. Finding which States/UTs and districts report the most and the least crime.
3. Comparing different crime types: murder, rape, kidnapping, theft, dowry deaths and so on.
4. Taking a closer look at crimes against women, children, and SC/ST communities.
5. Showing all of this through clear, interactive visuals.

### Scope

This is descriptive and exploratory work. We're not trying to explain *why* crime happens or claim that one thing causes another. We only report what the data shows.

### What we plan to deliver

- A cleaned dataset and Jupyter notebooks anyone can rerun
- A set of static and interactive charts
- A short write-up of what we found (in this README and in `/reports`)
- A Streamlit dashboard, if time allows

---

## 2. Dataset and Use Cases

### About the data

The Kaggle dataset comes from the National Crime Records Bureau. It's a bundle of CSV files with State/UT-level and district-level crime counts, covering roughly 2001 to 2013. The files are grouped by theme:

- IPC crimes, district-wise
- Crimes against Scheduled Castes and Scheduled Tribes
- Crimes against women
- Crimes against children
- A few other files (juveniles, victims, property stolen and recovered, etc.)

We haven't gone through every file yet. Once we've downloaded and inspected everything, the exact file list and column names will go into `docs/data_dictionary.md`.

The district-wise IPC file usually has columns like STATE/UT, DISTRICT, YEAR, MURDER, ATTEMPT TO MURDER, RAPE, KIDNAPPING & ABDUCTION, DACOITY, ROBBERY, BURGLARY, THEFT, RIOTS, DOWRY DEATHS and TOTAL IPC CRIMES, plus a few more.

### Who could use this

| Use case | Who it helps |
|---|---|
| Spotting crime hotspots by state or district | Police, policy makers |
| Following long-term trends for a specific crime | Researchers, journalists |
| Understanding crimes against women, children and SC/ST groups | NGOs, social-welfare departments |
| Deciding where resources should go | Government planners |
| Making the numbers understandable to everyone | The general public, students |

### How we'll prepare the data

1. Load the CSVs and check shape, data types, nulls and duplicates.
2. Clean up State/UT and district names (casing, spellings, and states that were split or renamed, like Andhra Pradesh and Telangana).
3. Drop aggregate rows such as TOTAL so nothing gets counted twice.
4. Deal with missing values and column names that change from year to year.
5. Reshape from wide to long format where the plots need it.
6. Save the cleaned files in `data/processed/`.

### Limitations we're aware of

- This is *registered* crime. The numbers reflect how much gets reported and recorded, not only how much happens.
- The data has no population figures, so raw counts will make big states look worse. If we bring in population data later, we'll say where it came from.
- District boundaries changed over the years, so comparing districts across time needs some care.

---

## 3. Planned Visualizations

Each plot below is meant to answer a specific question. We'll fill in the actual findings after the analysis is done.

| # | Visualization | Library | What it shows | What we hope to learn |
|---|---|---|---|---|
| 1 | Line chart of total IPC crimes per year (India) | Matplotlib / Plotly | National trend | Is crime rising, falling or flat? Are there any spikes? |
| 2 | Horizontal bar chart, top 10 States/UTs by total crime | Seaborn | State ranking | Which states report the most crime |
| 3 | Heatmap of State × Year | Seaborn | Intensity across states and years | Persistent hotspots and sudden jumps |
| 4 | Choropleth map of India | Plotly / GeoPandas | Geographic spread | Regional clusters (north, south, central...) |
| 5 | Stacked bar chart of crime composition per year | Matplotlib | Share of each crime type | Which categories dominate and how the mix shifts |
| 6 | Multi-line chart: murder, rape, kidnapping, dowry deaths | Plotly | Trends of serious crimes | Which one is growing fastest |
| 7 | Bar/line charts for crimes against women and children | Seaborn / Plotly | Trends for vulnerable groups | Which direction they're heading and which states are hit hardest |
| 8 | Grouped bar chart, crimes against SC vs ST | Matplotlib | Comparison of the two groups | Relative scale and which states stand out |
| 9 | Box / violin plot of district-wise crime per state | Seaborn | Spread and outliers | Districts with unusually high crime for their state |
| 10 | Correlation heatmap between crime types | Seaborn | Relationships between categories | Which crimes tend to rise together |
| 11 | Treemap / sunburst, State → District | Plotly | Hierarchical share | Which districts make up most of a state's total |
| 12 | Interactive dashboard (optional) | Streamlit | Filters by year, state, crime type | Easy exploring for people who don't code |

### Questions we want to answer

- Which State/UT has the highest registered crime, and has that changed over time?
- Which crime categories grew the most between the first and last year in the data?
- Are crimes against women and children concentrated in particular regions?
- Which districts keep showing up as outliers within their state?

---

## 4. Tools and Libraries

| Category | Tools |
|---|---|
| Language | Python 3.10+ |
| Data handling | pandas, numpy |
| Static plots | matplotlib, seaborn |
| Interactive plots | plotly, plotly.express |
| Maps | geopandas, plotly (India GeoJSON) |
| Dashboard (optional) | streamlit |
| Environment | Jupyter Notebook / JupyterLab, VS Code |
| Getting the data | Kaggle website or kaggle CLI |
| Collaboration | Git and GitHub (branches + pull requests) |
| Documentation | Markdown |

To install the dependencies:

```bash
pip install -r requirements.txt
```

---

## 5. Repository Structure

```
crime-in-india-analysis/
├── README.md                  # Proposal and documentation
├── requirements.txt
├── .gitignore
├── data/
│   ├── raw/                   # Original Kaggle CSVs, left untouched
│   └── processed/             # Cleaned datasets
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   ├── 02_eda.ipynb
│   └── 03_visualizations.ipynb
├── src/                       # Helper functions we reuse
├── visuals/                   # Exported charts (PNG/HTML)
├── docs/
│   └── data_dictionary.md
└── reports/
    └── insights.md
```

---

## 6. Timeline

| When | What | Who |
|---|---|---|
| Week 1 | Set up the repo, write the proposal, download and inspect the data | Both |
| Week 2 | Data cleaning and preprocessing | Mantavya |
| Week 3 | EDA and the trend/state-level plots (1–5) | Mantavya |
| Week 3 | Vulnerable-group, district and correlation plots (6–11) | Vinil |
| Week 4 | Map, dashboard (if we get to it), insights report, final documentation | Both |

---

## 7. How We're Working Together

- We both commit from our own GitHub accounts to the same repo.
- Branches are named `feature/<short-name>`, for example `feature/data-cleaning` or `feature/choropleth-map`.
- Nothing goes into `main` without a pull request that the other person has looked at.
- Commit messages follow `type: short description`, like `feat: add state-year heatmap` or `docs: update data dictionary`.

---

## 8. References

- Kaggle dataset: https://www.kaggle.com/datasets/rajanand/crime-in-india
- National Crime Records Bureau: https://ncrb.gov.in
- Official docs for pandas, Matplotlib, Seaborn, Plotly and GeoPandas

---

## 9. License and Acknowledgements

The data comes from NCRB, shared on Kaggle by Rajanand. This project is for educational purposes only.
