# Global Climate Classification — Köppen–Trewartha
This project analyzes changes in global climate classification using ERA5
temperature and precipitation data. The analysis applies the
Köppen–Trewartha climate classification system consistently across three
climate intervals and examines changes in climate groups and types from
1961 through 2025.

The project is implemented in R as a reproducible Quarto book and is
organized into six stages: data acquisition, data transformation,
determinant calculation, climate classification, transition analysis,
and transition mapping.

## 🌍 Live Project

The complete Quarto book is available at:

[Global Climate Classification Change Analysis](https://rkforest.github.io/global-climate-classification-change-analysis/)

## Analysis

The project examines global climate-classification change from several
complementary perspectives:

1. Köppen–Trewartha climate groups and types for each climate interval
2. Changes in the global land-area distribution of climate classifications
3. Climate-group transition matrices
4. Climate-type transition matrices
5. Gains, losses, and net changes in climate groups and types
6. Geographic distribution of within-group and between-group changes
7. Expansion of dry and desert climate classifications
8. Retreat of polar climate classifications
9. Long-term spatial patterns of climate-group transitions

Together, these analyses show both how global climate classifications have
changed and where those changes have occurred.

## Data Sources

Source, transformed, and derived climate data are not stored in the
repository. Running the workflow creates the required `data/` directories
and downloads or generates the necessary files.

### ERA5

Temperature and precipitation data are obtained from the ERA5 reanalysis
produced by the European Centre for Medium-Range Weather Forecasts (ECMWF)
and distributed through the Copernicus Climate Data Store.

The project uses:

- Monthly 2 m air temperature
- Monthly total precipitation
- ERA5 land-sea mask

### Natural Earth

Natural Earth coastline data are used as geographic reference data for the
global maps.

## Climate Periods

The analysis uses three non-overlapping climate intervals:

| Climate Interval | Abbreviation | Years |
|---|---|---|
| WMO Climatological Reference Period | REF | 1961–1990 |
| WMO Climatological Standard Normals | CSN | 1991–2020 |
| Recent Climate Interval | RCI | 2021–2025 |

REF and CSN provide established 30-year climatological reference periods.
RCI is a project-defined recent five-year interval used to examine emerging
climate signals and is not a WMO climatological normal.

## Köppen–Trewartha Climate Classification

The Köppen–Trewartha system used in this project contains six broad climate
groups and thirteen climate types.

The same classification rules are applied independently to REF, CSN, and
RCI. This provides a consistent basis for identifying changes among climate
groups and types through time.

## Project Structure

```text
Projects/
├── era5-data/
│   └── data/
│       └── transformed/             # Shared ERA5 climatologies
│
└── global-climate-koppen-trewartha/
    ├── _quarto.yml
    ├── index.qmd
    ├── 01-determinant-calculation.qmd
    ├── 02-climate-classification.qmd
    ├── 03-transition-analysis.qmd
    ├── 04-transition-mapping.qmd
    ├── R/
    │   └── climate-periods.R
    ├── data/
    │   ├── reference/               # Classification reference data
    │   └── derived/                 # Classification analysis outputs
    └── README.md
```

### 01-determinant-calculation.qmd

Reads the shared ERA5 temperature and precipitation climatologies from the companion ERA5-DATA project and calculates the temperature, precipitation, and aridity determinants required by the Köppen–Trewartha climate classification system.

### 02-climate-classification.qmd

Creates the classification-specific reference tables and coastline data, applies the Köppen–Trewartha classification rules to each climate interval, and summarizes the resulting climate groups and types.

### 03-transition-analysis.qmd

Quantifies climate-group and climate-type transitions for REF → CSN, CSN → RCI, and REF → RCI using transition matrices and calculations of gains, losses, and net classification change.

### 04-transition-mapping.qmd

Maps the geographic distribution of classification changes, including within-group and between-group changes, expansion of dry and desert climate classifications, retreat of polar classifications, and the long-term REF → RCI transition pattern.

## Software

The climate-classification analysis is written in R and rendered with Quarto. Positron is used as the development environment.

Major R packages include:

- arrow
- fs
- gt
- patchwork
- rnaturalearth
- sf
- terra
- tidyverse
- viridisLite

The project uses `renv` to manage reproducible R package dependencies. Package versions are recorded in `renv.lock`.

ERA5 acquisition and transformation are performed separately in the companion **ERA5-DATA** project.

## Reproducible Environment

This project uses **renv** to manage R package dependencies.

After cloning the repository, restore the project environment with:

```r
install.packages("renv")
renv::restore()
```

This installs the package versions recorded in `renv.lock`, helping
reproduce the software environment used during development.

## Reproducing the Analysis

This project uses transformed ERA5 climate datasets prepared by the companion **ERA5-DATA** project. The two projects are expected to reside in sibling directories under `~/Projects/`.

1. Clone or obtain both the `era5-data` and `global-climate-koppen-trewartha` projects, placing them in sibling directories.

2. Prepare the shared monthly temperature and precipitation climatologies for REF (1961–1990), CSN (1991–2020), and RCI (2021–2025) using the acquisition and transformation notebooks in `era5-data`.

3. Open the Global Climate Classification — Köppen–Trewartha project in Positron and restore its R environment using `renv::restore()`.

4. Run the analysis notebooks in sequence:

       01-determinant-calculation.qmd
       02-climate-classification.qmd
       03-transition-analysis.qmd
       04-transition-mapping.qmd

The first notebook reads the shared ERA5 climatologies from `../era5-data/data/transformed/` and produces classification determinants. Subsequent notebooks generate climate classifications, analyze transitions among climate groups and types, and produce geographic maps of those transitions.

The classification-specific reference tables and coastline data are generated by `02-climate-classification.qmd`.

A complete rebuild requires running the acquisition and transformation workflow in ERA5-DATA before executing the classification analysis. Existing derived datasets may be reused when the corresponding calculation switches are disabled.

## Output

The project renders as an HTML Quarto book containing the complete workflow,
data summaries, Köppen–Trewartha climate classifications, transition
matrices, net-change analyses, and global transition maps.

## Notes

- REF and CSN are 30-year climate intervals; RCI is a shorter five-year
  interval intended to characterize recent conditions.
- RCI should not be interpreted as a WMO climatological normal.
- All climate intervals are classified using the same Köppen–Trewartha
  methodology.
- Transition analyses are performed for REF → CSN, CSN → RCI, and
  REF → RCI.
- Maps of dry and desert climate expansion describe changes in climate
  classification and should not be interpreted as direct measurements of
  land degradation or desertification.
- Large downloaded and generated climate datasets are excluded from the
  Git repository and can be recreated by running the workflow.

## Author

Rick Forest

## Data Licensing

This repository contains code developed for this project. ERA5 data from the
Copernicus Climate Data Store and Natural Earth geographic data remain
subject to their respective licenses and terms of use.
