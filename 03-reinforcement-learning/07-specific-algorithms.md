# Some Specific Algorithms

## Model-based vs model-free

![](https://miro.medium.com/max/700/1*BsN4a2N1EDmgG19wWDd9CQ.png)

* Some RL methods attempt to construct a model of the environment, e.g. try to explicitly define the states, transitions, and their costs/rewards. Once constructed, the RL agent searches the underlying representation and makes decisions based on that search.

* Other RL methods simply use experience to map state/action pairs to outcomes. The only internal model of the world is the "policy" which maps state/action pairs to their expected (learned) rewards.

* Model based RL is not always feasible, but it is often desirable when it can be done. 
    * This is because model free RL makes (sometimes wrong) assumptions about the world based on its (limited) experience. 

## Model Free Algorithms:

* Q-learning (which we have already explicitly discussed)
    * Explores the state space
    * Receives rewards
    * Discounted rewards flow backwards on iterative passes through the same state via the bellman update equation
    * Q learning does not explicitly learn and update a policy
        * Instead it learns the values of state/action pairs based on experience.
        * It ultimately generates a policy, but does so not by judging the "quality" of the existing policy, it does so by exploring states and taking actions (possibly from a policy, but could also be totally random and still learn)
    * This algorithm is especially bad when the number of actions is very large, since each state/action pair gets a unique estimate of its value.
        * Imagine a robot that can turn one servo an arbitrary amount, Q-learning can't capture the relationship between a 15 degree turn and 15.5 degree turn, they are treated as completely separate and distinct actions. 
    * This algorithm might also have a hard time converging, which isn't always the worst thing, but it can be frustrating to not know when your model is "done" and therefore be unsure if it can get any better or if training is now just a timesuck.

* Policy Gradients, PPO (PPO is currently considered the best default algorithm)
    * Policy based method, which never attempts to estimate the value of individual states.
    * Instead an individual policy is maintained and updated.
    * Good at handling stochastic environments, because it can have a policy that outputs a probability distribution. Value iteration methods learn this in an implied way, but also must be forced to explore with "tricks" and "hacks" whereas policy gradients have this baked into their bones.
        * Also solves the "epsilon greedy" problem.
    * Downside is that it often finds a "local max" rather than a global one, as with all gradient based methods.

* Asynchronous Advantage Actor Critic
    * Multiple separate agents act individually, and report their experience to a "master" agent.
        * These agents train in a unique copy of the environment.
        * The idea is to diversify the experience gained by each.
        * Allows parallizable experience gathering, which improves training speed.
    * Actor-Critic:
        * The value of a state, and the policy are estimated separately by separate neural networks
            * Combines value-based methods (Q-learning) and policy based (policy gradients)
            * The "actor" is the policy network that maps states to actions
            * The "critic" is the value network that maps states to values
            * When the actor chooses an action that leads to a low value state, it is "criticized" which causes the policy to be updated.
    * Advantage:
        * Instead of estimating just the rewards for state/action pairs and updating them according to the bellman equations, we also quantify how wrong our predictions were and use this to:
            * Make bigger updates when our expectations were off by a lot.
            * Make smaller updates when our expectations were nearly correct.

* There are more, and lots of optimizations for these major models, but these are some of the most important ideas.

## Model Based Methods

There are essentially two options here:

* Learn the model through exploration.
    * There are a variety of clever algorithms attempting to do this...
    * But they ALL try to build an MDP under the hood, then use value iteration, supervised learning, or other more traditional methods to build the policy from the learned understanding of the world.
    * These methods bounce back and forth between updating the policy (finding the best actions to take) and updating the model (exploring the world).
    * This introduces a second source of error (learning the wrong model and learning the wrong policy) but is often more efficient esp. when the policy 
* provide the model.
    * This is possible in, e.g. games where all the rules are explicitly known and well codified. Esp. turn based games like Chess and Go.
    * This is NOT possible in situations like self driving, where the model of the world would be impossibly complex.
    * AlphaGo learns this way! The model of the world is completely known (e.g. I know exactly what all the states and state transitions are)

* In model based methods you still iteratively learn the value of states or state/action pairs, but because you "know" how the world works it's easier and more efficient to percolate the rewards backwards from their states. 

* More about model based: http://bair.berkeley.edu/blog/2019/12/12/mbpo/
* More about RL algos: https://spinningup.openai.com/en/latest/spinningup/rl_intro2.html 
* More still RL algos: https://smartlabai.medium.com/reinforcement-learning-algorithms-an-intuitive-overview-904e2dff5bbc
