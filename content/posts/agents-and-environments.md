---
title: "Intelligent Agents : Rational Behavior, Structure and Environments"
date: "2019-09-20"
template: "post"
draft: false
slug: "/posts/intelligent-agents/"
category: "Artificial Intelligence"
tags:
  - ""
description: ""
---

An **intelligent agent** is an entity that observes and acts upon an environment through its sensors and actuators. It can be a robot in the real world or a software agent within a simulation.

An agent, depending on its environment, can receive a stream of sensory inputs. The inputs at any given instant is called a **percept**. The **percept sequence** is the complete history of all percepts it has perceived. In general, an agent's next action depends on the contents this sequence.

<figure style="width: 500px">
	<img src="/media/artificial intelligence/agent-environment-interaction.png" alt="Agent Environment Interaction">
	<figcaption>Agent Environment Interaction</figcaption>
</figure>

# Rational Behavior

The purpose of any agent is to make some changes in its environment. If the environment undergoes the desired changes then the agent has performed well. This is evaluated using a **performance measure**.

Notice, we use the environment state for evaluation and not the agent state. This is because an agent can delude itself into thinking that its performance is optimal.

## Example

Say we have a vacuum cleaner agent, and we want it to suck up as much dirt as possible. So, we give it a performance measure: **+1** if it cleans up dirt on one tile.

A rational agent can maximize the performance measure by cleaning up all the dirt, dumping it all on the floor and repeating this forever. A more suitable measure will be to reward the agent for having a clean floor.

There remains some knotty issues to untangle. For example, the notion of a clean floor is based on the average cleanliness over time. Yet the same average cleanliness can be achieved by two agents in two ways. One that does a mediocre job all the time and another that cleans energetically but takes long breaks.

Every performance measure can have bad consequences, even if it is well intentioned. As a general rule it is better to design performance measures according to what you want in the environment rather than according to how an agent should behave.

# Rational Action

A rational agent need not know everything, it only has to make the right choice given adequate prior knowledge and informative percept sequence. *What is rational* at any given time depends on four things:

- the performance measure that defines success
- prior knowledge of the environment
- actions that can be performed by the agent
- percept sequence to date

This leads to the definition of a **rational agent** :

<figure>
	<blockquote>
		<p>
    An agent is rational, if it selects an action that is expected to maximize its performance measure, given the evidence provided by the percept sequence and in-built knowledge.
    </p>
	</blockquote>
</figure>

Providing it the ability to learn greatly improves the effectiveness of an agent by slowly weaning away its dependency on prior knowledge. It can also widen the range of environments where it can be effective.

And note that, rationality maximizes *expected performance* not *actual performance*.

# Structure

The simplest approach to build an agent is the **table-driven approach**. Here, we create a table that maps all possible percept sequences to the appropriate next-action. Needless to say, this lookup table will consume immeasurable disk space and in most cases is quite impossible to design.

## The Four Basic Structures

The four basic structures of an agent are:

- Simple reflex agents
- Model-based reflex agents
- Goal-based agents
- Utility-based agents

### Simple reflex agents

These are the simplest type of agents. A **simple reflex agent** selects an action based only on the current percept, ignoring the percept sequence. This is a collection of **condition-action rules**:

```python
if car-in-front-is-breaking
  initiate-breaking
else if car-in-front-is-moving
  move-forward
```

The major problem with such agents is that a little bit of unobservability or incomplete rule-set will cause serious trouble. When a unseen situation occurs, the agent will not have a corresponding reaction in its rule-set. It may be forced to react with a random action.

```python
def simple_reflex_agent(percept):
  persistent: rules

  state <- interpret_input(percept)
  rule <- rule_match(state, rules)
  action <- rule.ACTION

  return action
```

### Model-based reflex agents

To handle the partial observability problem, the agent can maintain an internal state of the external world that depends on the percept sequence. Updating this internal state requires two more pieces of knowledge:

