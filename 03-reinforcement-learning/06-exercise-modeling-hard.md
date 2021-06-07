# Exercise: Modeling Problems as Reinforcement Learning

In this exercise you'll be broken into small groups and asked to take a problem and define it in terms of reinforcement learning.

## The Questions

For each of the below scenarios, answer the following questions:

1. Define the state for this problem, and be as specific as possible.
    * What values or measurements can be extracted from the environment?
    * How should they be represented?
    * Should you perform any "feature engineering" from the raw data?
    * Should you discretize the measurements somehow?
    * Are there some terminal states?
2. Roughly how large is the state space that you have defined? Is it...
    * 10 states
    * 100 states
    * 1000 states
    * 10,000 states
    * 100,000 states
    * 1,000,000 states
    * More than 1,000,000 but a finite number of states.
    * Literally an infinite number of states.
3. What actions are available to your agent?
4. Define one or more possible reward schemes.
    * What states should provide positive rewards?
    * What states should provide negative rewards?
    * Carefully consider the impact (and possible unintended consequences) of this reward scheme.
5. How might you go about training this model?
    * Can you accurately simulate the environment?
    * Does the agent need an adversary, or can it train alone?
    * Can training data be obtained in a way other than simulating the environment?

## The Scenarios:

### Self Driving Cars

You know what they are!

### Every Atari Game

Read this short write up [https://www.technologyreview.com/2020/04/01/974997/deepminds-ai-57-atari-games-but-its-still-not-versatile-enough/](https://www.technologyreview.com/2020/04/01/974997/deepminds-ai-57-atari-games-but-its-still-not-versatile-enough/) and potentailly scan this more detailed blog post [https://deepmind.com/blog/article/Agent57-Outperforming-the-human-Atari-benchmark](https://deepmind.com/blog/article/Agent57-Outperforming-the-human-Atari-benchmark) about how DeepMind built a single system that is capable of beating 57 different games. 

Consider the unique challenges associated with building this more general agent, but assume the following:

* The only information available to the agent are the pixels and a number representing the score. Nothing else can be extracted from the environment.
* The agent's actions are anything the controller allows
    * Which includes multiple simultaneous button presses...