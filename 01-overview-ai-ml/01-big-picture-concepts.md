# Big Picture AI and ML Concepts

In this section we are attempting to layout the scope of the field of AI, and in so doing foreshadow the rest of the class.

## Narrow vs Broad AI & General AI 

* "Artificial General Intelligence" is what most sci-fi movies portray: A machine that "thinks" in very much the same way we imagine humans and many other animals thinking.
    * Such machines take in all kinds of input (like animals) and can perform reasoning based on those inputs in a wide variety of contexts.
    * The SOTA in AI is currently quite far from this. 

* Instead, we have "narrow" AI systems.
    * These can achieve superhuman results, but only in quite limited domains.
    * AlphaGo can play Go, but it cannot answer even the most basic math questions.
    * Watson can answer a variety of well-formed questions, but can't play Go.
    * Self driving cars can't ride a bike...
        * In fact the "navigation" and "driving" components are separate, and several more purpose-built AI systems power different aspects of driving.
            * A CNN system for object localization
            * A separate system to process LIDAR input
            * A Reinforcement Learning agent to process the outputs of these other AI's and make decisions to turn the wheel or accelerate/decelerate...
            * Explicitly NOT one unified system making decisions. Many smaller systems added together.

## ML vs Non-ML systems

* Machine learning systems are a form of AI that involve automatically finding patterns in large datasets
* Many AI systems don't work this way. For example:
    * Google Maps uses an explicit model of the world and graph search to find the shortest path between two places.
        * Although ML is now used to predict traffic.
    * Deep Blue (the chess AI) was an "expert system" that just did tree search and used hand crafted algorithms to determine the value of each move.
    * (there are many others, feel free to share your favorite)

* ML is becoming especially popular for a few reasons:
    1. Hardware is much faster now than ever before, and ML works best with access to lots of computational power.
    2. The internet age has resulted in a wide variety of incredibly large datasets.
    3. Some types of patterns are extremely hard to define explicitly, and ML systems have become adept at finding some such patterns. 
        * Computer vision and weather prediction are two prime examples.

## Sample of applications:

Pick a few of your favorites and talk about them.

* Forecasting (many kinds)
* Image classification, localization, segmentation, generation
* Text classification, generation, translation
* Pathfinding
* Scheduling
* Game Playing
* Recommendation Engines
