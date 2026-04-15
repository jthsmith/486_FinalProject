# EECS 486 Final Project - Homelessness Policy & Housing Data Pipeline

## Description
Pulls together several public datasets such as Census ACS, HUD homeless counts, federal grant data, and also includes a custom dataset centered on implementation of policy solutions to homelessness by federal “Continuum of Care” districts. Merges them into one clean CSV that's ready for modeling. The end goal is training a classifier to predict whether a city will see a decrease in homelessness year-over-year based on factors including rent, poverty rates, and especially housing policies.

## Files
Main
dataprep.ipynb                        # main notebook, run this
PolicyMaster.csv                      # housing policy scores by CoC (2022–2024)
coc-county-mapping - Sheet4.csv       # maps counties to CoC codes
FederalCoCData.csv                    # federal HUD grant awards by CoC and year

## Raw Data (annual CSVs, 2014–2024)
poverty20XX.csv     # Census ACS poverty status by county
rent20XX.csv        # Census ACS median gross rent by county
vacancy20XX.csv     # Census ACS housing vacancy by county
2007-2024-PIT-Counts-by-CoC.xlsx - 20XX.csv   # HUD point-in-time homeless counts by CoC

## Intermediate & Output CSVs
final_df.csv                # merged wide-format data before filtering
final_df_filtered.csv       # filtered to target CoCs
final_df_long.csv           # reshaped to long format (one row per CoC per year)
final_grouped.csv           # aggregated at CoC level
final_with_funding.csv      # after adding federal funding columns
normalized_df_filtered.csv  # normalized features, filtered to target CoCs
final_merged_df.csv         # final output with policy scores merged in

## Data Sources
HUD Point-in-Time Counts — yearly homeless counts by CoC
Census ACS 5-Year Estimates — median rent, vacancy rates, poverty stats by county
HUD Federal CoC Grants — how much federal funding each CoC got per year
PolicyMaster.csv — policy scores for Housing First, rental assistance, hostile policies, and city shelter

## How the Pipeline Works
Load annual CSVs for rent, vacancy, and poverty (2014–2024), keep only the useful columns, and rename them by year.
Load HUD homeless count data and filter to the pertinent columns.
Join everything to a CoC-county crosswalk so we can connect Census data (county-level) to homeless counts (CoC-level)
Merge all years into one wide dataframe, then reshape it to long format (one row per CoC per year)
Add federal funding data 
Engineer features: percent change in homelessness, unsheltered share, normalized rent/population/funding
Merge in policy scores from PolicyMaster.csv
Train a Decision Tree classifier to predict if homelessness went down that year

## Requirements/Installation
pandas
numpy
scikit-learn
tqdm
sklearn
matplotlib
re

### Install with:
pip install pandas numpy scikit-learn tqdm
