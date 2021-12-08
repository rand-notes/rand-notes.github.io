---
date: 2021-10-05
title: lec 1
url: fi/iv126/1
---


{{<image src="/images/iv126/optimization-methods.png" position="center" alt="optimization-methods">}}

# Approximate Methods


is usually understood to give an approximate solution, with some kind of **guarantee of performace**. i.e. it solves TSP, and the total cost is never off by more than a factor of 2.


## Exploration (Diversification)

> Terms Diversification and Intensification are being used mostly in conjunction with population-based optimization techniques

consists of probing a much larger portion of the search space with the hope of finding other promising solutions that are yet to be refined. This operation amounts then to diversifying the search in
order to avoid getting trapped in a local optimum. By doing so, we would be doing, de facto, a global search.


## Exploitation (Intensification)


consists of probing a limited (but promising) region of the search space with the hope of improving a promising solution S that we already have at hand. This operation amounts then to intensifying
(refining) the search in the vicinity of S. By doing so, we would be doing, de facto, a local search..

## Heuristic Algorithms

is essentially a hunch. Heuristic algorithms is the case that we notice a event but doesn't have any proof. As is solving the traveling salesman problem by starting at a random vertex and going to the
nearest not yet visited each step. It is a plausible idea, that should not give a too bad solution. In this case, it can be shown that it won't always give a good solution.


### Metaheuristics

is a higher-level procedure or heuristic designed to find, generate, or select a heuristic (partial search algorithm) that may provide a sufficiently good solution to an optimization problem, especially
with incomplete or imperfect information or limited computation capacity.

#### Metaheuristics Classification

{{<image src="/images/iv126/metaheuristics.png">}}

##### Local Search vs Global Search


One type of search strategy is an improvement on simple local search algorithms. A well known local search algorithm is the hill climbing method which is used to find local optimums. However, hill
climbing does not guarantee finding global optimum solutions.

Many metaheuristic ideas were proposed to improve local search heuristic in order to find better solutions. Such metaheuristics include simulated annealing, tabu search, iterated local search, variable
neighborhood search, and GRASP. These metaheuristics can both be classified as local search-based or global search metaheuristics.

Other global search metaheuristic that are not local search-based are usually population-based metaheuristics. Such metaheuristics include ant colony optimization, evolutionary computation, particle
swarm optimization, genetic algorithm, and rider optimization algorithm.


##### Single-solution vs Population-based

Single solution approaches focus on modifying and improving a single candidate solution; single solution metaheuristics include simulated annealing, iterated local search, variable neighborhood search,
and guided local search.

Population-based approaches maintain and improve multiple candidate solutions, often using population characteristics to guide the search; population based metaheuristics include evolutionary
computation, genetic algorithms, and particle swarm optimization.

Another category of metaheuristics is Swarm intelligence which is a collective behavior of decentralized, self-organized agents in a population or swarm. Ant colony optimization, particle swarm
optimization, social cognitive optimization are examples of this category.


##### Hybridization and Memetic Algorithms

A hybrid metaheuristic is one that combines a metaheuristic with other optimization approaches, such as algorithms from mathematical programming, constraint programming, and machine learning. Both
components of a hybrid metaheuristic may run concurrently and exchange information to guide the search.


On the other hand, Memetic algorithms represent the synergy of evolutionary or any population-based approach with separate individual learning or local improvement procedures for problem search. An
example of memetic algorithm is the use of a local search algorithm instead of a basic mutation operator in evolutionary algorithms.


##### Parallel Metaheuristics

A parallel metaheuristic is one that uses the techniques of parallel programming to run multiple metaheuristic searches in parallel; these may range from simple distributed schemes to concurrent search
runs that interact to improve the overall solution.


##### Nature-inspired and Metaphor-based Metaheuristics


A very active area of research is the design of nature-inspired metaheuristics. Many recent metaheuristics, especially evolutionary computation-based algorithms, are inspired by natural systems. Nature
acts as a source of concepts, mechanisms and principles for designing of artificial computing systems to deal with complex computational problems. Such metaheuristics include simulated annealing,
evolutionary algorithms, ant colony optimization and particle swarm optimization.


