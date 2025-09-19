### Project Title

**Author**

#### Executive summary
This project aims to predict **shipping time** for shipments based on their attributes — such as route, mode (Air/Ocean), weight, cost, and shipping company details. Using the Kaggle Shipping Optimization Challenge dataset, I performed data cleaning, feature engineering, and exploratory data analysis (EDA) to understand key drivers of shipping time. Early results show that **shipment mode** (Air vs. Ocean) and **route/company combinations** are the dominant predictors, with significant differences in average transit time and variance. This sets the foundation for building predictive models that can improve estimated times of arrival (ETAs) and help logistics teams make better planning decisions.

#### Rationale
Accurate shipment time predictions are crucial for logistics companies. Overly optimistic ETAs can lead to missed service-level agreements (SLAs), customer dissatisfaction, and added operational costs, while overly conservative ETAs may reduce competitiveness. Understanding which factors drive shipping time enables businesses to proactively manage routes, allocate capacity, and set realistic customer expectations — ultimately improving efficiency and customer trust.

#### Research Question
Can we accurately predict shipment delivery time based on shipment characteristics (route, mode, cost, weight, company, etc.) so that we can provide reliable ETAs and optimize logistics planning?

#### Data Sources
The primary data source is the **[Shipping Optimization Challenge dataset on Kaggle](https://www.kaggle.com/datasets/salil007/1-shipping-optimization-challenge)**.  
- **Training data:** Shipment-level records with columns such as `shipment_mode`, `pick_up_point`, `drop_off_point`, `source_country`, `destination_country`, `freight_cost`, `gross_weight`, `shipment_charges`, `shipping_company`, and the target `shipping_time`.  
- **Company details file:** Enrichment data with cut-off times, processing days, turnaround times, and capacity bands for each company/route combination.

### Methodology
1. **Data Cleaning & Feature Engineering**
   - Parsed and extracted `send_timestamp` features (year, month, day, hour).
   - Created derived features like `route`, capacity spans, and numeric encodings for processing days.
   - Merged company details with shipment records to add operational context.
2. **Exploratory Data Analysis (EDA)**
   - Analyzed distribution of shipping times (multi-modal: Air tightly clustered, Ocean long-tailed).
   - Generated boxplots, scatterplots, and grouped summaries by mode/route/company.
   - Identified key drivers: mode, route, company.
3. **Modeling**
   - Used **target encoding** for categorical variables to reduce dimensionality.
   - Trained and compared several models: Naïve Median, Linear Regression, Random Forest, and HistGradientBoosting.
   - Evaluated models with **MAE**, **RMSE**, and **% of predictions within ±12 hours**.
4. **Model Selection**
   - Chose **Random Forest (TE)** for its lowest MAE and best balance of performance, interpretability, and robustness.

#### Results
| Model | MAE | RMSE | % within ±12h |
|------|------|------|---------------|
| **Random Forest (TE)** | **4.08** | 6.99 | **91.0%** |
| Linear Regression (TE) | 4.24 | **6.87** | 93.7% |
| Naïve Baseline | 7.57 | 12.81 | 70.4% |

**Key Insights**
- Random Forest (TE) reduced MAE by **46%** compared to the naïve median baseline.
- Over **9 out of 10 shipments** were predicted within ±12 hours of actual delivery time — a strong operational KPI.
- Feature importance confirms shipment mode, route, and company as top predictors — actionable levers for planners.

**Visual Summary**
![MAE Comparison](MAE_plot.png)  
![% within ±12h Comparison](accuracy_plot.png)

#### Next steps
- **Refinement:**  
  - Tune RF hyperparameters (tree depth, min samples per leaf) for marginal gains.
  - Build separate models for Air vs. Ocean to capture different dynamics.
- **Advanced Modeling:**  
  - Implement **quantile regression** for ETA bands (P50/P90) to provide uncertainty ranges for planners.
  - Evaluate Gradient Boosting (LightGBM/XGBoost) for improved speed and feature interpretability.
- **Deployment Considerations:**  
  - Automate feature pipelines (timestamp parsing, target encoding).
  - Integrate into a dashboard or API to deliver ETA predictions to business users.

#### Outline of project

- [Link to notebook 1]()



##### Contact and Further Information
