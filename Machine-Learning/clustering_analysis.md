# Unsupervised learning - Clustering

Clustering (cluser analysis) is a technique that allows us to find groups of similar objects, objects that are more related to each other than to objects in other groups.
Exaples of business-oriented applications of clustering include the grouping of documents, music, and moviews by different topics, or finding customers that share similar interests based on common purchase behaviors as a basis for recommendation egines.

## k-means
It belongs to the cateory of protoype-based clustering.

- Drawbacks
  - One or more clusters can be empty
  - we have to specify the number of clusters, k, a priori

## Hard VS Soft clustering

Hard clustering: a family of algorithms where each sample in a dataset is assigned to exactly on cluster.
Soft clustering: sometimes called fuzzy clustering, it assign a sample to one or more clusters.

- fuzzy C-mean (FCM, also called soft k-means or fuzzy k-means).

## hierachical

- agglomerative
  - single linkage
  - complete linkage
- divisive clustering

## density-based clustering 

Density-based spatial Clustering of Applications with Noice (DBSCAN)

Advantages:it does not assume that the clusters have a spherical shape as in k-means.

Disadvantage: With an increasing number of features in our dataset -assuming a fixed number of training examples - the negative effect of curse of dimensionality increases.
