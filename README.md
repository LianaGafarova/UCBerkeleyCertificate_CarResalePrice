# What drives the resale price of a used car?

## Business Understanding

The objective of this project was to identify the key factors affecting the resale price of used cars. As a part of the analysis, we evaluated whether the price of the car is driven by the following factors: region, year, manufacturer, model, condition, fuel, cylinders, odometer, title status, transmission, drive, size, type, paint color and state.

## Data Understanding
Several steps were taken to get to know the dataset and identify any data quality issues with the dataset.

1. Review of the columns in the dataset to ensure understanding of all the potential variables for the analysis.

2. Review of the rows in the dataset to identify duplicate records, outliers, records with missing values that can be excluded from the analysis sample

3. Review of the final analysis sample to identify any bias in the data (the data represent only certain categories of cars)

## Data Preparation

We confirmed that there are no duplicate records on the data based on "id".
We found a significant number of records with missing or duplicate VIN numbers. Since VIN would not be used for model development, we decided to keep the records.
The small sample of records with missing data for the continous variables were excluded from the analysis sample.
A "missing" category was defined for the categorical variables with missing data.
We applied log transformation to the car price and confirmed that the distribution of log-price looks normal.
We analyzed the relationship between log-price and independent variables to make a decision on the final list of variables to keep in the model.
We hot encoded the categorical variables.
We prepared train (70%) and test (30%) samples for model development.

## Modeling

We developed five different models:

1. Linear regression
2. Ridge regression
3. Lasso regression
4. Feature Selection using Lasso
5. Linear Regression with 2-Degree Polynomial Features based on 20 selected variables
 
Models were validated using both train/test and k-fold validation techniques. Mean Squared Error (MSE) was used to compare the error in the prediction for different modelling methodologies. Grid search was applied to find the optimal alpha values for ridge and lasso regression.

## Evaluation

Below is the summary of our observations:

- The multiple linear regression model was built as a benchmark model,but ended up being top second model based on performance
- Ridge and Lasso regresisons had comparable performance
- A more condenced model was developed with 20 features using sequential forward selection but it came at a cost of higher MSE
- The best model was the 2-degree polynomial features linear regression, based on 20 features selected with sequential forward selection in the previous step. Ideally, it would make sense to try to build this model using all the features, but the process is very computationally intense and the job would take a very long time and may never finish.

The following variables are the top predictors in the model:

- Condition of the car (Fair, Salvage)
- Number of cylinders (4, 6)
- Fuel type (gas, hybrid and other)
- Drive type (fwd and missing)
- Size (missing)
- Type (pickup, truck and other)
- State (FL, ME, OR)
- Year
- Odometer

This analysis has the following limitations:

- There are a large number of records with missing and other values. Instead of imputing these values, we decided to use hot encoding after assigning missing and other to different categories, which increased the dimensionality of the dataset.
- The data was very granular for variables such as region, model and state. All this information may be valuable in predicting a price of a car, but having all of thse variables one-hot-encoded produces a very large dataset. If there was a way to consolidate these features to have fewer values, the analysis could be expanded.
- Given that there were outliers in the data (very old cards dated as of 1900) and very expensive luxury cars, building a set of segmented models instead of one model could also improve the prediction quality. For example, we could build a separate model for luxury cars and another model for economy cars. We can also build a different model for very old antique cars and another model for newer cars.

We made the following recommendations to our client:

- Newer cars tend to have a much higher resale value.
- Cars with more than 50K miles on them have a much lower resale value.
- In addition to age and mileage, other important factors for the resale value are condition, number of cylinders, fuel and drive type
  
We identified opportunities to further enhance the prediction by improving quality of the data and potentially developing separate models for luxury and antique cars as well as different types of cars.

You can find the Jupyter notebook in this location: 
