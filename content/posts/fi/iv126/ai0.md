---
date: 2021-09-02
title: ai 0
url: iv126/0
---

# Environments

## Fully Observable vs Partially Observable

If an agent's sensors give it access to the complete state of the environment at each point in time, then we say that he task environment is fully observable. If the agents has no sensors at all then the
environment is **unobservable**


## Single-Agent vs Multi-Agent Environments


For example, an agent solving a crossword puzzle by itself is clearly in a single-agent enviroment, whereas an agent playing chess is in a two-agent enviroment. Sometimes the border is blurred. The key
is performance measure whose value depends on agent A behavior. For example in chess, the opponent V is trying to maximize its performance measure, which, by the rules of chess, minimizes agent A's
performance measure. This, chess is a **competitive** multiagent environment. On the other hand, in the taxi-driving environment, avoiding collisions maximizes the performance measure of all agents, so its
is a partially **cooperative** multiagent environment.

## Deterministic vs Nondeterministic

If the next state of the environment is completely determined by the current state and the action executed by the agent(s), then we say the environment is deterministic; otherwise, it is
nondeterministic.

If the environment is parially observable, however, then it could appear to be nondeterministic. Most real situations are so complex that it is impossible to keep track of all the unobserved aspects; for
practical purposes, they msut be treated as nondeterministic.

**We say that a model of the environment is stochastic if it explicitly deals with probabilities.**

> Stochastic != Nondeterministic


## Episodic cs Sequential

In an episodic task environment, the agent's experience is divided into atomic eppisodes. In each episode the agent receives a percept and then performs a single action. Crucially, the next episode does not depend on the actions taken in previous episodes. In sequential environments, on the other hand, the current decision could affect all future decisions. 

Chess and taxi driving are sequential: in both cases, short-term actions can have long-term consequences. On the other hand, detecting defected item on assembly line doesn't affect whether the next part
is defective so it's episodic.

Episodic environments are much simpler than sequential environments because the agent does not need to think ahead.


## Static vs Dynamic

If the environment can change while an agent is deliberating, then we say the environment is dynamic for that agent; otherwise, it is static. Static environments are easier to deal with because the agent
need not keep looking at the world while it is deciding on an action. Dynamic environments, on the other hand, are continuously asking the agent what it wants to do; if it hasn’t decided yet, that counts
as deciding to do nothing. If the environment itself does not change with the passage of time but the agent’s performance score does, then we say the environment is **semidynamic**. 

Taxi driving is clearly dynamic: the other cars and the taxi itself keep movingwhile the driving algorithm dithers about what to do next. Chess, when played with a clock,is semidynamic. Crossword puzzles are static.


## Discrete vs Continuous


The discrete/continuous distinction applies to the state of the environment, to the way time is handled, and to the percepts and actions of the agent.


## Known vs Unknown

Strictly speaking, this distinction refers not to the environment itself but to the agent's (or designer's) state of knowledge about the "laws of physics" of the environment. In a known environment, the
outcomes (or outcome probabilities if the environment is nondeterministic) for all actions are given. Obviously, if the environment is unknown, the agent will have to learn how it works in order to make
good decisions.

The distinction between known and unknown environments is not the same as the one between fully and partially observable environments. It is quite possible for a known
environment to be partially observable—for example, in solitaire card games, I know the rules but am still unable to see the cards that have not yet been turned over. 

Conversely, an unknown environment can be fully observable—in a new video game, the screen may show the entire game state but I still don’t know what the buttons do until I try them.

# The Structure of Agents

The job of AI is to design an agent program that implements the agent function—the mapping from percepts to actions. We assume this program will run on some sort of computing device with physical sensors and actuators—we call this the agent architecture:

> agent = architecture + program


## Simple Reflex Agents

The simplest kind of agent that select actions on the basis of the current percept, ignoring the rest of the percept history.

Use **condition-action rule** -- `**if** car-in-front-is-braking **then** initiate-braking`

