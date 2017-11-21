# Model evaluation and Hyperparameter tuning

## Holdout cross-validation

A classic and popular approach for estimating the generalization performance of machine learning models is holdout cross-validation.

**Model selection**: tuning and comparing different paramenter settings to further improve the performance for making predictions on unsee data, it refers to a givent classifcation problem for which we want to select the optimal values of tunning parameters. (**Hyperparameters**)

A better way of using holdout method for modle selection is to separate the data into three parts: a traning set, a validation set, and a test set.

The advantage of having a test set that the model hasn't seen before during the training and model selection steps is that we can objtain a less biased estimate of its ability to generalize to new data.

A disadvantage of the holdout method is that the preformance estimate is sensitive to how we partition the training set into the training and validation subsets

## K-fold cross-validation

Randomly split the training dataset into k folds without replacement, wheere k - 1 folds are used for the model training and on fold is use for testing. This procedure is repeated k times so that we obtain k models and performance estimates.

Random sampling without replacement: 2, 1, 3, 4, 0
Random sampling with replacement: 1, 3, 3, 4, 1

## Debugging algorithms with learning and validation curves

- Diagnosing bias and variance problems with learning curves
- Addressing overfitting and underfitting with validation curves
- Fine-tuning machine learning models via grid search
- Algorithm selection with nested cross-validation
- Looking at different performance evaluation metrics
  - precision
  - recall
  - F1-score
  - Receiver operator charateristic (ROC): this graphs are useful tools for selecting models for classification based on their performance with respect to the false positive and ture positive rates, which are computed by shifting the decision threshold of the classifer.
  - Area under the cureve (AUC) can be computed based on ROC curve to charaterize the performance of a classification model
