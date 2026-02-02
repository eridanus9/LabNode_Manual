# Project Management

## 1. Project Menu Overview
**Primary gateway for managing your workspace.**

<img src="figures/project/project_menu.png" alt="Alt Text" width="250"/>

Access the menu by clicking **Project** in the top navigation bar.

| Option | Shortcut | Description |
| :--- | :--- | :--- |
| **New Project** | `Ctrl + N` | Opens the interface to create a brand-new project. |
| **Load Project** | `Ctrl + O` | Opens the database list to open a previously saved project. |
| **Close Project** | `Ctrl + C` | Closes the currently active project without exiting the software. |
| **Users** | N/A | Access user management settings. |
| **Exit** | `Alt + F4` | Quits the application. |

---

## 2. Creating a New Project
**Shortcut:** `Ctrl + N`

### Step 1: Project Particulars (Metadata)
Define the core project identity in the **Project Particulars** tab.

<img src="figures/project/project_particular.png" alt="Alt Text" width="400"/>

* **Project Name:** Enter the unique name for the project.
* **Project Number:** Input the specific reference number for this project.
* **Client:** Specify the client name associated with this work.
* **Input Formats:** Define the date and time structures used in your source data (e.g., `yyyy-MM-dd` and `HH:mm`).
* **Use Client Tag:** Toggle this switch to enable or disable the use of client-specific tags.

### Step 2: Source Data File Configuration
Select the appropriate file format icon (.csv, Excel, or GCData) and configure the specific settings.

#### A. For .csv Files
* **Date/Time Toggle:** Use the toggle switch to indicate if Date and Time information is combined within a single cell.

<img src="figures/project/project_sourceDataCSV.png" alt="Alt Text" width="400"/>

#### B. For Excel Files

<img src="figures/project/project_sourceDataExcel.png" alt="Alt Text" width="400"/>

* **Date/Time Toggle:** Enable the switch if Date and Time are contained in a single cell.
* **Cell Mapping:** Specify the starting cell positions for the following data columns:
    * **Date first cell:** (e.g., A1)
    * **Time first cell:** (e.g., B1)
    * **Tags first cell:** (e.g., C1)
    * **Values first cell:** (e.g., D1)

#### C. For GC Data Files
Utilize the checkboxes to configure **Offline data settings**:

<img src="figures/project/project_sourceDataGCData.png" alt="Alt Text" width="400"/>

* **Remove First Peak:** Select this to remove the first peak found in the dataset.
* **Exclude Labeled Signal:** Enable this to exclude specific labeled signals (e.g., "TCD") from processing.
* **GC Number:** Specify the GC Number used to analyze and post-process the data.

---

## 3. Loading a Project
**Shortcut:** `Ctrl + O`

The **Load Project** window displays a list of projects organized by Number, Name, and Client.

<img src="figures/project/project_load.png" alt="Alt Text" width="400"/>

### How to Manage Projects
1.  **Select:** Click on a project row. A **blue vertical bar** will appear on the left to indicate selection.
2.  **Load:** Click the blue **Load** button at the bottom of the window to open the selected project.
3.  **Delete:** Click the **Red Trash Can Icon** on the far right of a row to permanently remove a project.
4.  **Close:** Click the **Close** button to exit without performing any actions.