Sometimes we can create rules that will create infinite fail loop, in these cases we can **randomize** agents action.


## Model-based Reflex Agents

The most effective way to handle partial observability is for the agent to keep track of the part of the world it can't see now. That is, the agent should maintain some sort of **internal state** that
depends on the percept history and thereby reflects at least some of the unobserved aspects of the current state. 

Updating this internal state information as time goes by requires two kinds of knowledge to be encoded in the agent program in some form. First, we need some information about how the world changes over
time, which can be divided roughly into two parts: the effects of the agent’s actions and how the world evolves independently of the agent. i.e. if agent turns right the car goes right; if raining the
cameras get wet. This knowledge about world is called a **transition model**.

Second, we need some information about how the state of the world is reflected in the agent’s percepts. For example, when the car in front initiates braking, one or more illuminated red regions appear in
the forward-facing camera image. This kind of knowledge is called **sensor model**.

Together, the transition model and sensor model allow an agent to keep track of the state of the world—to the extent possible given the limitations of the agent’s sensors. An agent that uses such models
is called a **model-based agent**.



## Goal-based Agents

Knowing something about the current state of the environment is not always enough to decide what to do. For example, at a road junction, the taxi can turn left, turn right, or go straight on. The correct
decision depends on where the taxi is trying to get to and for that agent needs some sort of **goal** information (i.e. being at final destination).

The agent program can combine this with the model (the same information as was used in the model-based reflex agent) to choose actions that achieve the goal.

Sometimes goal-based action selection is straightforward—for example, when goal satisfaction results immediately from a single action. Sometimes it will be more tricky—for example, when the agent has to
consider long sequences of twists and turns in order to find a way to achieve the goal. **Search** and **Planning** are the subfields of AI devoted to finding action sequences that  achieve the agent's
goals.


## Utility-based Agents


Goals alone are not enough to generate high-quality behavior in most environments. For example, many action sequences will get the taxi to its destination (thereby achieving the goal), but some are
quicker, safer, more reliable, or cheaper than others. For this we use term **utility**-the quality of being useful; therefore how happy the agent is. An agent’s utility function is essentially an
internalization of the performance measure. Provided that the internal utility function and the external performance measure are in agreement, an agent that chooses actions to maximize its utility
will be rational according to the external performance measure.

Technically speaking, a rational utility-based agent chooses the action that maximizes the **expected utility** of the action outcomes—that is, the utility the agent expects to derive, on average, given the
probabilities and utilities of each outcome.



# Summary

- An agent is something that perceives and acts in an environment. The agent function for an agent specifies the action taken by the agent in response to any percept sequence.

- The performance measure evaluates the behavior of the agent in an environment. A rational agent acts so as to maximize the expected value of the performance measure, given the percept sequence it has
	seen so far.
- A task environment specification includes the performance measure, the external environment, the actuators, and the sensors. In designing an agent, the first step must always be to specify the task
	environment as fully as possible.

- Task environments vary along several significant dimensions. They can be fully or partially observable, single-agent or multiagent, deterministic or nondeterministic, episodic or sequential, static or
	dynamic, discrete or continuous, and known or unknown.

- In cases where the performance measure is unknown or hard to specify correctly, there is a significant risk of the agent optimizing the wrong objective. In such cases the agent design should reflect
	uncertainty about the true objective.

- The agent program implements the agent function. There exists a variety of basic agent program designs reflecting the kind of information made explicit and used in the decision process. The designs
	vary in efficiency, compactness, and flexibility. The appropriate design of the agent program depends on the nature of the environment.

- Simple reflex agents respond directly to percepts, whereas model-based reflex agents maintain internal state to track aspects of the world that are not evident in the current percept. Goal-based agents
	act to achieve their goals, and utility-based agents try to maximize their own expected “happiness.”

- All agents can improve their performance through learning.


{{<image src="/images/agents.png" alt="Agents" position="center" >}}


