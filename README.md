
# World Stress Map 2025 | Python-Based Geospatial Analysis

**Exploration, quality control, spatial visualization, and statistical analysis of crustal stress observations**

## Project Overview

This independent portfolio project explores the World Stress Map (WSM) Database Release 2025 using Python and geospatial analysis techniques.

The project develops a reproducible workflow for inspecting stress observations, identifying data-quality issues, visualizing the geographic distribution of maximum horizontal compressive stress (SHmax), and investigating regional stress-orientation patterns.

The regional analysis focuses on **Germany and surrounding regions**, using a geographic bounding box of **5°–16°E and 47°–55°N**.

The analysis is based on the publicly available WSM database maintained by the GFZ Helmholtz Centre for Geosciences. This is an independent educational project and is not an official GFZ research product.

## Research Objectives

1. Explore the structure and attributes of the WSM 2025 database.
2. Validate geographic coordinates and SHmax azimuth values.
3. Select reliable observations using WSM quality classes A–C.
4. Visualize global and regional stress-observation distributions.
5. Construct SHmax orientation symbols using geodetic calculations and coordinate transformations.
6. Examine the spatial distribution of stress-regime classifications.
7. Calculate axial circular statistics for SHmax orientations.
8. Compare regional orientation patterns and assess sensitivity to repeated observation locations.

## Dataset and Study Area

**Primary dataset:** World Stress Map Database Release 2025

- Original database: 100,842 observations
- Geographic coordinates: WGS 84 (EPSG:4326)
- Mapping projection: ETRS89-extended / LAEA Europe (EPSG:3035)
- Regional study area: 5°–16°E, 47°–55°N
- Quality selection: A, B, and C
- Additional filtering: valid geographic coordinates and available SHmax azimuths
- Final regional subset: 584 observations

Country boundaries are obtained from Natural Earth (1:110m Admin 0 – Countries).

The regional selection is based on a rectangular geographic extent, not national administrative boundaries.

## Methodology

### 1. Exploratory Data Analysis

The original database is inspected using pandas to examine its structure, data types, missing values, quality classes, stress regimes, and observation attributes.

### 2. Data Validation

Latitude, longitude, and azimuth values are checked for validity and availability.

The analysis distinguishes genuine missing values from special dataset codes, including AZI = 999, which indicates unavailable orientation information.

Observations are filtered to retain valid coordinates, available azimuths, and quality classes A–C.

### 3. Geospatial Analysis

Valid geographic observations are converted into GeoPandas geometries.

The project produces global and regional maps, with Natural Earth country boundaries providing geographic context.

SHmax orientation symbols are constructed from the observation coordinates and azimuths using geodetic forward calculations, then transformed into EPSG:3035 for visualization.

Symbol lengths are chosen for cartographic display and do not represent stress magnitudes.

### 4. Stress-Regime Analysis

The frequencies and spatial distributions of normal faulting (NF), thrust faulting (TF), strike-slip faulting (SS), intermediate regimes (NS and TS), and undetermined regimes (U) are examined.

Both raw counts and normalized percentages are considered.

### 5. Axial Orientation Statistics

SHmax is an axial quantity: orientations separated by 180° describe the same axis.

The analysis therefore uses angle doubling, circular averaging, and mean resultant length rather than relying on ordinary arithmetic means.

The regional dataset is additionally divided at 51°N to compare northern and southern observations.

### 6. Sensitivity Analysis

Repeated geographic coordinate pairs are identified.

An exploratory comparison retains one record per exact coordinate pair to assess how this selection affects the calculated axial mean and resultant length.

This is a sensitivity check rather than a definitive method for removing duplicate measurements.

## Key Results

### Observation Characteristics

The selected regional dataset contains 584 observations at 524 unique coordinate pairs.

Of these observations, 285 (48.80%) have an undetermined stress regime. Among observations with determined regimes, strike-slip is the most frequently recorded category (173 observations, 57.86%).

### SHmax Orientation Statistics

| Dataset | Observations | Axial mean SHmax | Mean resultant length |
|---|---:|---:|---:|
| Full regional subset | 584 | 163.12° | 0.628 |
| Northern subset (51°–55°N) | 122 | 0.27° | 0.445 |
| Southern subset (47°–<51°N) | 462 | 160.40° | 0.700 |
| One record per coordinate pair | 524 | 162.81° | 0.623 |

The overall dataset shows a preferred NNW–SSE SHmax orientation, with considerable variation among individual observations.

The southern subset has a higher mean resultant length than the northern subset, indicating stronger net alignment. The axial means of the two subsets differ by approximately 19.87°.

Retaining one observation per exact coordinate pair produces only a small change in the overall axial mean and resultant length.

These findings describe the selected observation sample. The north–south comparison is exploratory and does not establish the statistical significance or tectonic causes of regional differences.

## Limitations

- Observations are unevenly distributed geographically.
- Some observation records share identical coordinate pairs.
- Measurements may differ in depth, method, and source.
- A substantial proportion of stress regimes are undetermined.
- The north–south division at 51°N is exploratory rather than a geological boundary.
- Mean orientations and resultant lengths summarize the sample but do not independently establish spatially uniform stress fields.
- The sensitivity analysis retains the first record at each repeated coordinate pair; this choice is not a substitute for evaluating measurement independence or quality.

## Repository Contents

| File | Description |
|---|---|
| `figures/` | Selected maps and scientific visualizations |
| `.gitignore` | Excludes temporary files and locally downloaded datasets |
| `01_WSM_Data_Exploration.ipynb` | Database structure, attributes, quality classes, and exploratory statistics |
| `02_WSM_Data_Validation.ipynb` | Coordinate checks, azimuth validation, and data filtering |
| `03_WSM_Spatial_Analysis.ipynb` | Global and regional mapping, SHmax orientation symbols, and repeated-location investigation |
| `04_WSM_Stress_Patterns.ipynb` | Stress regimes, axial orientation statistics, regional comparison, and sensitivity analysis |
| `README.md` | Project overview, methodology, results, and reproducibility |
| `requirements.txt` | Python dependencies |

## Technologies and Skills

**Languages and libraries:** Python, pandas, NumPy, GeoPandas, Matplotlib, pyproj

**Geospatial methods:** Coordinate reference systems, geographic filtering, spatial data visualization, geodetic calculations, and coordinate transformations

**Data analysis:** Data validation, exploratory statistics, categorical analysis, axial circular statistics, and sensitivity assessment

**Development environment:** JupyterLab and GitHub

## Reproducibility

The notebooks use relative file paths and are intended to be executed sequentially.

### Data Download

1. Download the World Stress Map Database Release 2025 from the [official WSM download page](https://www.world-stress-map.org/download).
2. Save the CSV in the project directory under the filename `WSM_Database_2025.csv`.
3. Download the [Natural Earth 1:110m Admin 0 – Countries](https://www.naturalearthdata.com/downloads/110m-cultural-vectors/) shapefile.
4. Extract the shapefile and its companion files into the `natural_earth/` directory.


## Data Sources and Attribution

**World Stress Map Database Release 2025**

Heidbach, O., Rajabi, M., Di Giacomo, D., Harris, J., Lammers, S., Morawietz, S., Pierdominici, S., Reiter, K., von Specht, S., Storchak, D., and Ziegler, M. O. (2025). *World Stress Map Database Release 2025*. GFZ Data Services.

https://doi.org/10.5880/WSM.2025.001

**Basemap**

Natural Earth. *1:110m Admin 0 – Countries*.

https://www.naturalearthdata.com/

## Project Status

Completed exploratory and regional stress-orientation analysis, prepared as an independent Python and geospatial data-analysis portfolio project.
