# What Drives the Price of a Car?

## Notebook Link
(Add your notebook link here)

## Project Overview
This project analyzes used car prices using a large marketplace dataset (~426K listings) following the CRISP-DM process. The goal is to identify key drivers of price to improve dealership inventory and pricing decisions.

## Data Preparation
Data was cleaned to improve reliability and remove distortions:
- Removed missing values (price, year, odometer)
- Restricted price range ($500–$100,000)
- Removed extreme mileage (>300,000 miles)
- Dropped non-predictive identifiers (VIN, URLs)

Final dataset: ~376,956 records.

## Exploratory Data Analysis
Key observations:
- Price distribution is right-skewed  
- Newer vehicles have higher prices  
- Higher mileage lowers price  
- Fuel type, transmission, and title status show clear price differences  

## Modeling
Pipeline included:
- Scaling numerical features  
- One-hot encoding categorical features  

Models:
- Ridge Regression  
- Lasso Regression  

Hyperparameters tuned using GridSearchCV with cross-validation.

## Model Performance
- Ridge: R² = 0.4590, MSE = 111,298,551.22  
- Lasso: R² = 0.4590, MSE = 111,299,276.56  

The model explains ~45.9% of price variance, indicating moderate predictive power.

## Key Drivers
Positive:
- fuel_diesel  
- title_status_lien, title_status_clean  
- year  

Negative:
- odometer  
- fuel_hybrid, fuel_gas, fuel_electric  
- title_status_parts only  

## Recommendations
- Prioritize newer, low-mileage vehicles  
- Use title status as a filtering criterion  
- Treat diesel as a potential premium segment  
- Use model outputs to guide pricing and inventory decisions  

## Next Steps
- Add engineered features (e.g., vehicle age)  
- Incorporate additional variables (condition, location)  
- Test nonlinear models  
