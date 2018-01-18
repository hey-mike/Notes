# Ensemble learning

Ensemble methods: combine different classifiers into a meta-classifier that has a better generalization performance than each individual classifier alone.

Example: assuming that we collected predictions from 10 experts, ensemble methods would allow us to strategically combine these predictions by the 10 experts to come up with a prediction that is more accurate and robust than the predictions by each individual expert.

- Majority voting: select the class label that has been predicted by the majority of classifiers, that is, received more than 50 percent of the votes.Strictly speaking, it refers to binary class settings only.
- Plurality voting: select the class label that received the most votes.

## Why using logistic regression and k-nearest neighbors classifier as part of pipleline?

Both algorithms(using the Euclidean distance metric) are not scale-invariant in contrast with decision trees.

## Bagging ( boostrap aggregating)

The convertional baggin algorithm involves generating 'n' different boostrap training samples with replacement. And training the algorithm on each boostrapped algorithm separately and then aggregating the predictions at the end.

Bagging is used for reducing overfitting in order to create strong learners for generating accurate predictions. Unlike boosting, baggin allows replacement in the boostrapped sample.

- Advantages
  - Improves stability & accuracy of machine leraning algorithms
  - Reduces variance
  - Overcomes overfitting
  - Improved misclassification ratre of the bagged classifier
  - In noisy data enviroments bagging outperforms boosting
- Disavantages
  - Bagging works only if the base classifers are not bad to begin with. Bagging bad classifiers can further degrade performance
 
## Adaptive Boosting (weak learner)

Ada Boost is the first original boosting technique which creates a highly accurate prediction rule by combining many weak and inaccurate rules. Each classifer is serially trained with the goal of correcly classifying examples in every round that were incorrectly classified in the previous round.

For a learned classifier to make strong predictions, it should follow the follwing 3 conditions:

- The rules should be simple
- Classifier should have been trained on sufficient number of training examples.
- The classifer should have low training error for the traning instances

Advantages

- Very simple to implement
- Good generalization - suited for any kind of classification problem 

Disadvantages

- Sensitive to noisy data and outliers
