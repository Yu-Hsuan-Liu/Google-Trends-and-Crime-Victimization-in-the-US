# Google Trends and Crime Victimization in the US

Replication code for:

> Liu, Y.-H., Wolff, K. T., & Lo, T.-Y. (2023). Big data in crime statistics: Using Google Trends to measure victimization in designated market areas across the United States. *Methodological Innovations*. https://doi.org/10.1177/20597991231183962

The study builds victimization estimates for motor vehicle theft, burglary, larceny, and rape from Google Trends search activity across 107 U.S. designated market areas, 2010-2019, and compares them with UCR rates. Both measures are regressed on social disorganization covariates constructed from ACS data, with Cook's distance diagnostics for influential DMAs.

Three pieces of code: `GT_CodeForCrimeKeywords2010-2019.ipynb` samples Google Trends through pytrends (repeated pulls with long sleeps, since every request returns a different sample); the Rmd merges ACS, UCR, and the search estimates and produces the regression tables; `GT_Geo_Code_Heat_Map.ipynb` draws the DMA choropleth maps.

The merged dataset is included as `data/final.data.2010_2019.csv`, so the modeling sections of the Rmd run without rebuilding the merge. The raw ACS and UCR downloads sit outside the repository, and their local paths in the Rmd would need adjusting to rebuild from scratch.
