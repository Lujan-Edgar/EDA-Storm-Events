# EDA-Storm-Events
As part of my final project for the MATLAB Exploratory Data Analysis course, I transformed a messy CSV dataset into a clean and structured analytical report. The project explores the impact of Hurricane Harvey across multiple U.S. states by performing data cleaning, filtering, aggregation, and damage analysis using MATLAB’s table and grouping tools

# Hurricane Harvey Impact Analysis (MATLAB)

This project analyzes the impact of **Hurricane Harvey (2017)** on several U.S. states using NOAA Storm Events data.  
The analysis is implemented in a MATLAB Live Script (`HurricaneHarvey.mlx`) and focuses on filtering relevant data, cleaning it, and summarizing damages by state, county, and event type.

## Objectives

- Select only the events related to Hurricane Harvey within a specific time window.
- Focus on a subset of affected states.
- Quantify and compare **property + crop damage** across states and counties.
- Identify the **most frequent event types** associated with Harvey’s path.

## Dataset

The project uses a **Storm Events 2017** CSV file (e.g. `StormEvents_2017_finalProject.csv`), which contains severe weather reports including event type, location, dates and estimated damages.

> **Note:** The dataset is not included in this repository.  
> You can obtain a similar dataset from the [NOAA Storm Events Database](https://www.ncdc.noaa.gov/stormevents/).

## Tools & Technologies

- **Language:** MATLAB
- **File type:** Live Script (`.mlx`)
- **Main functions used:**
  - `readtable` / custom `StormEvents(...)` function
  - `ismember`, logical indexing
  - `sortrows`
  - `groupsummary`
  - Basic table filtering and date-time comparisons

## Methodology

1. **Import the data**

   - Load the Storm Events CSV into a MATLAB table using a custom `StormEvents("StormEvents_2017_finalProject.csv")` helper.
   - Keep only the variables needed for the analysis (state, date-time, event type, property damage, crop damage, etc.).

2. **Filter by states and time window**

   - Define a list of target states:
     ```matlab
     targetStates = {'ARKANSAS','KENTUCKY','LOUISIANA', ...
                     'MISSISSIPPI','NORTH CAROLINA', ...
                     'TENNESSEE','TEXAS'};
     ```
   - Filter the table to include only these states.
   - Filter events to the months **August–September**.
   - Further restrict the data to a specific date/time window representing Harvey’s active period.

3. **Data cleaning and transformation**

   - Remove rows with missing values in `Crop_Cost` (or other key fields).
   - Compute a **Total_Cost** variable combining property and crop damages.
   - Sort the data by:
     - `Property_Cost`
     - `Crop_Cost`
     - `Begin_Date_Time` / `End_Date_Time`

4. **Aggregations and summaries**

   - Use `groupsummary` to:
     - Sum **total damages per state**.
     - Summarize damages by **event type**.
     - Aggregate damages by **county (CZ_Name)**.
     - Find the **most frequent event type** in each county and across all states.

5. **Insights**

   Examples of questions this analysis helps answer:

   - Which states experienced the highest total damages during Harvey?
   - Which counties were most heavily affected in terms of cost?
   - What event type (e.g., flooding, tornadoes, wind) occurred most frequently?
