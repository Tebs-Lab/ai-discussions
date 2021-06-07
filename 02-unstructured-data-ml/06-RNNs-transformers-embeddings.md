# Enconding Natural Data

One of the primary challeges in natural language processing is properly encoding the text so that mathematical models such as neural networks can extract meaning from the text, and process it into some kind of result. The field has evolved quite a lot over time, and we're going to briefly present a few of the once-common strategies for language encoding then spend some time talking about the current favorite method: embeddings.

## Rules Based Systems

At first there were rules based systems. Like many other systems at the time, these were "expert systems" designed with extensive help from linguists and grammatician. These systems would look at a sentnce and try to identify critical aspects of a sentence (the subject, object, key verb...), label the words into types (adjective, noun, verb adverb), and map their function (which adjectives describe which nouns?).

These expert systems could produce some data structure representing the sentence or document, and then these structures could be used for some custom built purpose (grammar check, chat bot...)

Unlike ML systems, these systems didn't have any real purpose for statistical based learning, and as a result the data structures didn't need to be strictly numerically based, nor did they have to explicitly encode individual words or longer sentences into pure numeric formats. 

## Bag of Words

Once statistical learning methods began advancing, NLP researchers needed pure numeric encodings that could meaningfully represent, words, sentences, or other strings of text. Some simple strategies like the classic one-hot-encoding were fleetingly popular — but the need for a vector the size of the entire vocabulary just to represent a single word was prohibitively costly for all but the simplest use cases.

The "Bag of Words" encoding came next. Instead of representing single words at a time, this strategy reduces an entire string of text into a vector. Again the vector is the lenght of the vocabulary, but instead of one-hot the individual values are the number of times that word appears in a the text.

For example, say our vocabulary is only 5 words:

Hello, live, work, to, friend

Each of these words is represented by a position in a vector, and we loop through the text to create the vector for our text. 

The sentence, "Hello friend" becomes the vector `[1, 0, 0, 0, 1]`  

"Live to work" and "work to live" both become the vector `[0, 1, 1, 1, 0]`

For some simple tasks such an encoding can work reasonably well especially if the input texts are always short. For example, mapping Tweets to a binary positive/negative sentiment system. But such a simple system clearly discards much of the semantic meaning of the sentence by completely ignoring the order of the words. It also struggles with words like "live" that have multiple possible meanings ("The new feature is going live tomorrow." vs "She is going to live!")

Such an encoding can indeed be used with a standard ANN. That said, none of the state of the art research is proceeding down this path.


## TF-IDF

TF-IDF, or Term Frequencey Inverse Document Frequency is a way to turn an individual word into a numeric value rather than process a series of words the way Bag of Words would. The TF-IDF value is a representation of how common a word is within a particular document as well as how common the word is accross all documents in an entire corpus or dataset. We won't be using it, but you can view the [mathematical details on Wikipedia](https://en.wikipedia.org/wiki/Tf%E2%80%93idf) if you're curious

While this is useful in some information retrieval contexts for many natural language tasks such as machine translation and sentiment analysis, information about a words commonality isn't especially helpful. Researchers needed a way to create a numeric representation of individual words that could somehow capture the semantic meaning of those words...

## Word Embeddings

In 2013, a team of researchers at Google published two papers describing Word2Vec, a neural network that transformed individual words into vectors that could represent the word's semantic meaning. Word2Vec formed a strong foundation for reseach, and ultimately led to the creation of a now-standard tool: Word Embedding layers. 

Word embedding layers provide a generic interface for the first layer of any neural network that wants to process one word at a time as input. Their function is simple: Embedding layers act as a lookup table mapping a word from our vocabulary into a dense vector of a chosen length representing that word.

The values associated with each position in the word-vector are learned during back-propagation just as the weights in a Dense layer would be, but don't require an entire matrix multiply as each word maps to a single vector of the matrix representing the entire vocabulary. This difference saves computational time, but learns through backpropagation very similarly to a Dense layer. 

Sometimes we may use a pre-trained network (such as Word2Vec) to create the word embeddings. Although it is now quite common to train an embedding layer as part of the network, which allows the word embeddings to learn patterns that are specific to the task at hand. 

Regardless, the result is a lookup that maps words to vectors and (if it works as expected) words that are closely related in the dataset result in vectors that are near each other in vector space. When it REALLY works, these embedding vectors can be thought of as a rich set of features extracted from the word.

