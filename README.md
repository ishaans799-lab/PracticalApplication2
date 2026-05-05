# What Drives the Price of a Car?

Notebook Link
Main analysis notebook: PriceOfCarAnalysis.ipynb
Project Overview
This project investigates what drives used car prices using a large marketplace dataset (initially ~426K listings). The analysis follows the CRISP-DM process:

Business Understanding
Data Understanding & Cleaning
Exploratory Data Analysis (EDA)
Modeling
Evaluation
Findings and Recommendations
The dealership-focused objective is to identify the strongest predictors of price so inventory sourcing and pricing decisions can be improved.

Data Preparation Summary
The raw dataset was cleaned to improve model reliability and reduce distortion from missing/invalid values and extreme outliers.

Cleaning steps included:
Removing records missing core fields (price, year, or odometer)
Restricting prices to a realistic range ($500 to $100,000)
Filtering extreme mileage values (vehicles above 300,000 miles removed)
Dropping non-predictive identifiers (such as VIN/URL-type fields)
After cleaning, the working dataset contained approximately 376,956 records.

Exploratory Data Analysis Highlights
EDA was used to inspect price behavior across numeric and categorical factors and to validate modeling assumptions.

Key patterns observed:
Price distribution is skewed, with many lower/mid-priced vehicles and a long upper tail.
Newer vehicles generally trend higher in price.
Higher odometer values are associated with lower prices (depreciation effect).
Category-level differences (fuel type, transmission, title status) show meaningful price separation.
These patterns supported the selection of both numeric and categorical inputs for supervised regression.

Modeling Approach
A preprocessing + modeling pipeline was used:

Numerical features were scaled
Categorical features were one-hot encoded
Regularized linear models were trained and tuned:
Ridge Regression
Lasso Regression
Hyperparameters were selected using Grid Search with cross-validation
This approach balances interpretability with stability and helps reduce overfitting in high-dimensional encoded feature space.

Model Performance
Both regularized models produced nearly identical performance.

Test-set evaluation:
Ridge: R² = 0.4590, MSE = 111,298,551.22
Lasso: R² = 0.4590, MSE = 111,299,276.56
Interpretation:
The models explain about 45.9% of observed price variance.
Performance is moderate: the model captures major pricing structure, but unobserved factors (trim, local demand, accident history detail, options/packages, etc.) likely explain remaining variance.
Coefficient-Based Insights
Model coefficients were used for directional interpretation of major drivers.

Strong positive drivers (examples from output):
fuel_diesel (largest positive categorical effect)
title_status_lien
title_status_clean
year (newer model years increase predicted price)
Strong negative drivers (examples from output):
odometer (major depreciation signal)
fuel_hybrid, fuel_gas, fuel_electric (relative to model baseline category)
title_status_parts only
Business Recommendations for a Dealership
Based on the fitted model and coefficient patterns:

Prioritize newer, lower-mileage acquisitions
Model year and odometer consistently influence value, so procurement thresholds should emphasize recency and mileage quality.

Use title status as a hard screening feature
Clean/lien categories are associated with stronger valuations, while parts-only status is strongly unfavorable.

Treat diesel premium as an opportunity, not a blanket rule
Diesel shows a strong positive signal in this sample; combine that signal with local market demand and reconditioning cost before purchasing.

Apply model outputs as decision support
Use predictions and feature effects to shortlist inventory and set pricing bands, while still incorporating domain checks not captured in the dataset.

