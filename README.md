# DS2002 - FINAL PROJECT: COVID-19 Death Rates and Air Quality Analysis
### By Brynn Hill, Anika Tripathi, Clare Gibb, Deetya Gupta, and David Nu


## Project Overview
This project analyzes the relationship between COVID-19 death rates and air quality (measured via median AQI) across U.S. counties in 2020. The analysis utilizes an ETL (Extract, Transform, Load) pipeline to process raw datasets, extract insights, and visualize trends to better understand health and environmental factors.

## Features
- **Data Ingestion**:
  - Reads datasets from local CSV files.
- **Data Transformation**:
  - Converts data into structured formats.
  - Merges datasets on `state` and `county` columns.
  - Drops irrelevant columns and calculates derived metrics like "Deaths per 100,000 people."
- **Data Loading**:
  - Stores transformed data in a MySQL database.
- **Visualization**:
  - Generates scatter plots and bar graphs to communicate insights.
- **Cloud Integration**:
  - Stores transformed datasets in Google Cloud for scalability and accessibility.

## Dependencies
The following Python libraries are required for this project:
- **Pandas**: For data manipulation and transformation.
- **SQLAlchemy**???: For database integration with MySQL.
- **Matplotlib/Seaborn**: For creating visualizations.
- **Google Cloud SDK**: For cloud storage integration.

## Datasets
### 1. **COVID-19 Provisional Deaths by County**
   - **Description**: County-level data on provisional COVID-19 deaths by race and Hispanic origin.
   - **Source**: [CDC Data Portal](https://data.cdc.gov/NCHS/Provisional-COVID-19-Deaths-by-County-and-Race-and/k8wy-p9cg/data)

### 2. **Population by County**
   - **Description**: Population estimates for each county to normalize COVID-19 death rates.
   - **Source**: U.S. Census Bureau

### 3. **Annual AQI by County (2020)**
   - **Description**: Annual air quality index data for U.S. counties.
   - **Source**: Environmental Protection Agency (EPA)
