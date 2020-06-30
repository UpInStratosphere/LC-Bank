- Using **pre-order traversal with a leaf node check** for each node visited, we are guaranteed to visit each leaf node from the left to right. In other words, we will visit each path (from root to leaf node) systematically from left to right.
    - as long as the current node is not a leaf node, we will continue to travel to its children nodes
    - because for each leaf node we visit, we will assess the path then return that function.
- Because we will need to visit ALL paths, we need to use a parameter to store the data for each path, and another parameter to store the global answer.

```cpp
int maxDepth(TreeNode* root) {
    if (!root) return 0;
    int res = 0;
    DFS(root, 0, res); //one parameter to track current path, and one is used to store the global answer 
    return res;
}

void DFS(TreeNode *node, int curr, int &res){
    if (!node) return;
    curr++;
    if (!node->left && !node->right){
        res = max(res, curr);
        return;
    }
    DFS(node->left, curr, res);
    DFS(node->right, curr, res);
}
```
