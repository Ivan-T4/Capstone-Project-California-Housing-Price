# California Housing Price Prediction (1990 Census Data)

## Context

This project is based on the California Housing dataset from the 1990 census. Even though the dataset is historical, it provides a great opportunity to learn and practice how to build an end-to-end machine learning model for predicting house prices. Housing price prediction remains a relevant and important topic today, especially in 2025 where real estate is still a critical factor in personal finance, investment, and policy-making, but of course, many conditions have changed. While the predictions themselves may not directly apply to today’s market, the modeling process can serve as a reflection for anyone interested in applying similar methods with updated and more reliable data.

---

## Problem Statement

Predicting housing prices is always challenging because values depend on many complex factors like location, demographics, and economic conditions. In this dataset, we only have limited census-based features, so the question becomes:

*Given these features, how well can a machine learning model learn the relationship between housing and demographics to predict median house value?*

This project doesn’t aim to produce a perfect tool for 2025 housing prices, but rather to show the strengths and weaknesses of different modeling approaches and highlight what could be improved if more current data were available.

---

## Goals

- To explore how different machine learning algorithms perform in predicting house prices.

- To compare the effect of preprocessing and transformation choices on model performance.

- To identify which features play the most important role in the predictions.

- To create a learning benchmark that can help others reflect on how such models might be adapted or improved for today’s market.

---

## Dataset & Features

| **Attribute** | **Data Type** | **Description** |
| --- | --- | --- |
| `latitude` | Float64 | Latitude coordinates of the block group|x
| `longitude` | Float64 | Longitude coordinates of the block group|x
| `housing_median_age` | Float64 | Median age of the houses within the block group |
| `total_rooms` | Float64 | Total number of rooms across all houses in the block group |
| `total_bedrooms` | Float64 | Total number of bedrooms across all houses in the block group |
| `population` | Float64 | Total population living in the block group |
| `households` | Float64 | Total number of households in the block group |
| `median_income` | Float64 | Median income of households in the block group (US$) |
| `ocean_proximity` | Object | Categorical variable describing the block group’s proximity to the ocean |
| `median_house_value` | Float64 | Median house value in the block group ||

---

## Analytical Approach
The project follows a structured machine learning pipeline:

1. **Data Preparation** → handling missing values, preparing numerical and categorical features.

2. **Feature Transformation** → scaling, encoding, and considering outlier adjustments.

3. **Model Development** → training multiple algorithms, both baseline and advanced.

4. **Model Tuning** → optimizing hyperparameters to improve performance.

5. **Model Interpretation** → using feature importance and explainable AI techniques to understand predictions.

---

## Model Evaluation

Performance metrics used:
- **RMSE (Root Mean Squared Error):** Measures how far predictions deviate from actual values (lower = better).
- **MAE (Mean Absolute Error):** Average of absolute differences between prediction and true value.
- **MAPE (Mean Absolute Percentage Error):** Measures relative accuracy in percentage.


| Model | RMSE | MAE | MAPE |
|--------|------|------|------|
| **Baseline (No ML)** | 114,151 | 90,142 | 0.631 |
| **XGBoost Regressor (Tuned)** | 45,964 | 30,781 | 0.175 |
| **Transformed XGBoost Regressor (Tuned)** | 46,564 | 29,966 | 0.159 |

Using machine learning, the model **reduced RMSE by over 50%** compared to the baseline approach.

---

## Additional Information

It’s important to note that this dataset does not represent individual houses. Instead, each row corresponds to a census block group, which is a small geographic area defined by the US Census. The features such as `total_rooms`, `total_bedrooms`, and `population `are aggregated values for that block group, and the target variable (`median_house_value`) represents the median house price within that group.

---

## Conclusion

This project tested two machine learning models—tuned normal XGBoost and tuned transformed XGBoost—to predict California housing prices. Both delivered relatively strong performance given the historical dataset:

- Normal XGB: RMSE ≈ 45,964, MAE ≈ 30,781, MAPE ≈ 0.175

- Transformed XGB: RMSE ≈ 46,564, MAE ≈ 29,966, MAPE ≈ 0.159

These metrics suggest the models predict within ~15–17% of actual prices on average, which is solid for broad housing trends. The scatterplot confirmed strong alignment under $500K home values, though higher-value homes show larger deviations.

Feature importance and SHAP analysis consistently pointed to median income and ocean proximity as the strongest predictors, supported by geographic (longitude/latitude) and demographic (rooms, population) variables. While these features explain much of the variance, they are limited for modern prediction purposes.

Importantly, the project also showed that transformed regression does not always outperform normal XGB, and hyperparameter tuning plays a larger role than transformation itself. Saving the tuned pipelines with preprocessing included ensures reproducibility and interpretability.

---

## Actionable Recommendations

To improve the current model and create a more reliable housing price predictor, there are some part that can be improved:

1. #### **Modeling Improvements**

Explore newer models beyond XGBoost, such as `LightGBM`, `CatBoost`, or even `deep learning models`. Implement stacked or ensemble models for example have base learn like `XGBoostRegressor, XGBRandomForestRegressor, and Random Forest` to reduce error variance and capture both linear and nonlinear effects. And also consider using transformedtargetregressor with log in the stacked or ensemble models.

2. #### **Feature Improvements**

Add `economic variable` as features (e.g., `interest rates, employment, inflation, mortgage availability`) that strongly affect house affordability. Other variable like `neighborhood features` (e.g.,`school quality, crime rates, walkability, access to jobs/transportation`) can be crucial to affecting house price.

For more advanced variable like `environmental risk` data (e.g., `wildfire zones, flood risks, climate change effects`) can also be features that significantly influence property values today. For people who interested in **Property industry** can also include `market dynamics features` (e.g.,`rental yields, housing supply vs. demand, investor activity`) to reflect modern influences missing in historical data.

3. #### **Data Collection Improvements**

Changing from `census block-level` aggregation to `individual` property-level data would reduce error caused by averaging and lower RMSE, MAE, and MAPE. Use recent and continuous data (e.g., 2010–2025 housing transactions) instead of relying solely on 1990 data, so the model more relatable to the current economic conditions, not outdated conditions.


With these changes, in theory, the prediction error could be reduced, and the model would become more relevant for today’s housing market, but we can never rule out something that never happened before like pandemic, geo-political situation, never-happened disaster or other major things that can shift the housing price.

---