- how the world changes independent of the agent
- how the world is affected by the agent's actions

This knowledge is called a **model**, and the agent is called a **model-based agent**.

```python
def model_based_reflex_agent(percept):
  persistent: rules, state, action, model

  state <- update_state(state, action, percept, model)
  rule <- rule_match(state, rules)
  action <- rule.ACTION

  return action
```

The downside of this approach is that the agent still relies on a fixed set of handwritten rules.

### Goal-based agents

For complex tasks, a state description is not enough information to decide what to do. For example, how will a car decide the action at a fork in the road? It needs a destination or **goal information** which helps the agent evaluate whether a state is desireable or not. This is called a **goal-based agent**.

They do not have inbuilt condition-action rules, rather they use *search* or *planning* algorithms to reach goals, making them more flexible than reflex agents. A goal-based agent's behavior can be changed to go to different destinations easily, unlike a reflex agent where all it's rules have to be rewritten.

### Utility-based agents

Goals provide a crude distinction between desireable and undesireable states. But to get a more nuanced value for desirability we use the **utility** value given by a **utility function**. This is practically an *internal version* of the performance measure that judges the agent.

When you have two **conflicting goals** like safely and speed, then the utility function can make the appropriate tradeoffs. It can also provide a way to consider the **likelihood of success** against the importance of the goals. It is important to note that the utility function only provides the *expected* utility of actions.

# Learning Agents

The ability to learn allows an agent to operate in initially unknown environments by becoming more competent than its in-built knowledge alone might allow. This is a **learning agent** and it has four components :

- Performance element
- Learning element
- Critic
- Problem generator

<figure style="width: 850px">
	<img src="/media/artificial intelligence/learning-agent.png" alt="Learning Agent">
	<figcaption>Learning Agent</figcaption>
</figure>

The **performance element** takes in percepts and decides what action to perform. This element is what we previously considered to be the entire agent. For example, in a car agent, it decides when to apply the breaks and with how much force.

The **learning element** is responsible for making improvements to the performance element. It uses feedback from the critic and determines how the performance element must be modified.

The **critic** tells the learning element how well the agent is doing according to a fixed performance standard. It is required because the percepts themselves do not indicate success nor failure. For example, a chess program could receive a percept indicating that it has checkmated its opponent, but it needs the performance standard to know that's a good thing.

The **problem generator** is responsible for suggesting actions that will lead to new states and experiences, even if they are sub-optimal. This allows the agent to learn and make better decisions in the long run.

## Example

Consider a learning agent for a car. The performance element decides the steering angle and applied force on the brake. Its decision making is improved by the learning element. It can learn that tips tend to increase if the car does not smash into a tree on the way to the destination. The critic tells the learning element that smashing into trees is bad. The problem generator suggests experimenting with the breaks on different road surfaces under various conditions.

# State Representation

**How does an agent encode knowledge?** The representations of agent and environment states can be placed on a range of increasing expressive power. More expressive power translates to a more complex agent design but they are also more concise.

## Types

Three types of state representation are:

- Atomic representation
- Factored representation
- Structured representation

In the **atomic representation**, each state of the world is indivisible; a black box with no internal structure. The algorithms for search and game-playing use atomic representations.

A state with a **factored representation** has a list of attributes with values associated with them. The values can be a boolean, integer, string or an enumeration. Uncertainty can also be expressed by leaving the attribute blank. Areas including constraint satisfaction problems and propositional logic and machine learning use this representation.

**Structured representation** portrays a state as multiple objects, each with their own attributes and relationships with other objects. Relational databases, first-order logic and natural language processing use such forms.

<figure style="width: 550px">
	<img src="/media/artificial intelligence/atomic-factored-structured.jpg" alt="Types of state representation">
	<figcaption>Types of state representation</figcaption>
</figure>

Often, the more expressive language is much more concise; for example, the rules of chess can be written in a page or two of a structured-representation language such as first-order logic but require thousands of pages when written in a factored-representation language such as propositional logic.

