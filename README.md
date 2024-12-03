# DS2002 Final Project: Analyzing COVID-19 Death Rates and Air Quality

### By Brynn Hill, Anika Tripathi, Clare Gibb, Deetya Gupta, and David Nu

---

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Datasets](#datasets)
- [Dependencies](#dependencies)
- [How to Run the Project](#how-to-run-the-project)
  - [Prerequisites](#prerequisites)
  - [Running the Code](#running-the-code)
- [Project Structure](#project-structure)

---

## Project Overview

The goal of this project is to analyze the relationship between COVID-19 death rates and air quality across U.S. counties in 2020. By integrating multiple datasets, we aim to uncover insights into how environmental factors like air quality might correlate with the severity of COVID-19 impacts on different populations.

---

## Features

- **Data Ingestion**:
  - Reads datasets from CSV files: COVID-19 deaths, population data, and air quality index (AQI) data.
  - Utilizes user input for flexible file handling.

- **Data Transformation**:
  - Cleans and preprocesses data, including handling missing values and duplicates.
  - Renames state abbreviations to full names for consistency.
  - Merges datasets on `State` and `County` columns.
  - Calculates derived metrics like "Deaths per 100,000 people."

- **Data Loading**:
  - Saves the transformed data to a local SQLite database for persistence.
  - Uploads the transformed dataset to Google Cloud Storage (GCS) for accessibility and scalability.

- **Visualization**:
  - Generates scatter plots to examine relationships between variables.
  - Creates bar graphs and box plots to highlight trends and identify outliers.

- **Statistical Analysis**:
  - Calculates the Pearson correlation coefficient to assess the relationship between COVID-19 death rates and median AQI.

- **Cloud Integration**:
  - Integrates with Google Cloud Storage to store and retrieve data securely.
  - Utilizes Google Cloud authentication for secure access.

---

## Datasets

### 1. COVID-19 Provisional Deaths by County

- **Description**: County-level data on provisional COVID-19 deaths by race and Hispanic origin.
- **Source**: [CDC Data Portal](https://data.cdc.gov/NCHS/Provisional-COVID-19-Deaths-by-County-and-Race-and/k8wy-p9cg/data)
- **File**: `covid.csv`

### 2. Population by County

- **Description**: Population estimates for each county to normalize COVID-19 death rates.
- **Source**: U.S. Census Bureau
- **File**: `population.csv`

### 3. Annual AQI by County (2020)

- **Description**: Annual air quality index data for U.S. counties.
- **Source**: Environmental Protection Agency (EPA)
- **File**: `aqi_2020.csv`

---

## Dependencies

The project relies on the following Python libraries:

- **Pandas**: For data manipulation and analysis.
- **NumPy**: For numerical operations (often used implicitly through Pandas).
- **Matplotlib**: For creating visualizations.
- **SQLite3**: For database operations.
- **Google Cloud Storage**: For cloud storage integration.
- **Google Colab Modules** (if running on Colab):
  - `google.colab.auth` for authentication.
  - `google.colab.files` for file operations.

---

## How to Run the Project

#### 1. Download all the Files in `Datasets` Folder

#### 2. Install Required Libraries

Install the necessary Python packages using `pip`:

```bash
pip install pandas matplotlib google-cloud-storage
```

#### 3. Set Up Google Cloud Authentication

- **Using Service Account Key File (Jupyter Notebook, Kaggle, Pycharm, etc.)**

  - Download the JSON key file for your service account.
  - Set the environment variable `GOOGLE_APPLICATION_CREDENTIALS` to point to your key file:

    ```bash
    export GOOGLE_APPLICATION_CREDENTIALS="path/to/your-key-file.json"
    ```

- **Using Google Colab Authentication**
  - We recommend using Colab, since it was the IDE our code is initially written in.
  - If running on Colab, use the following code snippet to authenticate:

    ```python
    from google.colab import auth
    auth.authenticate_user()
    ```

#### 4. Prepare the Datasets

Ensure that the CSV files (`covid.csv`, `population.csv`, `aqi_2020.csv`) are in the same directory as your script or notebook.
(You can download these from the `Datasets` folder above!)

- If using Google Colab, upload the files using:

  ```python
  from google.colab import files
  uploaded = files.upload()
  ```

#### 5. Run the Script or Notebook

- **Running as a Script**:

  ```bash
  python your_script_name.py
  ```

- **Running in Jupyter Notebook or Google Colab**:

  - Open the notebook file (`your_notebook.ipynb`).
  - Execute the cells sequentially.

#### 6. Provide Input When Prompted

The script will prompt you to enter the filenames for the datasets:

```plaintext
Enter file name: covid.csv
Enter file name: population.csv
Enter file name: aqi_2020.csv
```

---

## Project Structure

- **Data Ingestion**:
  - `read_file()` function: Reads CSV files and returns a DataFrame.
  - User is prompted to input the filenames.

- **Data Transformation**:
  - Renaming state abbreviations to full names.
  - Cleaning and merging dataframes (`df1_cleaned`, `df2`, `df3_cleaned`).
  - Calculating "Death per 100,000" metric.

- **Data Loading**:
  - Saving the transformed DataFrame to a CSV file (`transformed_data.csv`).
  - Uploading the CSV file to Google Cloud Storage using `upload_to_gcs()` function.
  - Storing the data in an SQLite database (`final_data.db`).

- **Visualization and Analysis**:
  - Scatter plot: Examines the relationship between median AQI and COVID-19 death rates.
  - Bar graph: Compares deaths per 100,000 and median AQI across randomly selected counties.
  - Box plots: Identifies outliers in the data.
  - Pearson correlation coefficient: Quantifies the relationship between variables.

- **Cloud Integration**:
  - `upload_to_gcs()` and `download_from_gcs()` functions handle interactions with Google Cloud Storage.
  - Authentication is managed via Google Colab's `auth.authenticate_user()`.
