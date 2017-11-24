# Scifit-learn

**Overfitting** means that the model captures the patterns in the training data well, but fails to generalize well to unseen data.

- Training data: the slited data used to build machine learning model
- Test data: the reset of the data is used to assess how well the model words
- In scikit-learn, data is usually denoted with a capital X, while labels are denoted by a lowercase y. This is inspired by the standard formulation f(x) = y in mathematics, where x is the input to a function and y is the output.
- X (capital) represents two-dimensional array ( a matrix) and a lowercase y represents one-dimensioanl array (a vector)

## Pair plot

It is difficult to plot datasets with more than three features, due to computer have only two dimentsions, which allows us to plot only two (or maybe three) features at a time.
Pair plot looks at all possible pairs of features


## Decision Tree

- **Advantages**
  - The resulting model can easily be visulized and understood by noexperts (at least for smaller trees),.
  - The algorithms are completely invariant to scaling of the data.
- **Disadvantage**
  - Even it use pre-pruning, they tend to overfit and provide poor generalization performance

