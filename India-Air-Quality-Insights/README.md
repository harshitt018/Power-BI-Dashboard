# India Air Quality Insights — Power BI Dashboard

An interactive Power BI dashboard for exploring air quality across Indian cities, comparing pollutants, analysing AQI trends, and understanding the relationship between air quality and environmental factors.

## Project Overview

**India Air Quality Insights** is a data analytics project built using Microsoft Power BI. It transforms air quality data into interactive visualizations that help users explore city-wise AQI, pollutant levels, seasonal changes, and environmental conditions.

The dashboard contains **three pages**, each focusing on a different aspect of air quality:

1. National AQI Overview
2. AQI Trends & Pollutant Analysis
3. Environmental Factors & AQI Analysis

## Dataset

- **Dataset name:** India Air Quality Dataset (2025–2026)
- **Source:** [Kaggle — India Air Quality Dataset](https://www.kaggle.com/datasets/yogeshm01/india-air-quality-dataset-20252026)
- **Dataset creator:** yogeshm01
- **Main file:** `enriched_aqi_dataset.csv`
- **Source dataset size:** 10,521 rows and 22 columns

### Dataset contents

The dataset contains information related to:

- Country, state, city, monitoring station, latitude and longitude
- Date and time information
- Air Quality Index (AQI) and AQI categories
- Pollutant identifiers and pollutant measurements
- Temperature, humidity and wind speed

The source dataset contains records from multiple years. The dashboard's reporting period was restricted to data through September 2026, excluding records from 2027.

**Note:** The source CSV contains 10,521 rows, while the dashboard's Total Records KPI displays 7,462 in the current report view. The dashboard count reflects the processed model and its counting logic, so it should not be interpreted as the raw CSV row count.

## Dashboard Pages

### Page 1 — National AQI Overview

This page provides an overall view of air quality across Indian cities.

**Key Performance Indicators (KPIs)**

- Average AQI
- Maximum AQI
- Minimum AQI
- Total Records

**Visualizations**

- **Average AQI by City:** Compares average AQI across cities and helps identify locations with higher readings.
- **City-wise AQI Map:** Displays geographical AQI observations across India.
- **AQI Level Distribution:** Shows how records are distributed across AQI categories.
- **AQI Trend Over Time:** Displays changes in AQI across dates.
- **Pollutant Analysis:** Compares average levels of different pollutants.

**Filters:** Year and City.

### Page 2 — AQI Trends & Pollutant Analysis

This page focuses on temporal trends, seasonal differences and pollutant-level analysis.

**Visualizations**

- **Monthly AQI Trend:** Compares average AQI across the twelve months.
- **Seasonal AQI Comparison:** Compares average AQI across the defined seasons.
- **Pollutant Levels Over Time:** Tracks the selected pollutant across dates.
- **Pollutant vs AQI Correlation:** Uses a scatter plot to explore the relationship between pollutant concentration and AQI.
- **AQI Category Distribution by Year:** Compares the percentage distribution of AQI categories across 2025 and 2026.

**Season classification used in the project**

| Season | Months |
|---|---|
| Summer | March–June |
| Rainy | July–October |
| Winter | November–February |

These are the project's chosen seasonal groupings for comparison.

**Filters:** AQI Metric, Year, City and Pollutant, where applicable.

### Page 3 — Environmental Factors & AQI Analysis

This page explores how temperature, humidity and wind speed are associated with AQI.

**Key Performance Indicators**

- Average Temperature (°C)
- Average Humidity (%)
- Average Wind Speed (km/h)
- Average AQI

**Visualizations**

- **Environmental Factor vs AQI:** A scatter plot comparing the selected environmental factor with AQI, with colours representing AQI categories.
- **Average AQI vs Environmental Factor (Monthly Trend):** Compares monthly AQI with the selected environmental measurement using a secondary axis.
- **Average AQI by Environmental Factor Range:** Compares average AQI across ranges of temperature, humidity or wind speed.
- **Quick Insights:** Dynamically identifies the ranges with the highest and lowest average AQI for the selected environmental factor.
- **Summary Statistics:** Displays average, maximum, minimum, standard deviation and record count for the selected environmental factor.

**Filters:** Year, City and Environmental Factor.

The Environmental Factor selector supports:
- Temperature (°C)
- Humidity (%)
- Wind Speed (km/h)

## Data Preparation and Transformation

Power Query was used to prepare the source data for analysis.

Key preparation steps included:

- Checking and converting column data types.
- Selecting the relevant columns for analysis.
- Organising date, location and pollutant information into supporting tables.
- Creating dimension tables for dates, locations, pollutants and city mapping.
- Creating a separate `Fact_Environmental` query by referencing `Fact_AQI`.
- Unpivoting `Temperature_C`, `Humidity_%` and `Wind_Speed_kmh` into two columns: `Environmental Factor` and `Environmental Value`.
- Creating an `Environmental Range` column to group environmental measurements into readable ranges.
- Creating a Season column based on the project's month classification.
- Adding a `Record_Id` index to identify source observations in the environmental query.

These transformations support the interactive environmental analysis and range-based comparisons.

## Data Model

The Power BI model contains fact, dimension and supporting analytical tables, including:

- `Fact_AQI`
- `Fact_Environmental`
- `Dim_Date`
- `Dim_Location`
- `Dim_Pollutant`
- `Dim_City_Map`
- `City_AQI`
- `AQI Metric` field parameter

`Fact_Environmental` is a transformed query created from `Fact_AQI` for analysing environmental factors in a common structure.

## DAX and Analytical Calculations

DAX measures and calculations are used where dynamic or reusable calculations are needed.

Examples include:

- Average AQI
- Maximum and Minimum AQI
- Average Temperature
- Average Humidity
- Average Wind Speed
- Selected Environmental Value
- Quick Insight
- Summary Stat Value

The dynamic environmental measure uses selection logic to return the selected environmental factor. The Quick Insight calculation compares average AQI across environmental ranges, while Summary Stat Value returns the statistic selected for display.

The project also uses a `Summary_Stats` table to display multiple statistics through one measure.

Power Query performs several of the data preparation, grouping and range-classification operations; not every chart requires a custom DAX measure.

## Interactivity

The dashboard supports interactive exploration through:

- Year and City slicers
- AQI Metric selection
- Pollutant selection
- Environmental Factor selection
- Cross-filtering between compatible visuals

These controls allow users to explore different cities, periods, pollutants and environmental conditions without building separate dashboards for each selection.

## Tools and Technologies

- **Microsoft Power BI:** Dashboard development and interactive visualizations
- **Power Query:** Data cleaning and transformation
- **DAX:** Measures, dynamic calculations and insights
- **Kaggle:** Dataset source

## Key Analytical Questions

This project explores questions such as:

- Which cities have higher average AQI?
- How does AQI change across time?
- How do AQI categories differ between years and seasons?
- Which pollutants have higher average measured levels?
- How are pollutant concentrations associated with AQI?
- How does average AQI vary across temperature, humidity and wind-speed ranges?

The dashboard helps identify patterns and associations in the data. These patterns alone do not prove that a pollutant or environmental factor caused a change in AQI.

## How to Use

1. Download the Power BI report (`.pbix`) from this repository.
2. Open it in Microsoft Power BI Desktop.
3. Use the available slicers to filter by year, city, pollutant or environmental factor.
4. Interact with the charts to explore AQI trends and comparisons.

## Repository Structure

```text
India-Air-Quality-Insights/
├── README.md
├── India_Air_Quality_Dashboard.pbix
├── screenshots/
│   ├── Page-1-National-AQI-Overview.png
│   ├── Page-2-AQI-Trends-Pollutants.png
│   └── Page-3-Environmental-Factors.png
└── documentation/
    └── DAX-Measures.md
```

The screenshot and documentation files listed above can be added as supporting project files.

## Dashboard Screenshots

Add screenshots of the completed Power BI pages here so visitors can preview the dashboard directly on GitHub.

Recommended screenshots:
- National AQI Overview
- AQI Trends & Pollutant Analysis
- Environmental Factors & AQI Analysis

## Data Source and Attribution

Dataset: [India Air Quality Dataset (2025–2026) — Kaggle](https://www.kaggle.com/datasets/yogeshm01/india-air-quality-dataset-20252026)

The dataset is attributed to its Kaggle creator. Refer to the original dataset page for its licence and reuse conditions.

---

**Project:** India Air Quality Insights  
**Platform:** Microsoft Power BI  
**Focus:** AQI Analysis, Data Visualization, Pollutant Trends and Environmental Factors
