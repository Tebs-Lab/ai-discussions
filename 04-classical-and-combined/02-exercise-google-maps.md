# Exercise: Graph Modeling

## Questions

For each of the below situations, answer the following questions:

* In order to model this problem as a graph...
    * What should the nodes represent?
        * What properties might nodes have?
        * How will we collect this information about each node?
    * What should the edges represent?
        * What properties might edges have?
        * Are edges directed or undirected (might depend on the edge type even in a single graph)?
        * How will we collect this information about each edge?

* Once we know what the graph represents...
    * What properties might this graph have that are useful in solving the problem?
        * Are shortest paths useful in some way?
        * Are spanning trees useful in some way?
        * Are circuits (euclidian or hamiltonian) useful in some way?
        * Are there other properties of the graph that might be useful?

## 1. Roadways

Consider the modern marvel that is Google Maps... We can use this software to:

* Get directions from A to B
    * Driving, walking, biking, and on public transit!
* Model traffic patterns in real time
* And more. You've used it, you know what it can do!

Using the above questions as a guide, try to reverse engineer an appropriate graph representation of Google Maps. Consider the AI involved in pathfinding, but also consider the infrastructure and data collection systems that must power this major AI achievement (that is often not even considered AI!!). 

Then, answer these questions as well:

* How Can/Might/Does Google Maps (and competitors) combine supervised learning and graph search to route you along the fastest (rather than shortest) path?
    * Consider the constraints of the A* search algorithm...
* Consider the risks and pitfalls of real time data collection and adversarial samples… https://www.theverge.com/2020/2/3/21120463/google-maps-traffic-jams-99-phones-little-red-wagon-simon-weckert 
    * Could AI be used to mitigate this type of "attack" against the system?
* ...

## 2. Mapping Human Relationships

Consider the horrific catastrophe that are modern social networks... They use their software to:

* Discover our relationships with:
    * Other people
    * Businesses
    * Ideas/concepts
    * Products
* Predict our likelihood of:
    * Making purchase decisions
    * Knowing certain other people
    * Wanting a particular job
* And much more. 

Pick one of:

* Facebook
* Twitter
* LinkedIn
* YouTube
* Or another prominent social network that interests you...

Then use the above questions as a guide to model their most interesting data as a graph. Furthermore consider these:

* At or near their core, all of these systems are using the data they collect to generate recommendations, either of advertisements, videos or posts on the site itself, other people who use the service, etc.
    * Can any of our graph properties be used to help generate such recommendations directly?
    * What about indirectly, or in concert with other algorithms?
    * To explore this question you may wish to look into:
        * Graph Neural Networks,
        * content based Filtering,
        * Collaborative Filtering,
    * Can you think of a way to extract information from this graph that could then be passed through one of the other types of ML models we've discussed?
        