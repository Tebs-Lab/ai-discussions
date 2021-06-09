# Constraint Satisfaction

## CSP Very Basics

* Many problems that can be solved with AI can be classified as "Constraint Satisfaction Problems"
* Such problems impose a set of variables and a set of constraints.
* A solution to the problem is an assignment of values to the variables such that no constraints are violated.
* Constraints might be "unary"
    * E.g. Some specific variable cannot have some specific value.
    * E.g. Some specific variable cannot have a value greater than 10.
* Constraints might be "binary"
    * E.g. Two variables can't share the same value
    * E.g. Two variables MUST share the same value
* Constraints might be more complex
    * E.g. variables A, B, and C must add up to exactly the value 5.7
* Constraints might actually be "preferences"
    * Typically represented by a cost function to be maximized, where hard constraints represent an infinite cost.

## Examples

* Map Coloring
    * Each country must be a color.
    * No two neighboring countries can be the same color. 
    * Solution in a nutshell: model the map as a graph to get the constraints, then use a CSP algorithm.
        * Nodes are countries, which are also the variables from the CSP
        * Edges connect neighboring countries.
        * Extract the constraints from the edges: No nodes that are directly connected can be the same color.

* Making/Solving Crosswords
    * More than one way to do this, but here is one:
        * Variables are each box, which can be assigned any one letter value (unary constraint, each box is a single letter).
        * Variables are ALSO word slots, which must all contain a word from a provided dictionary (another unary constraint, each world slot must be a word!).
        * Multivariable Constraints are such that the individual letter boxes must be the proper letters from the selected word, and that crossing words share the letters at the appropriate cells.

* Scheduling Classes
    * You have a set of rooms, and a set of classes each with a length of time that they'll occupy a room.
    * To make things easy, assume every class is exactly an hour long, and classes can be scheduled in a room perfectly back to back (the hard version can also be solved, but this is easier to think about to start.) 
    * Variables are the individual hour long blocks for each room (!)
        * Assignments of a variable are a particular class to a particular time slot. 
    * Classes cannot start before 7:00am or after 5:00pm (unary constraint).
    * Classes cannot overlap in a particular room-time-slot (binary constraint)
    * You can imagine constraints to this becoming more complex (some classes are M/W/F, some T/Th... classes need 15 minute breaks, and can be arbitrary lengths of time...)


## Backtracking Search

* The naivest approach is recursive backtracking.
* In a nutshell: 
    * assign a value to a variable 
    * check if that assignment violated any constraints.
        * If so, undo the assignment and try a new value for that variable.
            * If NO valid assignments exist for this variable, undo the previous variable assignment and try again.
            * (you may continue "backtracking" in this way to undo many steps)
        * If not, make the assignment, and repeat the process with another variable assignment.

* Benefits: really easy to code.
* Drawbacks: without some cleverness this can be really slow, and can re-encounter states that it has already processed.
* Fix it up:
    * Use dynamic programming / memoization to ignore duplicate states that can be reached in different orders of assignments.
    * Use a heuristic. 
        * For example, a common heuristic is to always attempt to assign the variable which has the most constraints on the remaining (unassigned) variables.
            * This is a "fail fast" heuristic which will quickly exhaust impossible scenarios.
            * Good if lots of states can be reached by a different order of assignment as it will quickly prune the search space.
        * Another common heuristic is to choose the variable that rules out the fewest number of values for the remaining variables.
            * This is a "fail slow" heuristic, which will more likely find a solution along one of the early search paths
            * This is good if you're confident that there is a solution, and especially good if you can augment the heuristic with a clever way to pick which assignments are likely to lead to solutions.
            * Also good if it takes a long time to rule out any given assignment as "impossible"

## Forward Checking and Constraint Propagation

* Forward checking keeps track of ALL the remaining valid choices for each variable separately.
    * Anytime you make a choice, check all variables against their constraints and remove any choices that would violate those constraints given the choice you just made. 
    * If any variable has exactly one value remaining in its list, assign that one next.
    * If any variable has zero choices remaining in its list, backtrack.

* Constraint propagation is forward checking on steroids.
    * Every time an assignment is made, do the forward checking.
    * Furthermore, for each variable that was affected by the latest assignment, re-check that IT can still be satisfied.
        * If any variable loses a value, that variable is rechecked immediately.
        * This is essentially a way to discover that you've made an impossible assignment more quickly than.

## Note that:

* There are multiple well known ways to solve such problems. 
* But most CSPs are also NP-complete which can be a problem for "naive" methods
    * As with graph search, most real world applications of CSP solving algorithms rely on some kind of heuristic or a clever manipulation of the problem space to choose which constraint's to explore first. 
    * Very often these heuristics or clever choices can make solving the problem possible in a reasonable amount of time, or enable an approximate solution quickly.

* There are some graph theoretic properties that can bound problem complexity. 
    * For example if your "constraint graph" has no loops and if n is the number of variables, d is the size of the domain-per-variable then the CSP can be solved in O(n*d^2) whereas the "general" CSP problem is essentially intractable at O(d^n)
    * There are many such theorems, consider [This AI Textbook](http://aima.cs.berkeley.edu/) for a more complete treatment.

## Lastly: Other AI!

* Combining other forms of AI with CSP solving algorithms can be hugely impactful. Consider this hybrid system which is the state of the art for crossword puzzle solving:

1. Use a transformer or RNN to read the clues and classify the clue as one of N words from the dictionary.
    * Do this for all clues, then select the clue that has the highest confidence in its word choice.
2. Perform a round of constraint satisfaction.
    * Do forward checking to see if you've made any word-slot impossible to fill. Backtrack if so.

* In this case we're essentially using a neural network as a heuristic to make good word choices. 
* There is a ton of historical crossword data to use to train such a neural network. 
* The neural network will make errors, they are good approximations but never perfect. 
* The CSP algorithm on the other hand will enforce perfection.
* At the start, the CSP algorithm alone just flounders in the dark: every 4 letter slot might map to EVERY 4 letter word.
    * So we need a way to make smart choices!
* Near the end, the CSP algorithm will CRUISE because most words have been eliminated for each word slot. Eventually it will make sense to stop using the neural network and just fill out sections with their only possible valid words/letters.