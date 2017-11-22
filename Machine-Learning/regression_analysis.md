# Regression Analysis

## Datasets (https://archive.ics.uci.edu/ml/datasets/Housing)

- CRIM: This is the per capita crime rate by town
- ZN: This is the proportion of residential land zoned for lots larger than 25,000 sq.ft.
- INDUS: This is the proportion of non-retail business acres per town
- CHAS: This is the Charles River dummy variable (this is equal to 1 if tract bounds river; 0 otherwise)
- NOX: This is the nitric oxides concentration (parts per 10 million)
- RM: This is the average number of rooms per dwelling
- AGE: This is the proportion of owner-occupied units built prior to 1940
- DIS: This is the weighted distances to five Boston employment centers
- RAD: This is the index of accessibility to radial highways
- TAX: This is the full-value property-tax rate per $10,000
- PTRATIO: This is the pupil-teacher ratio by town
- B: This is calculated as 1000(Bk - 0.63)^2, where Bk is the proportion of people of African American descent by town
- LSTAT: This is the percentage lower status of the population
- MEDV: This is the median value of owner-occupied homes in $1000s


## RANDom SAmple Consensus (RANSAC) - fitting a robust regression model

- Select a random number of samples to be inliers and fit the model
- Test all other data points against the fitted model and add those points that fall within a user-givern tolerance to the inliers
- Refit the mole using all inliers.
- Estimate the error of the fitted model versus the inliers.
- Terminate the algorithm if the performance meets a certain user-defined threshold or if a fixed number of iterations has been reached; go back to step 1 otherwise

## Regulation

- Redge Regression
- Least Absolute
- Shrinkage and Selection Operator (LASSO)
- Elastic Net

