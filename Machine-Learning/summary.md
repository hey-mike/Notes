# Summary of machine learning

## Common used machine learning algorithm

Listed in order of increasing complexity:

- Logiistic regressiong
- K-nearest neighbors - Number of nearest neighbors to average
- Decision trees - Splitting criterion, max depth or tree, minimum saples needed to make a split
- Kernel SVM - Kernel type, kernel coefficient, penalty parameter
- Random forest - Number of trees, number of features to split in each node, splitting criterion, minimum saples needed to make a split
- Boosting - Number of trees learning rate, max depth of tree, split in each node, splitting criterion, minimun samples needed to make a split

## General procesdure

- **Project Scoping / Data Collection**
- **Inspect & Explore**
- **Data preprocessing**
  - formating, cleaning and sampling
  - Data Transformation:
    - Scalling
    - Label coding 
    - One hot encoding for categorical feature
- **Feature engineering** :It is the process of transforming raw data into features that better represent the underlying problem to the predictive models, resulting in improved model accuracy on unseen data
  - Indicator Variables
    - Indicator variable from thresholds
    - Indicator variable from multiple features
    - Indicator variable for special events
    - Indicator variable for groups of classes
  - Interaction Features
    - Sum of two features
    - Difference between two features
    - Product of two features
    - Quotient of two features
  - Feature Representation
    - Date and time features
    - Numeric to categorical mappings
    - Grouping sparse classes
    - Creating dummy variables
  - External Data
    - Time series data
    - External API's
    - Geocoding
    - Other sources of the same data
  - Error Analysis (Post-Modeling)
    - Start with larger errors
    - Segment by classes
    - Unsupervised clustering
    - Ask colleagues or domain experts
- **Feature selection**
    - It is a process where you automatically select those features in your data that contribute most to the prediction variable or output in which you are interested
- **Dimensionality reduction**
  - PCA
- **Split train and test data set**
- **Train data**
- **Model evaluation and hyperparameter tuning**
- **Save and deploy model**


## Dealling with umblanced dataset

**Problem**
The conventional model evaluation methods do not accurately measure model performance when faced with imbalanced datasets.

Standard classifier algorithms like Decision Tree and Logistic Regression have a bias towards classes which have number of instances. They tend to only predict the majority class data. The featueres of minority class are treated as noise and are often ignored. Thus, there is a high probability of misclassification of the nimority class as compared to the majority class.

- Random under-sampling
  - Advantages: It can help improve run time and storage problems by reducing the number of training data samples when the traing data set is huge.
  - Disadvantages
    - It can discard potentially useful information which could be important for building rule classifiers.
    - The sample chosen by random under sampling may be a biased sample. And it will not be an accurate representative of the population. Thereby, resulting in inaccurate results with the actual test data set.
- Random over-sampling
  - Advantages:
    - No information loss
    - Outerperforms under sampling
  - Disadvantages
    - It increases the likelihood of overfitting since it replicates the minority class events
- Cluster-based over sampleing
  - 

## Reference

Books:

- Introduction to Machine Learning with Python
  - review: get general ideas of how machine learning works
- Real-World Machine Learning
  - review: books follows general procedure to implement a machine learning model
- Python Machine Learning
  - review: it is a good book to advance machine learning knowledge with scikit-learn
- Pythoe Machine Learning Blueprints
  - review: a good book to build a full stack machine learning system with serveral examples

Online courses:

- Coursera - Machine Learning by Stanford University
  - review: A free open class designed by Standford University, this course teaches machine learning knowledge from basis to advance.
