# Cross Validation:

There are many kinds of cross validation, see https://scikit-learn.org/stable/modules/cross_validation.html for more details. In this lab we're going to use something called k-fold cross validation (because it is the default for SKLearn's hyperparameter search methods) but we strongly suggest experimenting with methods, especially "stratified k-fold" cross validation, which can also be easily applied to hyperparameter search using SKLearn. 

K-Fold cross validation separates your training dataset into K different training and validation sets, ensuring that each datapoint occurs in exactly one of the validation sets, and therefore appears in K-1 training sets. Take a look at this picture from the SKlearn docs:

![K-Fold Cross Validation Visualized.](https://scikit-learn.org/stable/_images/sphx_glr_plot_cv_indices_0041.png)

Cross validation is more expensive computationally than having a single training/validation split, but it provides a more robust estimate of our model's performance and generalization. Generally, when we have found the hyperparameter set we like via cross validation, we retrain the model one more time with ALL the training data before evaluating our results on a held-out test set. 

Stratified K-Fold cross validation is like K-Fold, but it takes extra steps to ensure that for all K validation sets, an equal number of datapoints selected from each of the classes in our classifiation problem. See this image from the sklearn docs again:

![Stratified K-Fold Cross Validation Visualized](https://scikit-learn.org/stable/_images/sphx_glr_plot_cv_indices_0071.png)

Typically "stratified" tactics are applied to classification problems, but there are similar tactics for regression problems. See this article for more information about that: https://scottclowe.com/2016-03-19-stratified-regression-partitions/

## A Note:

For time series data, you always want your validation and test sets to include only instances that are *more recent* than your training data. Just like with other tasks, training data should only include information that would be available before the prediction needs to be made, and with time series data that means only including training data generated **prior** to the prediction event.