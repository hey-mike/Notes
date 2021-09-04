# Data prepocessing

## Dealling with Missing data

-   Eliminating samples or feature with missing values
    -   There are three types of missing data
        -   Missing Completely At Random (MCAR)
        -   Missing At Random (MAR)
        -   Missing Not At Random (MNAR)
    -   Missing categorical feature
        -   KNN to predict the missing value
        -   Fill in missing values with most frequent value
-   Imputing missing values
    -   Small amount value: KNN
    -   Imputer
-   scikit-leran estimater

## Detecting outliers

-   Looking as a whole: EllipticEnvelope
-   Looking at individual feature (IQR)

## Handling categorical data

-   Mapping ordinal freatures
-   Encodeing class labels
-   Performing one-hot encoding on nominal features

## Paritioning a dataset in training and test sets

## Bringing features onto the same scale

## Selecting meaningful features

-   Sparse solutions with L1 regularization
-   Sequential freature selection algorithms
    -   feature slection : select a subset of the original freatures
        -   Sequential Backward Selection (SBS) : reduce the dimensionality of the inital feature subspace with minimum decay in performance of the classifier to improve upon computational efficiency.
    -   feature extraction : derive information from the feature set to construct a new feature subspace.

## Assessing feature importance with random forests

-   If two or more features are highly correlated, one feature may be ranked very highly while the information fo the other feature(s) may not be fully captured. On the other hand, we don't need to be concerned about this problem if we are merely interested in the predictive performance of a model rather than the interpretation of feature importtances.
