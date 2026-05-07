# Forecasting the Hotel Occupancy of 17 Hotels
**Authors:** Matthew Laci & Alex Figurella | Miami University, Farmer School of Business

## Overview
The main problem that we sought to find during our project was figuring out what the future
occupancy of a hotel may be 4 weeks in advance. Within our initial dataset, we started with
information ranging from January 1st, 2022, to June 30th, 2023, covering a total of 19 hotels.

After viewing the data and its included information, we found that two hotels: Hotel 77 and
Hotel 28 contained information that indicates both hotels went out of business. These hotels were
promptly removed from our database for more accurate reading.

We also decided to include another factor in our dataset, US National Holidays. We feel that
including this information would definitely explain an increase in hotel occupancy if our dates
were to fall under that category (More people would take time off to go on trips during national
holidays, as they might already be scheduled off).

Following our data cleaning process, we decided to first establish some baseline models
including a Naïve, SeasonalNaïve, AutoETS, MSTL, and AutoARIMA. For our SeasonalNaïve,
we decided to take a last week, and a last month (last 7 days and last 30 days). Following this, we
created a statsforecasting prediction with a daily frequency, then used it for our cross-validation
to predict 28 days (4 weeks) in advance with 5 windows.

After saving our results from our cross-validation into CSV format, we promptly fixed our
datatypes into their respective categories. After this came the evaluation of our statsforecasting
models against the BIAS, MAE, RMSE, and MAPE metrics (Final Results Below).
We then moved to ML/Neural/LightGBM modeling, where we followed similar steps as 
in the
statsforecasting portion. We selected our ML models to be Lasso, KNN, Random Forest, and
Light GBM. We then evaluated our results following the same metrics as prior (BIAS, MAE,
RMSE, and MAPE). After this, we decided to evaluate once again (Final Results Below).

We then move to using TimeCopilot and the Chronos, Moirai, TimesFm, and TabPFN models.
To do so, we had to follow the same cross-validation rules set in the StatsForecast section, but
switch the models used. Following this, we once again evaluated each model with the metrics
assigned and gathered our final results to see a real winner.

## Dataset
- 17 hotel time series, daily frequency
- Date range: January 2022 – June 2023
- Target variable: occupancy rate (y), normalized between 0 and 1

## Models Compared
| Family | Models |
|--------|--------|
| Baseline | Naive, SeasonalNaive (LastWeek, LastMonth) |
| StatsForecast | AutoETS, MSTL, AutoARIMA (weekly & monthly) |
| ML | LightGBM via MLForecast |
| Neural | AutoNBEATS, AutoNHITS via NeuralForecast |
| Foundation | TimesFM-2.5, Chronos, Moirai, TabPFN via TimeCopilot |

## Key Findings
- **Best model: TimesFM-2.5** with 26 total wins across all series and metrics
- Weekly seasonality models consistently outperformed monthly counterparts
- MAPE was excluded for series with near-zero occupancy values, as it becomes undefined or extremely inflated — MAE and RMSE were used as primary metrics instead
- Foundation models showed the largest advantage on volatile, low-occupancy hotels
- AutoARIMAWeek was the strongest traditional statistical model

## Project Files
| File | Description |
|------|-------------|
| `ISA_444_Project_May6th.ipynb` | Full modeling notebook with all code |
| `cv_results.csv` | Raw cross-validation results |
| `t_cv_results.csv` | TimeCopilot cross-validation results |
| `evaluation_metrics.csv` | ME, MAE, RMSE, MAPE by series and model |
| `wins_summary.csv` | Win counts per model across all metrics |

## Reproducibility
All models use the Nixtlaverse and TimeCopilot packages only.
Install dependencies with:
```
pip install statsforecast neuralforecast mlforecast timecopilot
```

[This is the link to the public collab](https://colab.research.google.com/drive/1DeDeKUzb_QiK7au-f24IgE2nNctoHFJB?usp=sharing)
