# Hyperparameter Search

Whenever we build an ML model, we have a lot of choices to make about hyperparameters. Sometimes we can rely on our intuition to guide us towards good choices, but one of the main benefits of ML models is that they find surprising results by "thinking" quite differently from the way most people think. Being primarily a statistical discipline, machine learning experts will often use validation data, a technique called "cross validation," and programatic methods to explore the possible combinations of hyperparameters and find ones that produce good models empirically. 

Generally, we use this to automatically find the best hyperparameters according to our cross-validation scores along whatever metrics we specify (e.g. accuracy or r^2). 

The two most popular tactics for hyperparemeter search are:

#### Grid Search

We supply a set of values for each hyperparameter that we want to search acrosss. SK-learn computes all the possible combinations of our selections and performs cross-validation on for each combination. 

#### Randomized Search

We supply a range of values for the hyperparameters we are interested in. SK-learn randomly selects values for each hyperparameter within our ranges and performs cross-validation. We specify how many times to perform this process.