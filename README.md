# Global Air Quality Assessment & Geospatial Analysis

A GIS and data-analysis project structure for exploring country-level daily Air Quality Index (AQI) observations.

> **Project status:** Analysis-ready starter repository. Add the source CSV and run the workflow before reporting findings or presenting maps as completed deliverables.

## Project purpose
This project is designed to:
- summarize AQI observations by country and date;
- compare country-level air-quality patterns;
- examine monthly and seasonal variation;
- prepare charts and a country-level choropleth map.

## Data source
The project is designed for the Kaggle dataset **AQI - Air Quality Index (Country-wise Daily AQI)** by Azmine Toushik Wasi:

https://www.kaggle.com/datasets/azminetoushikwasi/aqi-air-quality-index-scheduled-daily-update

Expected source file: `Dataset/data_date.csv`

Expected columns:
- `Date` (or `DateTime`): observation date
- `Country`: country name
- `Status`: AQI category
- `AQI Value`: numeric AQI value

The dataset description notes that multiple observations may exist for the same country and date. This workflow therefore calculates the mean AQI for each country-date pair before further summaries.

## Repository structure
```text
Global_Air_Quality_GIS_Client_Project/
├── Dataset/          # Place data_date.csv here (not included)
├── Maps/             # Exported GIS maps
├── Analysis/         # Analysis scripts and tables
├── Visualizations/   # Charts
├── Notebooks/        # Optional Jupyter notebooks
├── outputs/          # Processed data and summary outputs
├── src/
│   └── analyze_aqi.py
├── requirements.txt
└── README.md
```

## Setup
```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
```

## Run the analysis
1. Download the Kaggle dataset from the source link above.
2. Extract `data_date.csv` into the `Dataset/` folder.
3. Run:
```bash
python src/analyze_aqi.py
```

The script creates:
- `outputs/aqi_country_daily_average.csv`
- `outputs/country_aqi_summary.csv`
- `outputs/monthly_aqi_average.csv`
- `Visualizations/global_aqi_distribution.png`
- `Visualizations/top_10_country_average_aqi.png`
- `Visualizations/monthly_aqi_trend.png`

## GIS mapping
For a choropleth map, obtain a country-boundary GeoJSON or shapefile from a reputable source (for example Natural Earth), ensure country names can be matched to the dataset's `Country` values, and use QGIS to join the processed country summary table by country name. Apply graduated symbology to the mean AQI field and export the finished map to `Maps/`.

Country-name mismatches (for example, alternate spellings) may require a documented lookup table before joining.

## Interpretation notes
- AQI category thresholds can differ by reporting standard. Use the `Status` values supplied with the dataset unless a specific AQI standard is explicitly selected and documented.
- The mean AQI is a summary statistic; it can hide short-lived pollution peaks.
- Missing dates do not mean zero pollution.
- Do not describe a country as the “most polluted” based on a single day. State the period and aggregation method.
- This repository does not include the original dataset or claim results until the analysis is run on the downloaded source data.

## Project contribution record
Document only work actually completed. Suggested sections for a final client handover include: task requirements, processing steps performed, maps/charts delivered, key findings supported by outputs, limitations, and revision date.

## Attribution
Dataset: Azmine Toushik Wasi, Kaggle, “AQI - Air Quality Index (Country wise Daily AQI)”. See the source link above. Dataset licensing and reuse conditions remain subject to the Kaggle dataset's stated license and original authors' terms.
