# Search Algorithms in the Pacman Landscape
In this project, we implement various search algorithms(DFS, BFS, Dijkstra, A*, Greedy) to help Pacman traverse through mazes and complete various challenges.
## Graph Search
Each of the search algorithms follow the structure below with changes only to the fringe.
```python
function Graph-Search(problem, fringe):
    closed = []
    fringe.insert(MAKE-NODE(INITIAL-STATE[problem]))
    
    while not fringe.isEmpty():
        node = fringe.pop()
        if problem.isGoalState(node) return actions
        if node not in closed:
            closed.insert(node)
            children = problem.getSuccessors(node)
            for child in children:
                fringe.push(child)
```
### Depth-First Search (DFS)
<img align="left" width="200" height="200" src="images/search-dfs.gif"> DFS uses a stack(last-in, first out) structure as the fringe representation.  The algorithm selects the deepest fringe node from the start node for expansion.  

In general, DFS is not complete: for graphs with infinitely many nodes, the algorithm can fail to terminate at a target node.  It is also not optimal, since it only finds the "leftmost" solution without regard for path costs.

If the tree has a maximum depth m, the time complexity of the algorithm is O(b^m) and the space complexity is O(bm). 

### Breadth-First Search (BFS)
<img align="right" width="200" height="200" src="images/search-bfs.gif"> BFS uses a queue(first-in, first out) structure as the fringe representation.  The algorithm selects the shallowest fringe node from the start node for expansion.  

BFS is complete: if a solution exists, it must have finite depth which BFS will eventually search.  However, BFS is not optimal, as it does not consider path costs when determining which nodes to replace on the fringe.

If the solution is at depth s, the time complexity of the algorithm is O(b^s) and the space complexity is O(b^s). 

### Dijkstra
<img align="left" width="400" height="200" src="images/search-ufs.gif"> Dijkstra uses a priority structure as the fringe representation.  The algorithm selects the lowest code fringe node from the start node for expansion.  

Like BFS, Dijkstra is complete: if a solution exists, it must have finite depth which the algorithm will eventually search.  Unlike BFS, Dijkstra is optimal(in the case where all edge-costs are positive), since we explore nodes in order of increasing path cost.

### A* Search
<img align="right" width="250" height="250" src="images/search-astar.gif"> A* Search uses a priority structure as the fringe representation.  The priorities are determined by the sum of the edge cost and the value of the heuristic function.  Our implementation of the algorithm allows for multiple heuristics.  The search with a <a href = https://en.wikipedia.org/wiki/Taxicab_geometry>Manhattan Heuristic</a> is shown to the right.

The algorithm is complete and optimal in the case of an appropriate heuristic, requiring both admissibility(heuristic values are non-negative and less than the true optimal forward cost from a given position) and consistitency(heuristic path costs are less than true optimal path costs between nodes). 

