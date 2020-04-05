Summary and A* Pseudocode
This algorithm described by Sebastian is very similar to other search algorithms you may have seen before, such as breadth-first search, except for the additional step of computing a heuristic and using that heuristic (in addition to the cost) to find the next node.

A* Pseudocode

Search( grid, initial_point, goal_point ) :

1. Initialize an empty list of open nodes.

2. Initialize a starting node with the following:

	- x and y values given by initial_point.
	- g = 0, where g is the cost for each move.
	- h given by the heuristic function (a function of the current coordinates and the goal).

3. Add the new node to the list of open nodes.

4. while the list of open nodes is nonempty:
	- Sort the open list by f-value
	- Pop the optimal cell (called the current cell).
	- Mark the cell's coordinates in the grid as part of the path.
	- if the current cell is the goal cell:
		- return the grid.

	- else, expand the search to the current node's neighbors. This includes the following steps:

		- Check each neighbor cell in the grid to ensure that the cell is empty: it hasn't been closed and is not an obstacle.
		- If the cell is empty, compute the cost (g value) and the heuristic, and add to the list of open nodes.
		- Mark the cell as closed.
5. If you exit the while loop because the list of open nodes is empty, you have run out of new nodes to explore and haven't found a path.

## The code for the **A* search algorithm** has been broken down into the following functions:

- CellSort() - sorts the open list according to the sum of h + g
- ExpandNeighbors() - loops through the current node's neighbors and calls appropriate functions to add neighbors to the open list
- CheckValidCell() - ensures that the potential neighbor coordinates are on the grid and that the cell is open
- Heuristic() - computes the distance to the goal
- AddToOpen() - adds the node to the open list and marks the grid cell as closed
