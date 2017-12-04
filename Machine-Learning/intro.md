# Introduction

## Rule-based system VS Machine learning

1. The logic required to make a decision is specific to a single domain and task. Changing the task even slightly might require a rewrite of the whole system.
1. Designing rules requires a deep understanding of how a decision should be made by a human expert.

Machine learning summarized in four categories.

- Predictive learning: comprises two kinds of tasks where we aim to either predict a continuous valued phenomenon (like the future location of a celestial body), or distinguish between distinct kings of things (like different faces in an image)
- Feature design: A broad set of engineering and mathematical tools which are crucial to the successful performance of predictive learning models in practice.
- Function approximation: It is employed when we know too little abut a dataset to produce proper features ourselves (and therefore must learn them strictly from the data itself).
- Numerical optimization  powers the first three and is the engine that makes machine learning run in practice.

## Cost function
One of the key ingredients of supervised machine learning algorithms is to define
an objective function that is to be optimized during the learning process. This
objective function is often a cost function that we want to minimize.

## Basic process

- Define task
- Collect data
- Design features
- Train model
- Test model

## Predictive learning problems

1. Regression:
2. Classification: The key difference between the two is that instead of predicting a continuous-valued output (e.g., share price blood pressure, etc.), with classification what we aim at predicting takes on discrete values or classes.

## Three types of machine learning

- Supervised learning (making predictions about the future):
  - **supervised** refers to a set of samples where the desired output signals (lables ) are already known.
  - There are two sub categories:
    - **classification**: the goal is to predict the categorical class labels of new instances based on the pas observations, which is a choice from a predfined list of possibilities.
      - _i.e. distinguish spam and non-spam email_
    - **regression**: for predicting continuous outcomes, given a number of _predictor_ ( explanatory) variables and a continuous response variable (outcome), and we try to find a relationship between those variables that allows us to predict an outcome.
      - _i.e. predict a relationship between the time spent studying for the test and the final scores_
  - examples:
    - Identifying the ZIP code from handwritten digits on an envelope.
    - Determining whether or not a tumor is benign based on a medical image.
    - Detecting fraudulent activity in credit card transactions

A easy way to distinguish between classifcation and regression tasks is to ask whether there is some kind of continuity in the output.

- Unsupervised learning (Discovering hidden structures):
  - In uservised learning, we know the right answer beforehand when we train our model, and in reinforcement learning, we define a measure of reward for particular actions by the agent. In unsupervised learning, however, we are dealling with unlabeled data or data of unkow structure.
  - **cluster**: is an exploratory data analysis technique that allows us to organize a pile of information into meaningful subgroups (_clusters_) without having any prior knowledge of their group menmeberships.
    - _i.e._ it allows marketers to discover customer groups based on their interests in order to develop distinct mareting programs
  - **dimensionality reduction**
    - It is a commonly used approach in feature preprocessing to remove noise from data, which can also degrade the predictive performance of certain algorithms, and compress the data onto a smaller dimensional subspace while retaining most of the relevant information. 
  - Examples:
    - Identifying topics in a set of blog posts.
    - Segmenting customers into groups with similar preferences.
    - Detecting abnormal access patterns to a website.

unsupervised algorithms are used offten in an explortory setting, when a data scientist wants to understand the data better, rather than as part of a larger automatic system. Another common application for unsupervised algorithms is as a preprocessing step for supervised algorithms.

- reinforcement learning (Solving interactive problems):
  - The goal is to develop a system (_agent_) that improves its performance based on interactions with the _enviroment_.
    - _i.e. chess engine_, the agent decides upon a series of moves depending on the state of the board (the enviroment) and reward can be difned as _win_ or _lose_ at the end of the game


## Predictive modeling

- Preprocessing
  - Feature extraction and scalling
  - Feature selection
  - Dimensionality reduction
  - sampling
- Learning
- Evaluation
- Prediction


## Feature python libaries

- NumPy
- SciPy
- scikit-learn
- pandas
- matplotlib
