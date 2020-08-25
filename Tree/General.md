For each subtree, the answer for that subtree usually depends on:
- the results from both children subtrees AND
- the root value or the values of all the nodes in the current tree
- because results from subtrees are necessary, to get their results, we usually need to call the function recursively.

The subtree's answers don't need to be cached in a memo hashset even if we use postorder (classic recursion) where each tree's answer depends on its subtree's answers 
- Use local variables to save each subtree's answers in the current function (Because we only needs to access the curr tree's immediate subtrees, not every single subtree below). Therefore, no need to cache each already processed subtree's answers.

Difference with DP(DAG) problems
- each upper node (bigger subproblems) may lead to any of the lower nodes (not just immediate lower level nodes, could be either already calculated or visiting for the first time), hence need to store all the calculated lower level nodes so they dont have to be re-calculated each time their answers are needed.
