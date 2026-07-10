# Google Trends and Crime Victimization in the US

Replication code for the article:

> Liu, Y.-H., Wolff, K. T., & Lo, T.-Y. (2023). Big data in crime statistics: Using Google Trends to measure victimization in designated market areas across the United States. *Methodological Innovations*, 0(0). https://doi.org/10.1177/20597991231183962

## Overview

This repository contains the code behind the article. A Python notebook implements the methodology for extracting crime victimization estimates from Google Trends search data, and an R Markdown file documents the data analysis strategy along with the tables and figures generated for the article.

The study builds crime estimates for motor vehicle theft, burglary, larceny, and rape from Google Trends search activity across 107 U.S. Designated Market Areas (DMAs) for 2010 to 2019, then compares these estimates with Uniform Crime Reports (UCR) rates. Cross-sectional linear regression models relate the Google Trends and UCR measures to social disorganization covariates constructed from American Community Survey data (concentrated disadvantage, residential mobility, heterogeneity, and related indices). Diagnostic plots use Cook's distance to flag influential DMAs, and choropleth heat maps display the geographic distribution of the search-based estimates.

## Repository contents

| Path | Description |
|---|---|
| `GT_CodeForCrimeKeywords2010-2019.ipynb` | Collects Google Trends data through the pytrends API using combined crime-related keyword queries (motor vehicle theft, rape, larceny, and other categories), with scheduled sampling and sleep intervals. |
| `GT_Geo_Code_Heat_Map.ipynb` | Builds DMA-level choropleth heat maps of the Google Trends estimates with geopandas, geoplot, and plotly, using a DMA boundary shapefile. |
| `Cross-scetional-only-_Acs_and_GT_2010-2019_0626_2023.Rmd` | Main analysis: merges ACS five-year estimates, UCR offense counts, and Google Trends estimates at the DMA level; estimates the regression models; produces the article tables (stargazer) and Cook's distance diagnostics. |
| `data/final.data.2010_2019.csv` | Final merged DMA-level dataset (Google Trends estimates, UCR rates, and ACS-derived covariates). |
| `data/DMA_population_table.csv` | List of the DMAs used in the study with population totals. |
| `figures/` | Exported figures: violent and property crime heat maps and the Cook's distance scatter plot for the GT and UCR rape measures. |
| `output/regression_models2.html` | Rendered regression tables. |

## Data sources

As evidenced in the code, the analysis draws on:

- Google Trends search interest, retrieved with pytrends using crime-specific keyword combinations
- FBI Uniform Crime Reports, offenses known (ICPSR yearly file, 1960 to 2019)
- American Community Survey five-year estimates (2005-2009 through 2015-2019)
- A county-to-DMA crosswalk
- NCHS drug poisoning mortality by county
- FBI law enforcement employment counts
- A DMA boundary shapefile for mapping

The raw source files sit outside the repository; the merged analysis dataset is provided in `data/`.

## Requirements

**Python 3**: pytrends, pandas, numpy, scipy, geopandas, geoplot, plotly, shapely, pyproj, matplotlib.

**R**: tidyverse, dplyr, ggplot2, stargazer, xtable, kableExtra, MASS, plm, lmtest, multiwayvcov, MatchIt, psych, corrplot, sf, sp, geojsonio, rnaturalearth, viridis, readxl, janitor, among others loaded in the first chunk of the Rmd.

## Reproducing the analysis

1. Run `GT_CodeForCrimeKeywords2010-2019.ipynb` to sample Google Trends data for the crime keyword sets (the notebook repeats requests over long sleep intervals because Google Trends returns a different sample on each pull).
2. Knit the Rmd to reproduce the merged dataset, regression models, tables, and diagnostic figures. File paths in the Rmd point to local folders holding the raw ACS and UCR downloads and must be adjusted. The included `data/final.data.2010_2019.csv` allows the modeling sections to run without rebuilding the merge.
3. Run `GT_Geo_Code_Heat_Map.ipynb` to regenerate the heat maps (requires the DMA shapefile).

## License

MIT License. See `LICENSE`.