On the other hand, reasoning and learning become more complex as the expressive power of the representation increases. To gain the benefits of expressive representations while avoiding their drawbacks, intelligent systems in the real world may need to operate at all points along the axis simultaneously.

# Environments

An agent has to be designed according to its intended **working environment**. Each kind of environment present their own set of problems to it.

Note that real world environments are not necessarily more complex than computer simulations. Making a [self-driving car for the GTA-V open world](https://www.youtube.com/playlist?list=PLQVvvaa0QuDeETZEOy4VdocT7TOjfSA8a) can be more difficult than building an agent to detect defective items on a conveyor. The more restricted the environment is, the easier it is to design an agent.

## Types of Environments

The range of environments that arise in AI is vast, but an environment can still be classified along a small number of **dimensions**:

### Fully Observable vs Partially Observable vs Unobservable

If the agent's sensors can access all properties of environment, relevant for choice of action, then the task environment is **fully observable**. In case of a defective sensor we have a **partially observable** task environment. If the agent has no sensors then the environment is **unobservable**.

### Deterministic vs Stochastic vs Non-Deterministic

If the next state of the environment is completely determined by the current state and action performed by the agent, then we say the environment is **deterministic**. We consider it to be deterministic even if we are unable to predict actions of other agents.

If the agent is not in a deterministic environment, then it has to keep track of all possible current states at each point of time. If there are probabilities associated with each of these states, then it is **stochastic**, otherwise it is **non-deterministic**.

#### Episodic vs Sequential

In an **episodic task environment**, the agent's experience is divided into atomic episodes where one episode does not affect another. In each episode, it receives a percept and it performs a single action. Spotting a defective item in an assembly line is an episodic environment.

In **sequential environments**, an action can have long term consequences. This is more difficult because the agent will have to think ahead.

### Single vs Multi agent

The distinction may seem simple enough. For example, an agent solving a crossword puzzle is in a **single-agent environment**, whereas a chess playing agent is in a **two-agent environment**. There are, however, some subtle issues.

Should an agent A treat another entity B as an agent or as part of the environment? The key distinction is whether the B's behavior is best described as maximizing a performance measure that depends on A's behavior. For example, in chess, A's performance measure depends on moves made by it's opponent agent B.

Another distinction can be made in multi-agent environments: **competition**. Chess is a competitive multi-agent environment, whereas driving is partially cooperative and partially competitive as no one wants an accident but there only a limited number of parking spaces.

Agents designed for multi-agent environments will also have a greater need for communication capabilities. Note that randomized behavior in competitive environments can help avoid the pitfalls of predictability.

### Static vs Dynamic vs Semi-Dynamic

If the working environment undergoes change as the agent is deliberating, then the environment is **dynamic**, otherwise it is **static**.

Static environments are easier, because agent does not worry about the passage of time or observe while thinking. Chess is a static environment, however chess with a clock is **semi-dynamic** because the agent's performance measure changes even though environment is unchanging. Taxi driving is dynamic because the other taxis do not stop moving.

### Discrete vs Continuous

This distinction applies to the way time, the states of the environment or percepts are handled. A chess environment has a finite number of **distinct states**. Taxi-driving has a **continuous environment state** (speed and location of vehicles have a range of values) and also has continuous actions (steering angles, etc).

### Known vs Unknown

If the agent knows the rules or laws of physics of the environment, ie. knows outcome of all actions, then it is a **known environment**, otherwise it is an **unknown environment**. Obviously, if the environment is unknown, then the agent has to learn how it works to make good decisions.

It is quite possible for an agent to be in a known and yet partially observable environment. Card games are an example of this. Her
e, we know the rules of the game but we cannot see what cards the opponent has. Conversely, an unknown environment can be fully observable, as in a new video game. Here I can see the whole screen but have no idea what the controller's buttons do until I try them.

# References

- [Artificial Intelligence: A Modern Approach](http://aima.cs.berkeley.edu/)
