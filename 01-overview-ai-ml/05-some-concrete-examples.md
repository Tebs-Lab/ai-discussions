# Some Concrete Examples of ML Algorithms

For each of these, describe the basics and draw an example of them working on some two dimensional data. If you're most familiar with models other than the ones listed here, talk about those.

The purpose of this is to make the idea of ML concrete before discussing it in more detail. When ML seems like magic it's much harder to conceptualize the rest of the topics, so having a basic understanding of how at least a few models *REALLY* work is super helpful.

## Linear Regression

* Expects linear relationships between data.
* Fits a line to that data.
* Works in many dimensions, but never works well with curves, cyclical patterns, or any other non-linear pattern.

## Decision Trees

* Iteratively splits the data into more and more homogenous "buckets" 
    * Using the gini index, entropy, or variance from the mean (engineers choice) to quantify that "homogeneity"
* Every time we make a split we consider every possible split point for every single feature and pick the split that maximizes our 
* Can be controlled with "hyperparameters" such as:
    * Max depth of the tree
    * Max number of leaf nodes
    * Minimum number of items in a node to split it.
    * ...

## Ensemble: Random Forests

* Ensembling in general is using multiple ML models to make a single prediction.
    * By having them "vote"
* Random Forests are a specific type of ensemble where we use:
    * Bagging/Bootstrap Aggregation/Sampling with replacement to create variance at the data level.
    * Feature selection to create variance at the level of the specific splits chosen by each tree.
* Often we'll train ~100-200 trees per forest. 

## Gradient Boosting

* Gradient boosting relies on sequential application of "weak learners" where each subsequent model is trained to predict the error of the chain of models ahead of it. 