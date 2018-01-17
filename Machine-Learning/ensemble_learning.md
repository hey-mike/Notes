# Ensemble learning

Ensemble methods: combine different classifiers into a meta-classifier that has a better generalization performance than each individual classifier alone.

Example: assuming that we collected predictions from 10 experts, ensemble methods would allow us to strategically combine these predictions by the 10 experts to come up with a prediction that is more accurate and robust than the predictions by each individual expert.

- Majority voting: select the class label that has been predicted by the majority of classifiers, that is, received more than 50 percent of the votes.Strictly speaking, it refers to binary class settings only.
- Plurality voting: select the class label that received the most votes.

## Why using logistic regression and k-nearest neighbors classifier as part of pipleline?

Both algorithms(using the Euclidean distance metric) are not scale-invariant in contrast with decision trees.

## Bagging ( boostrap aggregating)

## Adaptive Boosting (weak learner)
