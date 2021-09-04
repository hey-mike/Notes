# Dealing with unbalanced dataset

The conventional model evaluation methods do not accurately measure model performance when faced with imbalanced datasets.

## Collect more data

## Resampling

Standard classifier algorithms like Decision Tree and Logistic Regression have a bias towards classes which have number of instances. They tend to only predict the majority class data. The featueres of minority class are treated as noise and are often ignored. Thus, there is a high probability of misclassification of the nimority class as compared to the majority class.

### Random under-sampling

    -   Advantages: It can help improve run time and storage problems by reducing the number of training data samples when the traing data set is huge.
    -   Disadvantages
        -   It can discard potentially useful information which could be important for building rule classifiers.
        -   The sample chosen by random under sampling may be a biased sample. And it will not be an accurate representative of the population. Thereby, resulting in inaccurate results with the actual test data set.

### Random over-sampling

    -   Advantages:
        -   No information loss
        -   Outerperforms under sampling
    -   Disadvantages
        -   It increases the likelihood of overfitting since it replicates the minority class events

### Cluster-based over sampleing

    -   Advantages
        -   This clustering technique helps overcome the challenge between class imbalance. Where the number of examples representing positive class differs from the number of examples representing a negative class.
        -   Overcome challenges within class imbalance, where a class is composed of different sub clusters. And each sub cluster does not contain the same number of examples
    -   disadvanteges
        -   The main drawback of this algorithm, like most oversampling techniques is the possibility of over-fitting the traning data.

### Informed over sampling: synthetic minority over-sampling technique

    -   Advantages
        -   Mitigates the problem of overfitting caused by random oversampling as synthetic examples are generated rather than replication of instances
        -   No loss of useful infomation
    -   Disadvantages
        -   While generating sythetic examples SMOTE does not take into consideration neighboring examples from other classes. This can result in increase in overlapping of classes and can introduce additional noise
        -   SMOTE is not very effective for high dimensional data

### Modified synthetic minority oversampling technique (MSMOTE)

## Ensemble techniques
