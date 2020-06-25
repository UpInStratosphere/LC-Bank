## DFS
- DFS will keep traverse down a path until the current node's has no more unprocessed neighbor nodes (all processed). The backtracking part means that paths will go down whenever possible, only returns back and explore another path in the upper level once all lower level paths are finished.

- running DFS on all nodes a graph visit each nodes only once, and can group the nodes into disjointed components (in which all the nodes in the same component are all connected together). There may be one or more disjointed components in an undirected graph.
    - whenever the current node is marked as visited, it means it is already placed in a component (could be the current component OR another prior component). The point is that the current node is already processed and should not processed again BECAUSE the function that processed the current node the first time will process all of the current node's neighbors.
    
- running DFS on a source node and target node will let us determine if src node is connected to target(whether two are in the same connected component).
    - return as soon as target is found (can also build the path from src to target backwards as we return in each function), OR 
    - return when all nodes that are connected to src are visited and did not find the target node.
    
## BFS
- used to find the shortest path between two nodes in a graph
- a visited graph is also used. If a neighbor node is marked as visited, then it is either visited in a shorter path or visited previously in the same level. 
