# Exercise: CSPs and Combining Them With Other Stuff

## Questions

For each of the below scenarios, answer the following questions:

1. How can you model this problem as a constraint satisfaction problem?
    * What are the variables?
    * What is the domain?
    * Do you need to "relax" the problem somehow (for example using discrete instead of continuous variable values)? 
2. Can you quantify the size of the search space?
    * How many variables? 
    * How many values per variable? 
    * How many unique "states" result from those two facts?
    * Can you make a reasonable guess at how many such states are constraint violating?
    * Can you make a prediction about how early in the search process a constraint violation might be found?
2. Can you think of anything about the structure of the problem that could help you choose variable assignments in an efficient way?
3. Can you think of any heuristics that might help you assign variables in a clever way?
4. Could you use another form of AI to assign variables in a clever way?

## Scenarios

### Scheduling NBA games

The National Basketball Association is a professional basketball league comprised of 30 teams. Each year they must schedule 1230 games for the season. The actual constraints are even more complex than presented below, but here are SOME of the constraints:

* The 30 teams are divided into 2 equally sized conferences. 
    * Teams in the same conference must play each other 4 times over the course of the season.
    * Teams in opposite conferences must play each other 2 times over the course of the season.
* Each team must play 41 home games and 41 away games.
* Each team can only play one game per day.
* Teams may never play games for three consecutive days, but can play games on two consecutive days.
* Games must always be scheduled at appropriate times:
    * M-F games must start after 5:00pm but before 8:01pm (in local time to the arena)
    * Saturday/Sunday games may start after 12:00 noon but before 8:01pm
* Games must not overlap with other events in their respective arenas

Once you've answered the above questions, consider the following:

* TV contracts create "soft" constraints, or preferences for game times to maximize viewership. For example, if the Boston Celtics are playing a game at the LA Lakers stadium, there is a preference to start that game EARLIER so that Boston fans can watch it on TV.
    * Discuss possible ways to work this into your model.

* Consider the problem of data collection:
    * Who knows the arena schedules?
    * Who knows all the details of the TV contracts?
    * How might this data be collected for processing by a central system?

* Travel creates soft constraints: It's hugely disadvantageous for a team to have back-to-back games in New York then in San Francisco, but it is more reasonable to have back-to-back games in Salt Lake City then in Denver.
    * How might you account for these constraints?