# Autocheck Function 

## 1. Overview
The **Autocheck** function is an asynchronous data processing routine designed to clean time-series data by removing outliers. It utilizes two distinct Z-Score processing methods in parallel and compares their statistical results against the raw data to generate a "Stability Score" (Status).

The primary output of this function is the cleaned data set, along with a status flag indicating how significantly the cleaning process altered the data's statistical properties.

---

## 2. Inputs
The function accepts the following inputs via the `RunAutocheckAsync` method:

### A. Function Arguments
* **`dateTimeArray`** (`DateTime[]`): An array of timestamps corresponding to the data points.
* **`finalValues`** (`double[][]`): A jagged array representing columns of raw data to be processed.
* **`progress`** (`IProgress`): (Optional) A progress reporter for the user interface.

### B. Global Parameters
The function relies on the following application-level settings (captured from `MainWindow`):
* **`WindowSize`**: The size of the moving window for statistical calculation.
* **`Threshold`**: The Z-Score cutoff limit for identifying outliers.
* **`Stdev Ratio Limit`**: Determines if the *Overall STD* or *Small time-window STD* is used.
* **`Tolerance Ratio`**: Determines if a flagged outlier should be replaced or retained.

---

## 3. Processing Logic
For every column of data provided, the function performs the following steps:

### A. Dual-Method Processing
The data is processed simultaneously using two different instances of Z-Score processors:

* **Processor 1 (Standard):** Uses the fixed user-defined `threshold` and parameters.
* **Processor 2 (Iterative):** Uses a variable threshold approach.
    * *Start:* 7.0 (Very loose)
    * *End:* User-defined `threshold`
    * *Step:* 0.05
    * *Goal:* To gradually identify outliers.

### B. Cross-Validation (The "Auto" Check)
Once the data is processed, the function performs a statistical comparison to determine the reliability of the cleaning. It calculates the **Average** and **Standard Deviation** for three datasets:
1.  **Raw Data** (Original)
2.  **Method 1 Data** (Treated)
3.  **Method 2 Data** (Treated)

The function performs a matrix comparison (All vs. All) using the following sensitivity thresholds:

| Statistic | Sensitivity Threshold | Logic |
| :--- | :--- | :--- |
| **Average** | **5% (0.05)** | If the average changes by more than 5% between any two versions of the data, a flag is raised. |
| **Std Dev** | **50% (0.5)** | If the standard deviation changes by more than 50% between any two versions, a flag is raised. |

### C. Warning Generation
The function sums up all flags generated during the cross-validation logic.
* **Status 0:** The cleaning process was stable.
* **Status > 0:** The cleaning process significantly altered the data (e.g., removing a large number of points or high-magnitude outliers changed the average or variance drastically).

