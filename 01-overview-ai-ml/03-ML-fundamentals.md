# Machine Learning Fundamentals

We've decided to focus on ML first because it's so damn popular.

## What is ML?

* ML is a broad subcategory of AI.
* In non-ML systems an AI engineer explicitly codes the rules for how an input is turned into an output, regardless of what that is.
    * This might involve neat data structures (e.g. graphs and graph search for Google Maps)

* In an ML system, instead the engineers select one of many known templates for a "model."
    * Then, through a "training" process which always involves showing the template a lot of data, we get a "trained model" and the trained model is the thing that turns inputs into outputs. 
    * Each type of model has it's own unique training process.

* A motivating example:
    * If I asked you to write some software that could look at a picture and tell me if it's of a cat or not, what would you do?
        * Maybe do edge detection, then try to define some geometric rules for what makes a photo "cat-like"?
        * Maybe do some color analysis, pinks and greens are not cat-like but browns, blacks, whites, and oranges are more cat-like.
        * What about different poses?
        * What about zoomed out, where the scenery takes up a larger share of the pixels (cats exist on grass, but that's mostly green and therefore NOT cat-like...)
    * Instead, in the ML world we choose a model type that is good at "extracting features" from images, and just show it millions of pictures of cats and non-cats.
    * This is also beneficial because I can use that same template and send it a wide variety of data, your handcrafted algorithm can only do cats and updating it to also do airplanes might be really hard. 
        * With ML, it's only as hard as collecting more data. (which can honestly be hard, but that's another story.)

## Three Types of ML

* Supervised Learning
    * By far the most popular.
    * Involves learning from "labeled" data, meaning the answer to our question is known (we know which pictures are cats and which are not).
    * Widely used in a huge number of domains.

* Unsupervised Learning
    * Less popular in general.
    * Involves unlabeled data.
    * Often used as a way to "bootstrap" labeled data for supervised learning.
    * Clustering is the most common example.
    * We do not talk much about unsupervised learning in this class.

* Reinforcement Learning
    * Used in situations where an agent needs to keep making decisions.
    * Most popular in game playing and robotics, but has been used in some other domains.
    * Involves an "agent" and an "environment" where the agent "reads" the environment, takes an "action" and then "reads" the environment again to make it's next decision.

## Structured vs Unstructured Data

* Structured data, also called "tabular" data is anything you could readily put in a spreadsheet or a relational database table.
    * A row is a single data point
    * Each column is one piece of information relevant to that data point.

* Unstructured data is anything else, but some popular kinds of unstructured data that had ML applied to them successfully include:
    * Photos
    * Videos
    * Audio
    * Text / natural language

* The big-picture take away about these kinds of data is:
    * If you have structured data there are a LOT of ML algorithms to choose from for processing that data.
    * If you have unstructured data you almost certainly want to use some form of Neural Network.

## Continuous/Numerical Data vs Categorical Data

* Numerical data is exactly what it sounds like.
* Categorical data is something like a zip code or sex:
    * There are a finite number of choices.
    * The choices aren't "ordered" e.g. the zip code 85171 is not "one less than" 85170, they are just different
    * Usually we use a "one hot" encoding for categorical data
* Some algorithms work perfectly well with categorical data, and some really don't.
* BUT, all these algorithms are fundamentally mathematical/statistical, which means finding appropriate mathematical encodings for data that may not be itself fundamentally mathematical (e.g. human language) is a big area of research in ML.

# Regression vs Classification

* If you're predicting a numerical value, you call it "regression"
* If you're predicting a categorical value, you call it "classification"
* Even more complex tasks can generally be broken down into subtasks of these types:
    * Object localization is regression for the definition of the bounding box, and classification for the thing inside the box.

## Test/Train Data & Evaluating Performance

* Training data is used to form the model's understanding of the problem at hand. 
* Test data is left out at training time, and used to determine if the model learned to "generalize" (that is, perform well on held out data)
    * A model that works well on the training data, but poorly on the test data is said to be "overfit" which is a lot like memorizing the answers to a math test.
* A wide variety of metrics can be used to evaluate performance.
    * These metrics will be computed for both training and test datasets
        * As well as "validation" sets, which we'll discuss later.
        * We'll also discuss a handful of the most common metrics later in this class.

## Sources of Bias & Error

* The biggest source of bias is the data itself.
    * The three examples in the next exercise will elucidate this point in great detail!
    * But in short, ML models only learn whatever patterns are in the data itself. If that data was collected by humans, it likely has human bias embedded inside of it. ML models will learn that bias. 

* Bias can also be introduced by evaluators who might:
    * Not carefully look at the results across different demographic cross tabs
    * Explicitly have their own motives (e.g. Chinese government training an algorithm to target Uighurs)
    * ...

* Errors can also be created by using an algorithm that can't adequately capture the relationship between the input data and the output data.
    * Many of these algorithms have some very explicit modeling expectations...
        * Linear regression expects a linear relationship.
        * K-Nearest Neighbors expects a geometric distance-based relationship.
        * ...

* All of these can, of course, happen at once.