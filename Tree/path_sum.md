- each recursive function will return whether the current node will lead to a path that has the target sum.
- each node depends on the answer from the function returned from either its left child or right child node path.
- a parameter is needed to store the current path sum.

```cpp
bool hasPathSum(TreeNode* root, int sum) {
        if (!root) return false;
        return DFS(root, sum);
    }
    
//check the curr path validity state at the end of the path (leaf node)
bool DFS(TreeNode *node, int sum){
    if (!node) return false; 

    sum -= node->val;
    if (!node->left && !node->right)
        return sum == 0;

    //just need one of the children nodes to lead a valid path
    if (DFS(node->left, sum)) return true;
    if (DFS(node->right, sum)) return true;

    return false;

}
```

```cpp
vector<vector<int>> pathSum2(TreeNode* root, int sum) {
        if (!root) return vector<vector<int>>{};
        vector<vector<int>>res;
        vector<int>curr;
        build(root, sum, curr, res);
        return res;
    }
    
    //target tracks the value of the current path with the current node included
    void build(TreeNode *node, int target, vector<int>&curr, vector<vector<int>>&res){
        if (!node) return;
        
        target -= node->val; 
        curr.push_back(node->val);
        
        //if a leaf node, need to terminate the function at the current node regardless if the current path is valid 
        if (!node->left && !node->right){
            if (target == 0){
                res.push_back(curr);
            }
        }
        //if not a leaf node, keep traversing down. When the left child returns, the curr path is already reset
        else{
            build(node->left, target, curr, res);
            build(node->right, target, curr, res);
        }
        
        //wipe the slate clean for the current node
        curr.pop_back(); 
    }
```
