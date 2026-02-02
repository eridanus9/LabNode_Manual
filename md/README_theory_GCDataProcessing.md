# GC Data Post-Processing

## 1. Overview
The `GCPostProcessing` function is designed to standardise and analyze gas chromatography (GC) reports. It performs filtering, optional peak removal, and statistical normalization of peak areas and retention times.

This function distinguishes between **Online** and **Offline** data processing, applying stricter filtering rules to offline data.

---

## 2. Processing Workflow

### A. Offline Filtering Logic (Run only if `!isOnline`)
If the data is processed in "Offline" mode, the following filters are applied sequentially:

1.  **Signal Name Filter:**
    * If enabled (`isExcludeLabeledSignal`), it checks if the report's `SignalName` contains the excluded string. If it matches, the report is discarded.
2.  **Instrument Filter:**
    * If enabled (`isGCNumberToAnalyze`), it checks if the `Instrument` matches the target ID. If it does not match, the report is discarded.
3.  **Peak Removal (Solvent Stripping):**
    * If `isRemovePeaks` is enabled, the function identifies the **largest peak by Area** and removes it from the dataset.
    
### B. Statistical Calculations
After filtering, the function analyzes the remaining peaks to calculate distribution metrics.

1.  **Identify Dominant Peak (MEG):**
    * The system finds the peak with the maximum Area remaining in the set.
    * *Note:* If `isRemovePeaks` was active, this will be the *second* largest peak from the original raw data (the largest impurity).
2.  **Total Area Calculation:**
    * Sums the area of all peaks currently in the list.
---

## 3. Outputs

The function returns the modified `GCReportData` object with updated properties:

**Distribution Ratios:**
* **`PctAreaMEG`**: The percentage of the total area occupied by the dominant peak.
* **`PctAreaBelowMEGRetTime`**: The total area percentage of all peaks eluting **before** the dominant peak (lighter components).
* **`PctAreaAboveMEGRetTime`**: The total area percentage of all peaks eluting **after** the dominant peak (heavier components).

**Normalization:**
The function normalizes retention times relative to the dominant peak:
* The Retention Time (RT) of the dominant peak is treated as the reference (1.0).
* **`MaxNormalizedRetTime`**: The RT of the last eluting peak divided by the dominant peak's RT.
* **`MinNormalizedRetTime`**: The RT of the first eluting peak divided by the dominant peak's RT.

* **Updated Peak List:** The list may have the largest peak removed if configured.
* **`TotalArea`**: The new total area sum.
* **`MaxRetTime`**: The retention time of the dominant peak.
* **`AreaPercent` (Per Peak):** Every individual peak object is updated with its specific % contribution to the new total.
