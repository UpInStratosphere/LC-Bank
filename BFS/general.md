Queues hold all the valid shortest nodes from each level 
- if an node is visited for the first time, this is via the shortest path from the source node
- if a node is visited again: the duplicate visit does not help with the shortest path because the node was already visited
    - EITHER via a node at an upper level (already visited via shortest path)
    - OR via an earlier node at the current level (meaning there are more than 1 shortest path to that node)
