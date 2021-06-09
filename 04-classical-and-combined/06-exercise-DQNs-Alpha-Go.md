# Exercise: Super Modern Game Playing

AlphaGo is a state of the art game playing algorithm designed specifically to play the game Go, although many extensions of the design and architecture of AlphaGo have been built to play other games as well. 

## Part 1: Individual Research

Individually attempt to answer these three questions by doing some research.

* How does AlphaGo use Reinforcement Learning?
* How does AlphaGo use Adversarial Search?
* How does AlphaGo use Neural Networks?

## Part 2: Put it Together

In small groups...

1. Spend a few minutes discussing your answers to Part 1.
2. Attempt to describe the process that AlphaGo goes through when it makes a move.
    * For now, ignore the training process and just focus on what "making a move" looks like for the fully trained system.
    * Describe the role of RL, Tree Search, and NNs in this process.
    * The answer to this question might be pretty long... it's not a simple process!
    * What heuristics might be involved?
    * When is the tree search employed?
        * How might cut off decisions be made?
        * What is the evaluation function being used?
    * How many neural networks are involved?
    * Is a "policy" from RL being employed?
        * If so, how?

## Part 3: Taking a Step Back

As a group, discuss and research the following questions (you may wish to make some research assignments and then circle back).

1. AlphaGo and AlphaGo Zero employed several training tactics. Describe how these systems did the following things:
    * Trained from games played by human experts.
    * Trained with self play.
        * How was variation among the "self play" versions of the system achieved?
2. AlphaGo used two neural networks, a "policy" and a "value" network. AlphaGo Zero only used one. 
    * Describe the difference between these two setups.
    * What are the "features" and "labels" for each of these networks?
    * Can you find any information about the actual structure of these neural networks?
3. Training this system was expensive, but became cheaper over time.
    * Can you quantify how much training was done on the AlphaGo system that beat Lee Sedol?
    * Can you describe why/how AlphaGo Zero was able to train for much less time and yet outperform AlphaGo?