### Main Concepts for Metaheuristics


#### Representation

Representation have big impact on effectiveness and efficiency of any metaheuristic. A representation must have the following characteristics:

- **Completeness**: All solutions associated with the problem must be represented.
- **Connexity**: very important in designing any search algorithm. A search path must exist between any two solutions of the search space. Any solution of the search space, especially the global optimum
	solution, can be attained.
- **Efficiency**: The representation must be easy to manipulate by the search operators. The time and space complexities of the operators dealing with the representation must be reduced.

{{<image src="/images/iv126/representation.png" position="center" alt="optimization-methods">}}


**Linear Representations**  
 - strings of chars given alphabet
 - binary encoding, discrete encoding, permutation, vector of real numbers

**Non-Linear Representation**  
 - often based on graph structures, especially used trees


**Binary Encoding**  
The binary encoding consists in associating a binary value for each decision variable. A solution will be encoded by a vector of binary varibles.


**Discrete Encoding**  
Generalization of binary encoding. Solution is represented as vector of discrete values i.e. variables have values from alphabet. Used for problems where variables acquire values from finite domain e.g.
combinatorics problems or assignment problem.

**Assignment Problem**  
we have given set of n tasks, which have to be assigned to m agents so we maximaze overall gain. Task can be assigned to any agent. Solution represents a vector s with size n, where \\( s_i \\)
represents agent assigned to task i. \\(s_i = j \\) if agent j is assigned to task i.


**Permutation Problems**  

Every problem element must be only once in representation. e.g. sequencing, routing, planning

**Representation of Permutations**

e.g. TSP (n cities, that TS must go through), solution represents cities permutation denoting order of visited cities.


#### Objective Function


The objective funcction f formulates the goal to achieve. It associates with each solution of the search space a real value that describes the quality of solution, \\(f: S \rightarrow \mathbb{R} \\).
Also some decoding function d may be applied, \\( d: R \rightarrow S \\), to generate a solution that can be evaluated by the function f.

**Self-Sufficient Objective Function**

For some optimization problems, the definition of the objective funtion is straightforward. It specifies the originally formulated objective function. 
Self-Sufficient function is e.g. TSP - \\( min \sum dist(x, y) \\), example of non-sufficient could be SAT (T/F)


**Guided Objective Function**

For other probles, the definition of the objective funtion is a difficult task and constitutes a crucial quiestion. The objective function has to be transformed for a better convergence of the
metaheuristic. The new objective function will guide the search in more efficient manner.

**Relative and Competitive Objective Functions**

Used if function can't assign absolute value to all solutions.

e.g. game theory, strategy `A, B, C : A < B, B < C, C < A`


**Meta-Modeling**

at extremely computationally difficult objective functions is designed approximate model with a approximate objective functions.


#### Constrain Handling

**Reject Strategies**

we keep only consistent solutions.

**Penalizing Strategies**

Origin objective function is extended by a penalty function that will penalize inconsistent solutions. Depends on weights of nonsatisfied constraints. Penalty is order of magnitude higher that value of
objective function.

**Repairing Strategies**

Repairing inconsistent solutions by applying repairing strategies over generated inconsistent assignments, which will be repaired and it continue with another inconsistent solution.


#### Parameter Tuning

{{<image src="/images/iv126/parameters-init.png" position="center" alt="optimization-methods">}}


**Offline initialization**

We set parameters and start the algorithm.

- setting one parameter after another (nonoptimal)
- **Design of Experiments** - k factors/parameters with n possible values: n^k experiments
- statistical inferences, ML, ...

**Online initialization**

parallel algorithm restart with different parameters 



### Problem-specific heuristics

Heuristics is approximate solution to given problem. Meanwhile metaheuristics doesn't solve any specific problem, heuristics are tailored to some problem.


## Initial Solutions

- quality vs computational time
- using better initial solution not always leads to better local optima
- Generating consistent random solutions might be difficult for highly constraint problems

Main strategies:  
- random solution
- heuristic solution (i.e. by greedy algorithm)
- partially or fully initialized by user





