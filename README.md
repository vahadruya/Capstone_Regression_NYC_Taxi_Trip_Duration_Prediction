# NYC Taxi Trip Duration Prediction

<details>
<summary>Table of Contents</summary>

1. [About the Project](#about-the-project)
2. [Dataset Description](#dataset-description)
3. [Feature Engineering and Data Pre-processing](#feature-engineering-and-data-pre-processing)
4. [Model Implementation](#model-implementation)
5. [Model Evaluation and Results](#model-evaluation-and-results)
7. [Conclusion](#conclusion)
9. [Libraries Used](#libraries-used)
10. [Contact](#contact)
</details>

## About the Project

The NYC taxi trip duration dataset is a dataset released by the NYC [Taxi and Limousine Commission](https://www.nyc.gov/site/tlc/index.page), which includes several features like pickup time, dropoff time, pickup coordinates etc as possible predictors for prediction of taxi trip duration. The aim of this project is to accurately predict the trip duration using a regression model, using (but not limited to) the above features. This project also focuses on selecting the best combination of input features for accurate prediction, by combining both logical reasoning and iterations.

<div align = "right">    
  <a href="#nyc-taxi-trip-duration-prediction">(back to top)</a>
</div>

## Dataset Description

The dataset consists of various information as features in relation to a given taxi trip. They are:

*  **id** - a unique identifier for each trip
*  **vendor_id** - a code indicating the provider associated with the trip record
*  **pickup_datetime** - date and time when the meter was engaged
*  **dropoff_datetime** - date and time when the meter was disengaged
*  **passenger_count** - the number of passengers in the vehicle (driver entered value)
*  **pickup_longitude** - the longitude where the meter was engaged
*  **pickup_latitude** - the latitude where the meter was engaged
*  **dropoff_longitude** - the longitude where the meter was disengaged
*  **dropoff_latitude** - the latitude where the meter was disengaged
*  **store_and_fwd_flag** - This flag indicates whether the trip record was held in vehicle memory before sending to the vendor because the vehicle did not have a connection to the server - Y=store and forward; N=not a store and forward trip

Target variable to predict:
*  **trip_duration** - duration of the trip in seconds

<div align = "right">    
  <a href="#nyc-taxi-trip-duration-prediction">(back to top)</a>
</div>

## Feature Engineering and Data Pre-processing

*   Initially, the pickup and dropoff datetime features are converted into more meaningful variables such as the day of the week, day of the month, month of the year, and hour of the day. This allows for a better understanding of how the trip duration varies across different time periods, and also create new features which can establish temporal (daily, weekly and monthly) relationships with the trip duration.
*   Additionally, outliers of trip duration are handled by trimming extreme values and filtering pickup and dropoff coordinates within (and the near proximity of) NYC boundaries.
*   To select the combination of the most relevant features, separate datasets are created by considering different combinations of a few features of interest - namely, **passenger count**, **store_and_fwd_flag**, and **holidays**. Each of these datasets are then fit into regression models as separate iterations, which allows for a comparison of their impact on the predicting power of the models.
*   Further, the continuous variables are transformed using the appropriate transformations to ensure normal distribution of the residues. The features are scaled by applying standard scaling to ensure consistent scaling across features.

<div align = "right">    
  <a href="#nyc-taxi-trip-duration-prediction">(back to top)</a>
</div>

## Model Implementation

The scaled dataset is split into train and test dataset based on an appropriate test ratio. Seven different regression models are then implemented onto this dataset roughly in the order of increasing complexity, namely
1. Linear Regression
2. Lasso regularized linear model
3. Ridge regularized linear model
4. Polynomial regression
5. Light gradient-boosting machine
6. Decision Trees
7. XGBoost

The 2 best models out of these are then stacked together to test for further improvement.

<div align = "right">    
  <a href="#nyc-taxi-trip-duration-prediction">(back to top)</a>
</div>

## Model Evaluation and Results

The combination of **RMSE**, **R<sup>2</sup>** and **adjusted R<sup>2</sup>** are chosen as the appropriate metrics for evaluation of the regression models. The values of these metrics along with the model runtime (in seconds) for the regression from one particular iteration of input dataset were:

| Model | Train RMSE | Train R<sup>2</sup> | Train adj_R<sup>2</sup> | Test RMSE | Test R<sup>2</sup> | Test adj_R<sup>2</sup> | Runtime (s) |
| :--- |    :----:   | :---: | :---: |  :---: |  :---: |  :---: |  :---: | 
| Linear Regression | 28.321850	| 0.581448 |0.581444 |28.311827	|0.583317|0.583300	|0.427053|
| L1 regularized LR | 28.321850|0.581448|0.581444|28.311829|0.583317|0.583300|6.543669|
| L2 regularized LR | 28.321850|0.581448|0.581444|28.311834|0.583317|0.583300|3.810947|
| Polynomial Regression| 23.418874|0.653906|0.653882|23.406192|0.655516|0.655419|5.429366|
| Decision Trees | 13.972283|0.793512|0.793510|18.102460|0.733574|0.733564|246.243221|
| LightGBM| 12.051112|0.821904|0.821902|13.053452|0.807884|0.807876|379.578703|
| XGBoost | 5.952393|0.912033|0.912032|12.687642|0.813268|0.813260|1634.325324|
| Stacking |22.766780|0.663543|0.663540|25.829009|0.619858|0.619843|1986.644313|

On the basis of Test RMSE and Test R<sup>2</sup> scores, the XGBoost edges out the LightGBM in performance, which has the maximum R<sup>2</sup> and minimum RMSE. While the LightGBM had much lower model training time, it gave out feature importances not in accordance with the other models. Hence, the XGBoost is chosen as the best regression model.

<div align = "right">    
  <a href="#nyc-taxi-trip-duration-prediction">(back to top)</a>
</div>

## Conclusion

*  Overall, the XGBoost proved to be the most productive model for prediction of taxi trip durations. **distance** was adjudged to be the most important predictor, while **vendor_id** was concluded to be the least important one.than the other models in this context. Local explanation of the XGBoost using ELI5 also provided reasonable results.
*  On the iteration of input datasets by combination of certain relevant features - the dataset which dropped **passenger_count** and **store_and_fwd_flag** (due to their high class imbalance and feature prediction redundancy with respect to trip_duration) and included **holiday** as a predictor proved to be best input for the regression models, producing the best test metric scores.

<div align = "right">    
  <a href="#nyc-taxi-trip-duration-prediction">(back to top)</a>
</div>

## Libraries Used

For handling and manipulating data

<a href="https://pandas.pydata.org/" target="_blank"><img src="https://img.shields.io/badge/Pandas-black?style=flat-square&logo=Pandas&logoColor=white&link=https://pandas.pydata.org" alt="Pandas" width="84" height="25"></a>
<a href="https://numpy.org/" target="_blank"><img src="https://img.shields.io/badge/NumPy-4d77cf?style=flat-square&logo=Numpy&logoColor=white&link=https://numpy.org/" alt="Numpy" width="84" height="25"></a>
geopandas

For Visualisation

<a href="https://matplotlib.org/" target="_blank"><img src="https://img.shields.io/badge/Matplotlib-afc6d3?style=flat-square&logo=matplotlib&logoColor=white&link=https://matplotlib.org/" alt="Matplotlib" width="78" height="25"></a>
<a href="https://seaborn.pydata.org/" target="_blank"><img src="https://img.shields.io/badge/Seaborn-7db0bc?style=flat-square&logo=seaborn&logoColor=white&link=https://seaborn.pydata.org/" alt="Seaborn" width="65" height="25"></a>
<a href="https://ipython.org/" target="_blank"><img src="https://img.shields.io/badge/IPython-5781b3?style=flat-square&logo=ipython&logoColor=white&link=https://ipython.org/" alt="IPython" width="65" height="25"></a>
<a href="https://graphviz.org/" target="_blank"><img src="https://img.shields.io/badge/Graphviz-9be1f5?style=flat-square&logo=graphviz&logoColor=white&link=https://graphviz.org/" alt="Graphviz" width="70" height="25"></a>
folium

For Hypothesis testing, Pre-processing and Model training

<a href="https://www.statsmodels.org/stable/index.html" target="_blank"><img src="https://img.shields.io/badge/Statsmodels-3f51b5?style=flat-square&logo=statsmodels&logoColor=white&link=https://www.statsmodels.org/stable/index.html" alt="Statsmodels" width="98" height="25"></a>
<a href="https://scipy.org/" target="_blank"><img src="https://img.shields.io/badge/SciPy-0053a1?style=flat-square&logo=scipy&logoColor=white&link=https://scipy.org/" alt="SciPy" width="75" height="25"></a>
<a href="https://scikit-learn.org/stable/" target="_blank"><img src="https://img.shields.io/badge/Scikit%20Learn-f79939?style=flat-square&logo=scikit-learn&logoColor=white&link=https://scikit-learn.org/stable/" alt="Scikit Learn" width="115" height="25"></a>
ELI5, holidays


<div align = "right">    
  <a href="#nyc-taxi-trip-duration-prediction">(back to top)</a>
</div>

## Contact

<a href="https://www.linkedin.com/in/aditya-a-p-507b1b239/" target="_blank"><img src="https://img.shields.io/badge/Linkedin-0078b7?style=flat-square&logo=linkedin&logoColor=white&link=https://www.linkedin.com/" alt="Linkedin" width="85" height="25"></a>
<a href="mailto:apaditya96@gmail.com" target="_blank"><img src="https://img.shields.io/badge/Gmail-red?style=flat-square&logo=Gmail&logoColor=white" alt="Gmail" width="70" height="25"></a>

<div align = "right">    
  <a href="#nyc-taxi-trip-duration-prediction">(back to top)</a>
</div>

