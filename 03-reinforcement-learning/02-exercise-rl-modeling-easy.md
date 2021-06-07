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

## The Scenarios

### Cartpole

The Cartpole problem, also called the inverted pendulum problem, is simple:

* You have a stick attached to a cart such that the stick can freely swing along a single plane.
* The cart is also fixed in a plane, and can only move left or right.
* The goal is to keep the stick balanced in the upright position.

I think it's easier to see this problem than describe it in writing, so here are two videos of the cartpole problem in action:

* Simulated: https://www.youtube.com/watch?v=oXfT1hXvDbE
* Real world:https://www.youtube.com/watch?v=5Q14EjnOJZc

And, for fun, here is a simple game where you can play a few rounds of CartPole yourself:

* https://jeffjar.me/cartpole.html

### Frozen Lake

Read the description of this toy problem here: https://gym.openai.com/envs/FrozenLake-v0/
