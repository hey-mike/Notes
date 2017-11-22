# Embedding a machine learning model to web application

## Serializing fitted scikit-learn estimaters

Training a machine learning model can be computationally quite expensive.

- Model persistence (pickle): serialize and de-serialize Python object structures to compact byte code, so that we can save our classifer in its current state and reload it if we want to claasify new samples without needing to learn the modle from the training data all over again.
