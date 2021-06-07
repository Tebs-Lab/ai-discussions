# Challenges With Reinforcement Learning

* Exploration vs Exploitation
    * "Curiosity" rewards
    * Random exploration and annealed exploration
* Very delayed rewards
    * Intermediate rewards, but beware: unintended consequences.
* Massive and Infinite state-spaces
    * Discretizing the search space
    * “Approximate” RL (essentially feature extraction on the state space)
    * “Deep” RL learning (using neural networks to do feature extraction)
* Offline training / obtaining good training data
    * Single player games don’t have this problem, which is one reason why RL is so popular in that domain!
    * “Self play” with “evolutionary” models can help.
    * “Learn by watching” agents get rewards for making the same decision as experts in recorded games/tasks/logs.
    * Get’s even trickier for complex tasks, esp. Ones with multiple “correct  decisions” at any given “state”: e.g. how do I train self driving cars?
* Partially observable phenomena
    * asymmetric information games (Starcraft/League), 
    * Self Driving (physical blind spots but also the “problem of other minds”)
* Decision delay:
    * Slow sensors, network latency, etc.
    * Complex heuristics / feature extraction make things slow.
    * The world may have changed by the time I can take my action!
* Safety constraints
    * Unobserved states -> unreliable/unpredictable behavior
    * Use Constrained and/or Budgeted MDPs
        * In some set of states, fix the policy manually rather than using the learned policy
