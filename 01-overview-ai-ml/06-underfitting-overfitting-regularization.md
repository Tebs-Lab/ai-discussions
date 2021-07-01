# Underfitting, Overfitting, and Regularization

Keep it high level and go kind of fast! These are topics that are "in the weeds" from the perspective of most of the students, even though they are still very important concepts the actual implementation details can be confusing and unhelpful.

## Underfitting

* An underfit model is one that has not really learned much during the training process. 
* It performs poorly even on data that it has seen during training.

## Overfitting

* An overfit model has memorized the patterns in the training data without finding patterns that are general to the phenomenon being studied.
* Such models will perform well on the training data, but generally fail badly on the test data.
* This is like a student who has memorized the answers to a math exam, but doesn't actually know how to do the math.
    * If I just change the numbers but leave the wording of each problem exactly the same, this student will still fail the exam.

## Regularization

* Regularization is a general term for any tactic that will improve the chances that our model finds generalizable patterns, not just patterns specific to the training data.
    * Generally speaking applying regularization will decrease performance on the training set, but improve performance on held-out data (e.g. the test set)

* Lasso/Ridge for Linear Regression
    * Essentially these two algorithms introduce caps on the errors, which causes the underling algorithm to be less impacted by outliers.

* Decision Tree Regularization
    * Max depth, max leaf nodes, min sample to split are all examples of regularizing hyperparameters. 
    * They constrain the algorithm's ability to keep splitting the data into a bunch of buckets with exactly one data point in them (which would be perfectly homogenous, but definitely risks overfitting.)

* RF and Relation to Over/Underfitting
    * Ensembles in general make it harder to overfit, since many models have to agree on the answer.

* Learning Rate in Gradient Boosting
    * In GBMs the idea of a learning rate allows engineers to scale down each of the individual functions (in the very literal sense of multiplying it's output by some fraction), which results in less overfitting.