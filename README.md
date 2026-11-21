# Global AQI: Geospatial Analysis & Time-Series Exploration

A GIS and data-analysis project for exploring daily Air Quality Index (AQI) patterns across countries. It is designed around the Kaggle dataset **AQI - Air Quality Index (Country wise Daily AQI)** by Azmine Toushik Wasi.

## Project goals
- Clean and validate date, country, AQI and status fields.
- Average multiple observations for each **country and date** (as the dataset author recommends).
- Explore global and country-level AQI patterns over time.
- Create interactive country-level choropleth maps.
- Summarize AQI status categories and identify high-AQI observations.
- Provide a simple baseline forecast for a selected country (optional).

## Dataset

Download the CSV from Kaggle:

[Kaggle: AQI - Air Quality Index](https://www.kaggle.com/datasets/azminetoushikwasi/aqi-air-quality-index-scheduled-daily-update)

The dataset page describes `data_date.csv` with these fields:
- `Date` — observation date
- `Country` — country name
- `Status` — AQI category/status
- `AQI Value` — numeric AQI value

The dataset page notes that multiple values may exist for the same country on the same date and recommends averaging by date and country. The project follows that instruction.

### Add the data
1. Download `data_date.csv` from Kaggle.
2. Place it in `data/raw/data_date.csv`.
3. Do not commit a large or restricted dataset to GitHub unless its licence and redistribution terms permit it. The source page states: Database: Open Database; contents © Original Authors. Review the dataset's current terms before redistribution.

## Quick start

```bash
# 1) Create and activate a virtual environment
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

# 2) Install dependencies
pip install -r requirements.txt

# 3) Run the analysis pipeline
python run_analysis.py
```

Outputs are written to `outputs/` and the cleaned country-date table to `data/processed/`.

## Interactive GIS map

After running the pipeline, open `outputs/maps/global_aqi_latest.html` in a browser. The map uses Plotly's country-level choropleth and ISO-3 country codes. Country names that cannot be matched are listed in `outputs/unmatched_countries.csv`.

## Optional country forecast

```bash
python forecast.py --country Pakistan --days 30
```

This is an educational baseline forecast, not an official air-quality warning or health advisory. A simple seasonal-naive/linear baseline is used so results are reproducible and transparent.

## Repository structure

```text
Global_AQI_GIS_Repository/
├── data/
│   ├── raw/                 # Put data_date.csv here (not committed)
│   └── processed/
├── notebooks/
│   └── exploration_template.ipynb
├── outputs/
│   ├── figures/
│   └── maps/
├── src/aqi_gis/
│   ├── __init__.py
│   ├── cleaning.py
│   ├── analysis.py
│   └── mapping.py
├── .gitignore
├── requirements.txt
├── run_analysis.py
└── forecast.py
```

## Suggested GIS questions
1. Which countries have the highest mean AQI on the latest available date?
2. How does AQI vary by country through time?
3. Which countries show recurring high-AQI periods?
4. Are there visible seasonal patterns in a country's daily AQI series?
5. How do country-level patterns differ across the available date range?

## Methodology and limitations
- Records are grouped by `Country` and `Date`; numeric AQI values are averaged.
- The status for each country-date is recalculated from the mean AQI using common US EPA AQI bands where possible. The original `Status` is retained as `Original Status` for comparison. AQI category systems can differ by source/country, so document the classification convention in any report.
- A country choropleth is a country-level visualization, not a city-level exposure map. The source data does not provide coordinates, stations, or subnational boundaries.
- Missing or unrecognized country names may not appear on the map.
- Forecasts extrapolate historical observations and should not be interpreted as validated predictions.

## Reproducibility
Record the dataset download date, Kaggle dataset version, Python version and any changes to this workflow in your project report.
