# NYC Taxi Trip Duration Prediction

<details>
<summary>Table of Contents</summary>

1. [About the Project](#about-the-project)
2. [Dataset Description](#dataset-description)
3. [Feature Engineering and Data Pre-processing](#feature-engineering-and-data-pre-processing)
    + [Handling Missing values](#handling-missing-values)
    + [Feature Manipulation](#feature-manipulation)
    + [Handling outliers](#handling-outliers)
    + [Iterations](#iterations)
    + [Data Splitting, Balancing and Scaling](#data-splitting-balancing-and-scaling)
4. [Model Implementation](#model-implementation)
5. [Model Evaluation](#model-evaluation)
6. [Results](#results)
7. [Conclusion](#conclusion)
8. [Challenges Faced](#challenges-faced)
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
*  **pickup_latitude* - the latitude where the meter was engaged
*  **dropoff_longitude** - the longitude where the meter was disengaged
*  **dropoff_latitude** - the latitude where the meter was disengaged
*  **store_and_fwd_flag** - This flag indicates whether the trip record was held in vehicle memory before sending to the vendor because the vehicle did not have a connection to the server - Y=store and forward; N=not a store and forward trip

Target variable to predict:
*  **trip_duration** - duration of the trip in seconds

<div align = "right">    
  <a href="#nyc-taxi-trip-duration-prediction">(back to top)</a>
</div>

## Feature Engineering and Data Pre-processing
