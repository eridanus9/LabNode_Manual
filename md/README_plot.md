# Data Analysis & Visualization

## 1. Plot Menu Overview
The **Plot** menu acts as the central hub for accessing data analysis and visualization tools. It allows users to switch between three distinct modes:

<img src="figures/plot/plot_menu.png" alt="Alt Text" width="250"/>


* **Data Treatment:** Opens the Data Treatment interface designed for cleaning raw data, removing outliers (using the z-score method), and applying statistical treatments to datasets.
* **Plant Data Comparison:** Launches a window allowing for the side-by-side visual comparison of multiple plant data series to identify trends or discrepancies.
* **GC Data Comparison:** Accesses specialized Gas Chromatography (GC) post-processing tools. This interface provides variables such as Retention Time and Area calculations.
    * *Note:* This option is only available when the active project is explicitly configured to load the GC file format.

---

## 2. Data Plot Interface
The Data Plot window provides a comprehensive view of your datasets.

<img src="figures/plot/plot_window.png" alt="Alt Text" width="800"/>

### Window Layout
* **Main Toolbar (Red):** Contains main titles, saving options, and data configurations.
* **Data Panel (Yellow):** Displays a list of active datasets and controls their visibility.
* **Plot Canvas (Blue):** The main area for visual data representation.
* **Plot Properties (Green):** A menu to customize visualization parameters and display options.

---

## 3. Plot Controls & Properties
Customize the appearance of your graphs using the **Plot Properties** menu.

<img src="figures/plot/plot_properties.png" alt="Alt Text" width="400"/>

### Visual Customization
* **Show Line / Show Marker:** Toggle switches to display lines and data point markers.
* **Data Series:** Select the specific dataset from the dropdown to apply changes to.
* **Styling:**
    * **Maker Size & Style:** Adjust the size and shape (e.g., Square) of data points.
    * **Line Width & Style:** Adjust the thickness and pattern (e.g., Automatic) of the connecting lines.

### Fonts and Layout
* **Font Sizes:** Adjust font sizes for X/Y Axis, X/Y Titles, and the Legend.
* **Legend Position:** Change the location of the legend (e.g., TopRight).
* **Grid:** Toggle switches to show Major and Minor grids for both X and Y axes.
* **Limits:** Manually set the Minimum and Maximum limits for the X (Date) and Y (Value) axes.

---

## 4. Plant Data Treatment
This interface handles data processing and statistical analysis, specifically for outlier removal.

<img src="figures/plot/plot_dataTreatment.png" alt="Alt Text" width="800"/>

### Configuration Parameters
* **Tag Number:** The name or identifier of the data being treated.
* **STD Threshold:** The threshold value used for the z-score method (>0).
* **STD Ratio Limit:** The standard deviation ratio used for the z-score method.
* **Tolerance Ratio:** The ratio used to determine outlier replacement (must be < 1).
* **Moving Window [h]:** The duration of the moving window in hours.

### Actions
* **Wand Icon:** Treat Data using the Z-score method.
* **Trash Icon:** Delete the currently selected treated data.
* **X Icon:** Delete all treated data.

### Statistics Summary
The interface displays a table summarizing the **Max**, **Min**, **Mean**, and **STD** (Standard Deviation) for both the Total Raw Data and Total Treated Data.

---

## 5. Plant Data Comparison
Compare multiple data series simultaneously to view their statistics.

<img src="figures/plot/plot_DataCompare.png" alt="Alt Text" width="800"/>

### Comparison Tools
* **Plus (+):** Add data to the comparison view.
* **Trash Icon:** Delete the selected data from the view.
* **X Icon:** Delete all data from the view.

### List Box Information
For every series added, the list box displays:
* **Data Series:** The identifier of the data.
* **Data Description:** Details describing the dataset.
* **Data Statistics:** Key metrics including Max, Mean, Min, and STD.

---

## 6. GC Data Comparison
This module is for post-processing and comparing Gas Chromatography (GC) data.

<img src="figures/plot/plot_GCDataCompare.png" alt="Alt Text" width="800"/>

### Output Variables
The interface displays specific GC post-processing outputs:
* **PctAreaMEG:** The percentage of the total area occupied by the dominant peak
* **PctAreaBelowMEGRetTime:** The total area percentage of all peaks eluting before the dominant peak
* **PctAreaAboveMEGRetTime:** The total area percentage of all peaks eluting after the dominant peak
* **MinNormalizedRetTime:** Minimum Normalized Retention Time.
* **MaxNormalizedRetTime:** Maximum Normalized Retention Time.
* **MaxRetTime:** Maximum Retention Time.
* **TotalArea:** Total Area Calculation.

### Visualization Control
* **Checkboxes:** Select to view **Online** or **Offline** data on the plot.