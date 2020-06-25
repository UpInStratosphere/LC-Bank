## DFS
- running DFS on a graph is usually used to divide all the nodes in the graph into a number of disjointed components (for all nodes are all connected in the same component). There may be one or more disjointed components in an undirected graph.
- running DFS on a source node and target node will let us determine if src node is connected to target, and return as soon as target is found (can also build the path from src to target this way), OR when all nodes connected to src are visited and did not find the target node.
