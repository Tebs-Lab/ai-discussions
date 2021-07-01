# Data Preprocessing

Managing the data before we send it to out algorithms is very important!

## Cleaning vs Preprocessing

* Cleaning is all about making the data error free.
    * Generally the exact same cleaning process will always be performed for a particular kind of data.
    * Meaning, for my house price prediction models all the house data will be cleaned the same way.
    * Handle Missing values
    * Check for Wrong values
    * Handle Outliers

* Preprocessing is about preparing the data for our ML algorithms.
    * For example a one hot encoding
    * Different algorithms can benefit from different preprocessing tactics.

## Feature Extraction

* Any preprocessing tactic designed to take raw data and process it to a more informative format is called feature extraction.

## Feature Engineering

* Combining features of the data into new "derived" features is called feature engineering.

## Normalization / Scaling

* Normalization and scaling change the data in a way that alters it's format, but doesn't actually change the meaning of the data.
* For example, scaling in the context of housing prices:
    * Square feet and number of rooms are both informative about the price of a house.
    * But Sq Ft will be in the ~1,000-10,000 range and rooms will be in the 5-20 range.
        * For some algorithms, the larger values will dominate the underlying mathematics of the model, rendering the number of rooms metric useless.
    * Scaling means we coerce both the domains into 0-1 where 0 means "the smallest value from that column" and 1 means "the largest value from the column"
        * This computation is simple and reversable:
            * subtract the smallest value from all the samples, then divide by (largest_value - smallest_value)

## Note That

* There are MANY preprocessing techniques and some are actually super complex.
* Many of these make the underlying model less interpretable, which can be a downside, while simultaneously improving the performance of the model. That can be a tricky tradeoff to navigate in some circumstances.