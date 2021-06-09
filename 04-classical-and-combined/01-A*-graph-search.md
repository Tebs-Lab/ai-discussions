# A* and Heuristic Graph Search

* Graph review:
    * Nodes
    * Edges
        * Weighted?
        * Directional?

* Nodes and edges can both have arbitrary numbers of properties, 
    * you might have many "types" of nodes in any one graph depending on what it is modeling.

* Lots of things can be modeled by graphs, and some graph algorithms can be used to intelligently extract information from those graphs...

* Roads are graphs where:
    * Intersections/interchanges are nodes (anywhere that you can switch which road you're on is a node, really)
    * Roads are edges
        * Roads are directional, weight might be the length to the next interchange, but might also be weighted by traffic (or predicted traffic...)
        * More on this later!

* Social networks are graphs where:
    * Nodes are people, places, pages, posts...
    * Edges connect those things.
        * Many types of edges:
            * "Friends with" (bidirectional)
            * "follows" (unidirectional)
            * "likes" (unidirectional)

* A degree is a graph where:
    * nodes are classes. 
    * edges encode prerequisites.


* Graph search is used to find a shortest path between two nodes.
    * The shortest path from SF to NYC
    * "People you might know..."
    * Fastest way to earn this degree
    
* When graphs are super large, the standard algorithms don't work because they have to search too exhaustively.
    * A* is a graph search algorithm powered by a heuristic
    * The heuristic must be an underestimate of the true cost of getting from A to B.
        * In the "maps" case, you can use Latitude/Longitude and compute the straight line distance, which is always going to be an underestimate! Boom.
    * The algorithm uses the heuristic to prioritize searching nodes that "go in the right direction" and as long as the heuristic is an underestimate of the true cost, the shortest path will be found.
    * If it's not an underestimate A path will be found, but it might not be the shortest one...
        * But it's still often a decent one, so if an approximate solution is acceptable, the heuristic need not be perfect.

* Search is often an underlying component of an overall AI system.
    * Game playing algorithms might use pathfinding or graph search as part of a "model based" algorithm.

* Other graph algorithms can also be VERY useful on certain types of problems. For example:
    * Minimum spanning trees are used in planning telephony/network/road systems.
    * Hamiltonian Path's are used to plan postal routes, especially for "ad hoc" services like Amazon which don't just deliver mail to every house every day.
    * Flow networks are used to model systems that have transmission capacity, such as municipal water supply and internet infrastructure...