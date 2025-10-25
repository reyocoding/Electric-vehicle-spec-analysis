# Electric vehicle spec 2025

Table of Contents :

- [Project Background](#project-background)
- [Dataset Overview](#dataset-overview)
- [Insights Deep-Dive](#insights-deep-dive)
  - [Market Segmentation](#market-segmentation)
  - [Performance Metrics](#performance-metrics)
  - [Efficiency Analysis](#efficiency-analysis)
- [Prediction Model](#prediction-model)
  - [Feature Selection](#feature-selection)
  - [Training & Model Performance](#training--model-performance)
- [Conclusion](#conclusion)

## Project Background

This project explores a dataset containing specifications of various EVs available globally in 2025. The goal is twofold:

1. To extract insights about EV performance, efficiency, and market trends through exploratory data analysis (EDA).
2. To build a predictive model that estimates the **driving range** of an EV based on technical features such as battery capacity, drivetrain, efficiency, and more.

## Dataset Overview

The dataset shape is as follows:
![Untitled](files\untitled.png)

## Insights Deep-Dive

### Market Segmentation

This bar chart represents the top 10 EV brands in terms of models number :
![image](files\image_2.png)
We can see that:

- Mercedes-Benz is at the top with 42 models
- Secondly, Audi with 28 models
- The remaining brands follow, with BYD at the 10th spot with 17 models.

 ---
This bar chart represents EV body types by drivetrain type :
![image](files\image.png)
According to the chart :

- AWD (All-Wheel-Drive) is the most common drivetrain.
- RWD (Rear-Wheel-Drive) is the least common drivetrain.

When it comes to the car body types :
 **"SUV"** is most common type of body that also feature all types of drivetrain with:

- 110 models using AWD
- 62 using FWD
- 72 using RWD

On the other hand **"Coupe"** body type is the least with only having AWD EVs

### Performance Metrics

The scatter plot below illustrates the relation between the battery capacity and the range for each drivetrain type :
![image](files\image_4.png)
And we can tell that :

- A large portion of AWD models have a higher battery capacity and higher range, with an average battery capacity of 88.58 kwh.
- FWD models tend to have less battery capacity 55.50 kwh on average and with less range output
- RWD models have some variation in battery capacity with different ranges but tends to settle between AWD & FWD , on average RWD have a battery capacity of 74.93 kwh with Q1 (25%) 62 kwh and Q3(75%) of 86 kwh.

To further investigate this is a box plot that shows the range by drivetrain :

![image](files\image_l.png)
We can see that:

- AWD vehicles have the highest average range, around 454 km with most models ranging between 320 and 640 km with outliers that can reach up  to 665 km.
- RWD models have an average of 418 km , most RWD vehicles fall between 235 and 610km.
- FWD vehicles have the **lowest average range** at **298 km**. Their range spans from **135 km to around 500 km**

### Efficiency Analysis

The box plot displays the **efficiency** (in Wh per km) for each vehicle segment. Lower values indicate better energy efficiency.
![image](files\image_6.png)

- mini cars are the most energy efficient segment ,with the lowest average around 120 (wh per km).
- compact and medium segments also show low energy consumption with tight interquartile ranges (IQRs), suggesting consistent performance within those categories.
- Large & Executive segments have a higher average than compact and medium segments but with more variety as shown by the wide IQR .
- Luxury segment are less efficient with an average of 183 (wh per km)  but show variances and outliers with lower energy efficiency meaning some models are designed with performance-focused efficiency optimizations.
- Passenger Van segments are the least energy efficient with the highest median "202" (wh per km) and the widest spread.

## Prediction Model

### Feature Selection

Our target variable is the "Range" column
We want to make a model that can accurately predict the range of the EV according to its specs.
The dataset includes 22 columns. In order to improve the models accuracy we need to reduce the number of Features (columns/vehicle specs) for achieving the best result.
The following columns are considered the most important features for the model.

- Top\_speed\_kmh
- Battery\_capacity\_kwh
- Torque\_nm
- Efficiency\_wh\_per\_km
- Acceleration\_0\_100s
- Fast\_charging\_power\_kw
- Drivetrain (AWD - FWD - RWD)

A correlation matrix below shows the relationships between the features (numerical ones) :
![image](files\image_s.png)
The 'Drivetrain' column contains text values like AWD, FWD, and RWD instead of numbers. Since machine learning models need numerical data to work with, we have to convert these text categories into a format the model can understand.
We'll use a technique called one hot encoding, which creates separate columns for each drivetrain type. So instead of one 'Drivetrain' column with text, we'll have three new columns:

- One for AWD (1 if the car is AWD, 0 if not)
- One for FWD (1 if the car is FWD, 0 if not)
- One for RWD (1 if the car is RWD, 0 if not)

### Training & Model Performance

Since the features and the target variable are numerical values the best model to use is :

- "Linear Regression" model

We use Python with libraries like (pandas,numpy,matpotlib,sklearn) to train ,evaluate and plot the results .
You can check the full model code on `prediction\_model.ipynb` and the excel file .
After training the model here is the prediction results :
![image](files\image_7.png)
The results show that :

- The model has an R-squared of 0.94, which means it explains 94% of the variability in the target variable (the actual range). This indicates that the model is a very good fit for the data.
- The model have a MAE (mean absolute error) of 22 meaning its predicting on average  ± 22km from the actual range

This scatter plot illustrates the model's predictions vs the actual values:
![image](files\image_1.png)

## Conclusion

In this project, we successfully conducted an in-depth analysis of the 2025 EV market and developed a predictive model for vehicle range. Our findings highlight key market trends, such as the dominance of Mercedes-Benz and the prevalence of AWD SUVs. The exploratory analysis revealed a strong correlation between battery capacity and range, as well as distinct efficiency profiles across different vehicle segments.
Our linear regression model proved highly effective, explaining 94% of the variability in EV range with an average prediction error of just ±22 km. This demonstrates its potential as a valuable tool for stakeholders, from manufacturers to consumers, to estimate a vehicle's range based on its technical specifications.
