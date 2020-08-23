- How to represent the current problem with initial parameters
    - this determines the subproblems' parameters 
- At the function for the current problem, how does the current problem relate to the smaller subproblems
    - subproblem's parameters depends on the form of the initial problem's parameter
    - usually for the intermediate problem / curr function, there are multi-branched recursion on subproblems
- for a recursive problem to be DP problem, many different combination of the upper functions (upper level nodes conenctions) will arrive at the duplicate subproblems (lower level nodes in a DAG). 
    - Recursion solves the smaller problems first before using them to solve bigger problems, cache them.
- How to "combine" the answers from subproblems to find the answer for the current level

