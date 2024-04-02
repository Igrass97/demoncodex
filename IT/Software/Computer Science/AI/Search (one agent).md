Search the optimal solution to a problem with AI.

## Node
A **Node** is a data structure which contains:
1. A state
2. A parent (node that generated this node)
3. An action (action applied to parent to generate the node)
4. A path cost (from initial state to node)

### Expand a node
Consider all the possible states that I can get with the available actions for the node. (only the neighbors)

## Uninformed Search Problems
Search strategy that uses no problem-specific knowledge.

1. Start with a frontier that contains the initial state.
2. Start with an empty explored set.
3. Repeat:
	-  If the frontier is empty, there is no solution.
	-  Remove a node from the frontier.
	-  If node contains goal state, return the solution.
	-  Add the node to the explored set.
	-  Expand node, add resulting nodes to the frontier only if they aren't ready in the frontier or the explored set.

### Frontier
The data structure that is chosen for the frontier, will have impact on the efficiency and results of the algorithm.

#### Depth-First Search (using a Stack)
Last-in First-out

Search algorithm that always expands the deepest node in the frontier. It will go very deep into the graph, and then backup and try another way.

#### Breadth-First Search (using a Queue)
First-in First-out

Search algorithm that always expands the shallowest node in the frontier.
It will find the optimal solution.

## Informed Search Problems
Search strategy that uses problem-specific knowledge to find solutions.

### Greedy best-first search
Search algorithm that expands the node that is closest to the goal, as estimated by a heuristic function h(n).

**Example (Manhattan distance):** In a Maze problem, an heuristic function could be a function that estimates the distance between the nodes in the frontier and the goal, and takes the node with less distance (ignoring walls).

### A* search
Search algorithm that expands node with lowest value of g(n) + h(n)

g(n) = cost to reach node
h(n) = estimated cost to goal

It gives the optimal solution only if:
1. h(n) is admissible (never overestimates the true cost)
2. h(n) is consistent (for every node n and successor n1 with step cost c, h(n) <= h(n1) + c)