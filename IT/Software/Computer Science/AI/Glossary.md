## Agent
Entity that perceives it's environment and acts upon that environment.

## State
Configuration of the agent and its environment.

## Initial State
Starting point

## Actions
Choices that can be made in a state.

``` MATH
ACTIONS(s) returns the set of actions that can be executed in state s
```

## Transition model
A description of what state results from performing any applicable action in any state.

``` MATH
RESULT(s, a) returns the state after performing action a in state s
```

## State Space
The set of all states reachable from the initial state by any sequence of actions.

Can be represented as GRAPHS.

## Goal Test
Way to determine whether a given state is a goal state.

## Path Cost
Numerical cost associated with a given path. (how expensive is to get to the goal test).

## Solution
A sequence of actions to get to the goal.

## Optimal Solution
A solution that has the lowest path cost among all solutions.
