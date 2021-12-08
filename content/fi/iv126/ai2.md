---
date: 2021-10-10
title: lec 2
url: fi/iv126/2
---


# Neighborhoods

Definition: Function of neighborhood N is mapping \\( N: S \rightarrow 2^S \\), which assign every solution s from Z, set of solutions \\( N(S) \subset S \\)

{{<image src="/images/iv126/neighborhoods.png" position="center" alt="neighborhoods" >}}

# Effective Algorithms for Searching in Very Large Neighborhoods

space size: polynom of higher order of magnitude (n > 2)

main problem is indentification of improving neighborhoods or best neighbor without enumeration of whole neighborhood.

# Ejection Chain

e.g. Capacitated Vehicle Routing Problem

ejection chain: sequence of moving customer from one round to next one:  
- each ejection chain includes k levels starting at round 1 and ending at round k
- vertex is removed from round 1 and moved to round 2, vertex from round 2 is moved to round 3 and so on until vertex k-1 to k, last vertex from round is moved to round 1.

succesful change: no vertex is in solution more than once

ejection chain must be cyclic. This can be satisfied with placing last consistently last customer to last round.

{{<image src="/images/iv126/ejection-chain.png" position="center" alt="neighborhoods" >}}


# Cyclic Exchange in Groups

Problems with dividing n elements to q groups

/todo


# Incremental Evaluation of Neighborhood

Evaluation of solution is most expensive part of computation.

**Naive Evaluation**: complete evaluation of every solution in neighborhood.

Goal: Design suitable incremental evaluation of neighborhood.


e.g.

{{<image src="/images/iv126/k-opt.png" position="center" >}}


$$ \delta f = distance(A, E) + distance(C, D) - distance(A, D) - distance(C, E)$$


# Local Space Seach


## 2-opt

Simple local search algorithm for solving the traveling salesman problem. The main idea behind it is to take a route that crosses over itself and reorder it so that it does not. 

{{<image src="/images/iv126/2opt.png" position="center" >}}

## Selection of Neighbor from Neighborhood

**Steepest descent** - selecting the best neighbor (i.e. neighbor that most improve objective function)
**First Improving** - systematic/deterministic selection of first neighborhood that is better than current solution
**Random Selection** - random selection from improving neighbors.



# State Space

is defined by oriented graph G = (S, E), where set of vertices S corresponds to problem solutions defined by their representations and set of edges E is defined by operator of change used for generating
neighbors.


# Landscape

Landscape I is defined by pair (G, f), where G is state space and f is objective function, which is used for search.

# Fitness Landscape

Also called adaptive landscapes are used in evolution algorithms for visualization of relationship between genotypes and reproductive success.

# Accept Nonimproving Neighbors

## Simulated Annealing

SA use random selection of neighbor from neighborhood. Selection of better neighbor is always accepted (as is at Hill Climbing) but accept also a worse neighbor.
At start of search there is allowed bigger probability of worsening the solution, gradually the probability is decreasing.

## Threshold Accepting

Deterministic variant of SA.
Accept also worse solutions with max deterioration of threshold value Q.

## Great Deluge Algorithm

Analogy with flood and rising water surface. Climber (solution quality) always remain above water surface.


Algorithm for minimalization problems: we must decrese surface and we are trying to remain under surface


- If we are rising to quickly we found poor quality solution.
- When rising the computational complexity is also increasing.


## Tabu search

Deterministic extension of basic state space search algorithm. Often combined with other algorithms.

Allow to accept also worse solutions. Solution of worse quality is accepted when there is no better.
Cycles are prevented by so called tabu list.

**Tabu list**  
List with N last changes, which are forbidden. N is typically 5 to 9.


**Aspiration Criteria**  
Condition with which it's also possible to make changes included in Tabu List.
e.g. allowing changes that leads to better value of objective function.


# Iterative With Different Solutions

## Multistart Local Seach

Repeating of local search. Initial Solution is randomly generated with every new iteration.

## Iterative Local Search

Improving of Multistart Local Search. Found local optima is changed and used at next local search. Can be used with any local search algorithm.


# Change Landscape of the Problem

## Different Neighborhoods

### Variable Neighborhood Search

The idea is we are using another landscape to get out of local optima.

e.g. planning school timetable - to find some better solution, we can move one lecture to empty place, or we can move 10 lectures, which gives us more space to work (and to find better solution), but we
also need to compute more. So we often work with 'embedded neighborhoods'. Neighborhood i represents change of i + 1 lectures in timetable.


{{<image src="/images/iv126/vns.png" position="center" alt="vns">}}


### Variable Neighborhood Descent

VNS based on improving search with variable neighborhood. VND is deterministic version of VNS.

If we take school timetable - It's not needed to move 10 lectures if 2 is enough, so after each improvment we are going back

{{<image src="/images/iv126/vnd.png" position="center" alt="vns">}}

note: There are also nondeterministic variants working on similar principle.

# Change of the Objective Function or the Data Input


## Guided Local Seach

repeated local searches with modified value of objective function.
Every solution \\( s \in S \\) has set m characteristics with price \\( c_i \\)

$$ I_i(s) = 1 if s has characteristic i else 0 $$ 

effor to search within a part of space with lower prices of characteristics.
e.g. TSP: if edge (a, b) is in solution, price is determined by edge lenght (cities distance).

New objective function:

$$
f'(s) = f(s) \lambda \sum^m_{i=1} p_i I_i(s)
$$

penalization p_i: meaning of characteristic (we don't want big penalization). \\( p_i \\) is initialized to 0 for every i. \\( \lambda \\) is used for normalization

In TSP characteristic is one route (edge) of graph.

Characteristic with highest utility (hodnota) \\(u_i(s) = I_i(s) \frac{c_i}{1+p_i} \\) is penalized. Next time we want to avoid characteristics with high price. Characteristics used in solutions get
penalized for support of diversification.


Intensification:
 - GLS search through space with lower prices \\( c_i \\)

Diversification:
 - Characteristics used in generated local optima are penalized to avoid them next time.


/todo example








