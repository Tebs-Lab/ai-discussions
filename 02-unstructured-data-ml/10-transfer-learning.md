# Transfer Learning

Transfer learning is, in essence, the application of a neural net trained on one task to a new task. Because convolutional neural nets are almost exclusively used to examine visual data, they are particularly good at transfer learning. 

A network trained to recognize dogs and cats in photographs will learn some features that are universal to processing photographs, and so it may be a good starting point for a network that detects frogs and birds in photographs. A network trained to detect cancer in radiographs will learn some things that are universal to processing radiographs, and so might be a good starting point for a network that detects foregin bodies, or bone fractures. 

In this lab we'll use transfer learning to re-train a neural network to perform a new task. 

## When does it work?

* Task similarity vs data availability chart.
* CNNs and Transformers seem to work well... RNNs and ANNs a bit less so.

## Types and considerations:

* "Feature Extraction" - no retraining whatsoever.
* Unfreeze some layers and retrain a bit
* Unfreeze all layers and retrain
* iteratively unfreeze layers and train repeatedly as we unfreeze
* Learning rate decay

## General tips

* Slower training strategies work better.
    * start with SGD and slower than default learning rates.
* It's definitely worth trying if you have similar datasets.