Analysis of the embeddings themselves can be done. For example computing the cosine similarity between two words in the resulting vector space frequently reveals that semantically related words like cat and kitty are close to each other in the resulting vector space, as explained here [https://medium.com/@hari4om/word-embedding-d816f643140](https://medium.com/@hari4om/word-embedding-d816f643140)

![](https://miro.medium.com/max/700/1*sAJdxEsDjsPMioHyzlN3_A.png)

> image from linked reading

# Intro to Recurrent Neural Networks

Recurrent Neural Networks (RNN) are another specialization within the neural network family designed to work specifically with sequence data. The most common types of data to use with RNN's are time series data and textual data (natural language, programming languages, log files, and so on).

Sequence data, and especially variable length sequence data, presents significant challenges for other models in the neural network family (and many other kinds of models) for a few reasons including:

### Most models, ANN's included, require a fixed input size.

This is fine for some problems, looking at a fixed-size time window for weather prediction is perfectly reasonable. But it's a non-starter for problems like machine translation where arbitrary text documents (from single sentences to complete books) must be handled for the system to be worth anything. 

Earlier models working with sequence data often involved a preprocessing step that smashes variable length data into a fixed length feature vector. One of the simplest examples of this tactic is called the "Bag of Words" where a textual input is reduced to the number of times any given word appears in that data-point. The result of a "Bag of Words" transformation is a vector where each position represents one of the words in the entire corpus vocabulary, the integer value in that position represents how many times that word occurs in the data-point.  

This enconding for text is problimatic and limiting, as we discussed previously. For example, "live to work" and "work to live"  will result in the same "bag of words" encoding although all English speakers recognize the sentences are opposites of each other. 

One dimenstional CNN's can be used to solve this problem to some extent, although they are somewhat limited by the kernel size with respect to how far backwards in the sequence they can look at once. 

### Most models, including ANN's requre a fixed output size.

Similar to the above many sequence tasks (such as machine translation) require arbitrary length output, which is a non-starter for both ANNs and CNNs.

## RNNs Solve These Problems By Maintaining Internal State

The core idea of an RNN makes a lot of people raise their eyebrows at first, but it is actually quite simple. In addition to the weights and biases used in a traditional ANN, the RNN introduces a "state vector" which is internal to the recurrent nodes. This is sometimes drawn in a confusing way such as this illustration from [one of the readings](https://towardsdatascience.com/illustrated-guide-to-recurrent-neural-networks-79e5eb8049c9):

![](https://miro.medium.com/max/106/1*h_cfQuMl30szUkDAi7wrCA.png)

The idea is that this node is passing some information *to itself* across a series of sequental calls, one for each data point in the sequence (this could be time steps in a time series, words in a sentence, or characters in a string of text). 

This is true, but I think it's easier to imagine the state vector as a piece of memory internal to the node which is  updated (even during inference) for each piece of data in the input sequence:


![](assets/single-rnn-node.png)

X0 is the first input of the sequence (e.g. first word, first time step, or first character), y0 is the cell's output, and the state vector, like the weights matrix, is internal to the cell. However, unlike the weights, the state vector changes during forward passes instead of just during back-propagation. So, when we move on to the second piece of data in the sequence we have something like this:

![](assets/two-rnn-node.png)

The forward pass on datapoint X0 modified the internal state vector, so this is often drawn with an arrow connecting the whole cell to itself in a subsequent timestep, such as this drawing, from [another one of the readings](https://karpathy.github.io/2015/05/21/rnn-effectiveness/):

![](https://karpathy.github.io/assets/rnn/diags.jpeg)

The hidden state vector contains all the information that the network has accumulated about the sequence so far. Similar to a markov chain, RNN's implicitly assume that this vector is rich enough to capture all the relevant information about what has been processed earlier in the sequence (for examples, which words have already been seen).

The forward pass for a vanilla RNN works like this (assuming an activation function of tanh):

```
# Hidden state is updated:
#   W_hh (the weights for the hidden state vector)
#   W_xh (the weights for x)
#   self.h (the actual hidden state)
self.h = np.tanh(np.dot(self.W_hh, self.h) + np.dot(self.W_xh, x))

# Compute the output
#   self.W_xy (the weights for the output)
y = np.dot(self.W_hy, self.h)

return y
```

The output y can be passed to other neural network layers as usual, and the hidden state is carried over across the current sequence (but is reinitialized for each new sequence, usually to zero!) 

**Note** that there are 3 sets of weights:

* One that learns to transform the hidden state each timestep,
* One that learns to transform to the X input data at each timestep,
* One that learns to create the output based on the hidden state at each timestep.

## Backpropagation Over Time

To understand how backpropagation works with these models, it's best to think about "unrolling" the model as we saw in the diagram above:


![](https://karpathy.github.io/assets/rnn/diags.jpeg)

For each output, we compute a loss and the gradients flow backwards through the entire "unrolled" network. This has a few implications:

* The shared weight matricies are updated multiple times per backprop step. 
    * This exacerbates the exploding and vanishing gradient problems.
* It makes the model memory intensive during training, since the hidden states at each timestep have to be retained during training (but not during inference).
* Training is typically slow, since both during the forward passes and backpropagation there are dependencies over time — e.g. you must finish calculating the values for x0 before computing the values for x1, meaning we cannot leverage parallelism and GPU hardware nearly as well as we could with CNNs and ANNs.

## Transformers 

TODO: This section... https://jalammar.github.io/illustrated-transformer/