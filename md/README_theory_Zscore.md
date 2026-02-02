# Z-Score Outlier Removal Method

## 1. Theoretical Background
The Z-score method is a statistical technique used to identify and remove anomalies (outliers) from a dataset. It standardizes the data points by quantifying how many standard deviations a specific data point is away from the mean of the dataset.

The Z-score ($Z$) for a given data point is calculated using the following equation:

$$
Z = \frac{X - \mu}{\sigma}
$$

Where:
* **$X$**: The value of the individual data point being evaluated.
* **$\mu$**: The mean (average) of the dataset or the specific time-window.
* **$\sigma$**: The standard deviation of the dataset, representing the amount of variation or dispersion.

### Outlier Detection Logic
A data point is considered an **outlier** if the absolute value of its Z-score exceeds a specified threshold (typically 2.0 or 3.0).

> If $|Z| > \text{Threshold}$, the point is flagged as a statistically significant deviation from the norm.

---

## 2. User Parameters & Configuration
To implement this method, the following parameters must be configured in the Data Processing interface:

### A. Threshold
* **Definition:** The cutoff value for the Z-score calculation.
* **Function:** This determines the sensitivity of the outlier detection.
    * A **lower threshold** (e.g., 2.0) is more aggressive and will identify more points as outliers.
    * A **higher threshold** (e.g., 3.5) is more conservative and will only identify extreme spikes.

### B. STD Ratio Limit (Standard Deviation Scope)
* **Definition:** A control parameter that defines the scope of the statistical calculation.
* **Function:** It determines whether the Z-score is calculated using the **Overall STD** (the standard deviation of the entire dataset) or a **Small time-window STD** (a local, moving standard deviation).
    * *Global Scope:* Useful for stationary data where the mean and variance do not change over time.
    * *Local Scope:* Essential for drifting signals or non-stationary data, allowing the algorithm to adapt to changing signal dynamics.

### C. Tolerance Ratio
* **Definition:** A secondary validation criterion applied to flagged outliers.
* **Function:** This ratio acts as a final gatekeeper to determine if a flagged outlier should be **replaced** or **left unchanged**.
    * Even if a point exceeds the Z-score *Threshold*, it may be retained if it falls within the acceptable *Tolerance Ratio*. This prevents the removal of valid signal peaks that mimic outlier behavior but are physically significant.

---

## 3. Processing Workflow

1.  **Calculate Statistics:** Compute $\mu$ and $\sigma$ based on the selected *STD Ratio Limit* mode.
2.  **Compute Z-Score:** Apply the formula to each data point $X$.
3.  **Threshold Check:** Compare $|Z|$ against the user-defined *Threshold*.
4.  **Tolerance Check:** For points exceeding the threshold, apply the *Tolerance Ratio* logic.
5.  **Action:** If both conditions are met, the outlier is replaced (typically via interpolation or holding the previous value); otherwise, the raw data point is preserved.