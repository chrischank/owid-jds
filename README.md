# OWID_JDS
> Submitted by Christopher Yan Chak, Chan for the position of Junior Data Scientist for Our World in Data

## Overview

## GOAL: Calculate both Crude Death Rate and Age-Standardised Death Rate from Age-Specific Death Rates
### Data:
1. UN WPP Population Estiamtes (1950-2021) (UN DESA., 2022)
2. WHO Standard Population Distribution aggregate (Ahmad et al., 2001)
3. Age-Specific Death Rates COPD 2019

### Definitions (ONS., 2023, WHO., 2023):
> Age-Specific Death Rates: Number of deaths in hte age group per 1,000 population in the same age group\
> Crude Death Rate: Total deaths per 1,000 population\
> Age-Standardised Death Rates: A weighted average of the age-specific mortality rates per 100,000 persons, where the weights are the proportions of persons in the corresponding age groups.

### Summary
> 1. Crude Death Rate calculations
Since I could not find UN WPP Population Estimate for 1950-2021 for specific country, as the Special Aggregate, which contained past data only exist for various spatial/regional/economic zones
aggregates, I used the Standard Project to back interpolate results for 2019. Particularly, I looped through the various estimation scenarios (e.g. Medium Variant, High Variant, Zero-migration)
and interpolated 2019 population for both Uganda and USA for each. I believe this will also demonstrate my capabilities in python and data extraction.

- I found that in both in the future projection and the interpolated results, USA and UGA tends to over-estimate their Crude Death Rates results
- USA Crude Death Rate interpolated and sample projection were significantly higher than UGA, this is inverse of the real data obtained from the Census, although the UGA CDR is much closer to expected projections at each variants
- Initially I thought this was a mistake on my part, but upon checking the samples [2022 to 2026] trends from the interpolation from cubic spline tracks the resulted projection
- In reality from census results I downloaded from the USA and UGA census website, the CDR for the US is much lower than Uganda

> 2. Age-Standardised Death Rate
For Age-Standardised Death Rate, I calculated from standardised 5-years interval Population Census from USA and projected data from UGA, both were sourced from respective census,
For Uganda, the census only tallied 5-years interval up to 80+ years range, i.e. the calculation for 80-84 and 85+ cannot be made due to the aggregation, I did not want to risk
trying to separate out the last two intervals for accuracy sake.

- I found that the Age-Standardised Death Rate for both USA and UGA is as expected, where the interval Death Rate increases as age increases.
- The Age-Standardised Death Rate is higher for UGA at younger ages but the USA overtake UGA in ASDR at interval 40-44

----

- I found it perplexiing that the USA have higher Death Rate in both CDR and Age-Standardised Death Rate, I feel that this might be lack of complete account of Data from the Uganda Census.
- UGA overall lower **estimated** CDR might be attributed to younger population in general as less expected deaths in older ages.

## How to install dependencies

Declare any dependencies in `requirements.txt` for `pip` installation.

To install them, run:

```
pip install -r requirements.txt
```

To install conda env, run:
```
conda env create --file=ds_owid_jds.yml
```

## Layout

- Kedro file layout were used, kedro pipeline not tested
- Notebooks are located in ```./notebooks/EDA.ipynb``` notebooks are ran in relative paths
- Raw data are located (not tracked in git) ```./data/01_raw```
- Result data are located in ```./data/07_model_output```
- Plots output are located in ```./docs```