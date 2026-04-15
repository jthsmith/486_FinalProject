# EECS 486 Final Project - Homelessness Policy & Housing Data Pipeline

## Description
Pulls together several public datasets such as Census ACS, HUD homeless counts, federal grant data, and also includes a custom dataset centered on implementation of policy solutions to homelessness by federal “Continuum of Care” districts. Merges them into one clean CSV that's ready for modeling. The end goal is training a classifier to predict whether a city will see a decrease in homelessness year-over-year based on factors including rent, poverty rates, and especially housing policies.

## Files
`Main`<br>
`dataprep.ipynb` — main notebook, run this<br>
`PolicyMaster.csv` — housing policy scores by CoC (2022–2024)<br>
`coc-county-mapping` - Sheet4.csv — maps counties to CoC codes<br>
`FederalCoCData.csv` — federal HUD grant awards by CoC and year<br>

## Raw Data (annual CSVs, 2014–2024)
`poverty20XX.csv`     # Census ACS poverty status by county<br>
`rent20XX.csv`        # Census ACS median gross rent by county<br>
`vacancy20XX.csv`     # Census ACS housing vacancy by county<br>
`2007-2024-PIT-Counts-by-CoC.xlsx - 20XX.csv`   # HUD point-in-time homeless counts by CoC<br>

## Intermediate & Output CSVs
`final_df.csv`                # merged wide-format data before filtering<br>
`final_df_filtered.csv`       # filtered to target CoCs<br>
`final_df_long.csv`           # reshaped to long format (one row per CoC per year)<br>
`final_grouped.csv`           # aggregated at CoC level<br>
`final_with_funding.csv`      # after adding federal funding columns<br>
`normalized_df_filtered.csv`  # normalized features, filtered to target CoCs<br>
`final_merged_df.csv`         # final output with policy scores merged in<br>

## Data Sources
**HUD Point-in-Time Counts** — yearly homeless counts by CoC<br>
**Census ACS 5-Year Estimates** — median rent, vacancy rates, poverty stats by county<br>
**HUD Federal CoC Grants** — how much federal funding each CoC got per year<br>
**PolicyMaster.csv** — policy scores for Housing First, rental assistance, hostile policies, and city shelter<br>

## How the Pipeline Works
<ol>
  <li>Load annual CSVs for rent, vacancy, and poverty (2014–2024), keep only the useful columns, and rename them by year.</li>
  <li>Load HUD homeless count data and filter to the pertinent columns.</li>
  <li>Join everything to a CoC-county crosswalk so we can connect Census data (county-level) to homeless counts (CoC-level)</li>
  <li>Merge all years into one wide dataframe, then reshape it to long format (one row per CoC per year)</li>
  <li>Add federal funding data</li>
  <li>Engineer features: percent change in homelessness, unsheltered share, normalized rent/population/funding</li>
  <li>Merge in policy scores from PolicyMaster.csv</li>
  <li>Train a Decision Tree classifier to predict if homelessness went down that year</li>
</ol>

## Requirements/Installation
`pandas`<br>
`numpy`<br>
`scikit-learn`<br>
`tqdm`<br>
`sklearn`<br>
`matplotlib`<br>
`re`<br>

### Install with:
`pip install pandas numpy scikit-learn tqdm sklearn matplotlib re`
