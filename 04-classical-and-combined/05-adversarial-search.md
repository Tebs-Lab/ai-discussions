# Tree Search for Adversarial Problems

## Adversarial Tree Search

* Adversarial search is a strategy primarily used for playing games.
    * Although some other problems can be modeled this way, games are by far the most common use case.

* In the most basic form, we assume a game like Chess or Go:
    * Players take turns.
    * The complete state of the game is observable by both players.
    * The game is essentially zero sum: if one player has an advantage the other has a disadvantage.

* The basic idea:
    * Simulate all possible (or all relevant) moves that both the agent and it's adversary can make.
        * This simulation results in a tree.
    * Identify paths through the tree that result in a victory.
    * Only make moves that take you along one such path.

* **Do an example on the whiteboard for tic tac toe**

* This same strategy can be employed on basically every two player, turn-based game. 

## Two Most Common Varieties:

### Minimax

* Simulate the game to the terminal states.
* Percolate the utility values up the tree by assuming:
    * The agent always chooses the best action available (highest utility action), this is the MAX
    * The adversary always chooses its best action, the one that minimizes our agents utility. this is the MIN

* This is especially appropriate for playing games with no chance or randomness.
    * Essentially, we assume our opponent will play perfectly, and only make moves that would beat a "perfect" opponent. 
    * (at least, that's the goal!)

### Expectimax

* The same as minimax EXCEPT the opponent's rows are averaged instead of minimized.
* This is especially good in games where the opponent's actions are partially governed by chance, such as the roll of a die.

## Challenges

### Big Search Spaces

* Tic tac toe is solved, the number of valid states is roughly 9! (nine factorial)
    * Therefore the whole tree can be simulated. For other games this is not so...
    * Chess and Go for example:
        * The state space is too large to be reasonably explored.
        * The number of valid chess positions is estimated to be in the neighborhood of 10^50 [source](https://www.nwchess.com/articles/misc/Chess_Board_Positions_article.pdf) 
        * The number of valid Go positions is ~ 2^170 (!!!!!!) [source](https://www.i-programmer.info/news/112-theory/9384-number-of-legal-go-positions-finally-worked-out.html)
        * For reference, the number of atoms in the observable universe is estimated at ~10^80 [source](https://www.universetoday.com/36302/atoms-in-the-universe/)

* So, the search space has to be dramatically pruned. We can...
    * Use Heuristics to prioritize and cutoff search: 
        * Lots of Chess and Go positions are "bad" so we shouldn't explore their child states, 
        * similarly we should prioritize exploring "good" looking states.
    * Pruning: If we can put lower and upper bounds on our expected value, we can avoid exploring states that aren't going to be any better for us. 
        * Alpha/Beta pruning.
    * Cutting off search after some fixed depth or other heuristic...
        * But this creates the below problem:

### The Problem of Intermediate States

* In most games you don't know who has won until the game is over (or at least nearly over...)
* But because of the large search spaces issue, it's not reasonable to explore every path to the endgame. (this is generally true even with pruning and heuristics.)
* So, the intermediate states must be valued directly without relying on the search tree to actually reach a terminal state
* Because of this, we generally use an "evaluation function" which looks at the state of the game and assigns it a numerical score where high scores indicate a higher likelihood of winning the game somewhere down the line.
    * Building a perfect evaluation function is basically impossible for complex games.
    * But so is searching the whole space, so we have to do something!

* These evaluation functions can be anything
    * Including other ML models!
    * Deep Blue was Minimax with expertly crafted evaluation functions.
        * Even different eval functions for different opponents!


