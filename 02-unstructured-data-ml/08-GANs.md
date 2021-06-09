# Generative Adversarial Networks and MNIST

Generative adversarial networks are actually a combination of two neural networks called the Generator and Discriminator:

![GAN Diagram](assets/GAN_diagram.jpg)

The input for the discriminator is always either a sample from the training data, or a sample created by the generator. Using this setup, the discriminator is typically a binary classifier: Its job is to classify samples as real examples (i.e. samples from the training set) or fake examples (i.e. examples created by the generator). The generator's job, then, is to produce data that realistically mimics samples from the training set. In order to force the generator to create many different samples we provide random noise as input to the generator. 

## Training is Tricky...

* Mode Collapse
* Keeping the generator and discriminator evenly matched
* Metrics for success are hard to define numerically

## Extensions to GAN idea:

* Conditional GAN for incorporating label information.
* Thinking about the "latent space" as an embedding:
    * The values in the latent space control the output completely. 
    * Some GAN architectures have created clever ways to isolate particular portions of the latent space with articulated meaning.