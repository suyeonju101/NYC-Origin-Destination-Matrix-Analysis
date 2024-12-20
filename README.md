# NYC OD Matrix Creation and SUMO Traffic Simulation

## Overview
This project focuses on traffic simulation using the Simulation of Urban Mobility (SUMO) tool. It includes the creation of NYC Origin-Destination (OD) matrix and the preparation of simulation files compatible with SUMO. The repository contains scripts, data files, and notebooks to assist in preparing inputs for SUMO and analyzing outputs.

## Features
- **OD Matrix Creation**: Tools and scripts to generate OD matrix from external data (details are below).
- **SUMO Preparation**: Notebooks for preparing simulation inputs compatible with SUMO.

## Repository Structure

    ├── data 
    
        ├──2023.zip
    
        ├── uszips.csv
    
        ├── other
        
            └── 2024.zip
            
    ├── SUMO_preparation.ipynb  # Jupyter Notebook for preparing SUMO files
    
    ├── SUMO_files.zip          # Preconfigured SUMO files generated from running SUMO_preparation.ipynb

    ├── ODmatrix_creation.ipynb # Jupyter Notebook for creating OD matrices/
        
    └── od_matrix.csv           # Created OD matrix from running ODmatrix_creation.ipynb/


## Data Sources

### External Data
This project utilizes publicly available datasets from the U.S. Census Bureau's Longitudinal Employer-Household Dynamics (LEHD) program. The data is sourced from:

- [LEHD Main Data Directory](https://lehd.ces.census.gov/data/)
- [New York State LODES Data Directory](https://lehd.ces.census.gov/data/lodes/LODES8/ny/)

Specifically, the following datasets were used to build the **OD matrix**:
1. **`ny_od_main_JT00_2021.csv`**:
   - Contains the Origin-Destination (OD) flow data for all job types (JT00) in New York for the year 2021, which is updated in 2023.
   - Each row includes details on the number of workers commuting between specific origins and destinations.
2. **`ny_xwalk.csv`**:
   - A crosswalk file for New York state that maps geographic units (e.g., Census blocks) to their corresponding higher-level geographic identifiers (e.g., counties, tracts).
   - Used to translate and aggregate OD data for specific geographic regions.

*Note. These two data files are in zip file called **`2023.zip`** This zip file contains the necessary data files and will be automatically unzipped when running the Jupyter notebooks.* *Similarly, **'2024.zip`** contains the most recently updated data files (data from the year 2022, updated in 2024). The OD matrix built from these files are not used for creating SUMO files due to the smaller volume of data compared to the previous year.*

### Processed Data
- **`od_matrix.csv`**:
  - Derived from the raw datasets in **`2023.zip`** mentioned above.
  - Obtained by running **`ODmatrix_creation.ipynb**.
  - Represented aggregated OD traffic demand (flow) in a simplified format.

### Simulation Files
- **SUMO Configuration Files (`SUMO_files.zip`)**:
  - Built based on the OD matrix **`od_matrix.csv`**.
  - Included node file (`.nod.xml`), edge file (`.edg.xml`), and route files (`.rou.xml`) prepared for SUMO.
  - Future work: Need network file (.net.xml), edge-type file (.type.xml), and configureation file (.sumocfg).

## How to Run

1. Execute **`ODmatrix_creation.ipynb`**:  
   - This notebook processes the raw data and generates the file **`od_matrix.csv`**, representing the OD matrix.  

2. Execute **`SUMO_preparation.ipynb`**:  
   - This notebook uses the **`od_matrix.csv`** to prepare the three necessary input files for SUMO simulation.  
