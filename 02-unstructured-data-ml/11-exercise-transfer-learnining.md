# Exercise: Transfer Learning

In this exercise you'll be broken into small groups to discuss the usefulness of transfer learning in a few different contexts.

## The Questions

Answer the following questions for each of the circumstances described below:

1. How similar are the two tasks, as described?
    * Consider the data sets.
    * Consider the outputs.
2. How well do you expect transfer learning to work in this circumstance?
3. Which of these strategies would you use during the retraining process assuming you have a small amount of data for the new task?
    * Full Retraining (no layers frozen during retraining)
    * Fixed feature extraction.
    * Fine Tuning (some layers frozen during retraining)
    * Discriminative fine tuning (iteratively unfreezing layers)
4. Does your answer to 3 change if you have much more data for the new task?

## The Circumstances

### 1. ImageNet to Cancer Screening

You have a network that has been trained to classify images using the ImageNet dataset, which is a 1000 class dataset of photos from the real world. These images and classes are widely varied from animals to bikes to plants. You want to build a system that looks at radiographic images and detects the presence of cancer.

### 2. ImageNet Classification to Object Localization

You have a network that has been trained to classify images using the ImageNet dataset, which is a 1000 class dataset of photos from the real world. You want to build a system that can isolate the location within the image that contains the item of interest, which will always be one of the same 1000 classes from ImageNet.

### 3. Fractals to Image Net

Read the abstract of this paper: https://arxiv.org/pdf/2101.08515.pdf

You have a network that has been trained on this synthetic fractal dataset, and you want to use it to learn to classify images of the natural world as represented by the ImageNet benchmark.