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

### Chess

Chess is a classic board game. If you need a quick refresher on how to play chess, consider this source: https://www.instructables.com/Playing-Chess/

### Robotic Control: Item Picking

There is great interest in designing robotic systems that can automatically pick items from a conveyor belt and especially in being able to do so with specific items that might be mixed with other items. This can include spotting faulty parts or products from a conveyor belt, or simply grabbing items that might be produced at a variable rate from a conveyor belt. 

Here's a video of a robot performing this task: https://www.youtube.com/watch?v=cuCPAi576S0

If you search for "item picking" you'll find many more such videos, mostly advertisements for robots that can perform this task.

Assume you're designing an item picking robot system with the following constraints:

1. Your robotic arm has "six degrees of freedom" meaning it can be adjusted along:
    * Position on the X axis (surge)
    * Position on the Y axis (sway)
    * Position on the Z axis (heave)
    * Tilt on the X axis (roll)
    * Tilt on the Y axis (pitch)
    * Tilt on the Z axis (yaw)
    * Read more: https://en.wikipedia.org/wiki/Six_degrees_of_freedom
2. Assume you can adjust these 6 values directly and that you don't need to know anything more about the underlying robot in order to do so.
3. Your robot can also "grip" and "drop" which are considered single actions and they always work.
4. Your robot needs to move "faulty" parts from a conveyor belt with a constant speed to a statically located trash bin.
5. Your system can make the following readings:
    * Get the x/y location of all faulty parts relative to a fixed point of reference.
    * The the x/y/z location of the robot arms current position.