## nodes && edges properties
- symmetric : symmetric indicates undirected graph. 
- transitive : nodes can traverse through its neighbors and go to other connected nodes
- directed vs indirected graph (when building the graph using the edges given) :
    - for indirected graph, need to add to both nodes
    - for directed graph, just need to add for the src node
- weighted vs. unweighted
    - save the weight with the sink node 

## DFS
- DFS will keep traverse down a path until the current node's has no more unprocessed neighbor nodes. Path will go down whenever possible, only comes back and explore next neighbor once all of the previous neighbor's paths are finished.
    - the different paths will be explored from bottom up.
    
- running DFS on all nodes in a graph will visit each nodes only once, and can group the nodes into disjointed components. There may be one or more disjointed components in an undirected graph.
    - whenever the current visiting node is marked as visited, it means it is already placed in the current component OR been put in a prior component. The point is that the current node is already processed and should not processed again BECAUSE the function that processed the current node the first time will process all of the current node's neighbors.
    
- running DFS on a source node and target node will let us determine if src node is connected to target(whether two are in the same connected component).
    - return as soon as target is found (can also build the path from src to target backwards as we return in each function), OR 
    - return when all nodes that are connected to src are visited and did not find the target node.
    
## BFS
- used to find the shortest path between two nodes in a graph
- a visited graph is also used. If a neighbor node is marked as visited, then it is either visited in a shorter path or visited previously in the same level. 



## Union Find

```cpp
class DSU {
private:
    unordered_map<type,type>parent; // all valid nodes -> end root
    unordered_map<type,int>rank;   // all valid nodes -> rank
    int components;

public:
    //if nodes given, use below
    DSU(unordered_set<type>nodes){ //initialize for each node appeared in the given data
        for (auto node : nodes){
            parent[node] = node;
            rank[node] = 0;
        }
        components = nodes.size();
    };
    
    //if not given, then build DSU on the fly while processing each edge
    DSU(){
        parent = {};
        rank = {};
        components = 0;
    };
    
    //if node not in graph, create a new set for each node in the edge and return true
    //if node already in graph, does nothing and return false
    bool setParent(int x){
        if (parent.find(x) != parent.end()) return false;
        parent[x] = x;
        rank[x] = 0;
        components++;
        return true;
    }
    
    //finding the overall root of the curr node. This depends on the graph already has the node
    type findParent(int x){
        //if (parent.find(x) == parent.end()) return INT_MIN;
        if (parent[x] != x)
            parent[x] = findParent(parent[x]);
        return parent[x];
    }
    
    //merge sets and return true if they are in separate sets. do nothing and return false if they are in the same set already.
     bool merge(int x, int y){
        type rootx = findParent(x);
        type rooty = findParent(y);
        
        if (rootx == rooty) return false;
        
        if (rank[rootx] > rank[rooty])
            parent[rooty] = rootx;
        else if (rank[rootx] < rank[rooty])
            parent[rootx] = rooty;
        else{
            parent[rooty] = rootx;
            rank[rootx]++;
        }
        components--;
        return true; 
    }
    
    int getCount(){ //use a class getter function to return the total count
        return components;
    }
    
    
    int getMax(){ //use a class getter function to return the max component
        int ans = 0;
        unordered_map<int,int>freq;
        for (auto node_rank: parent){
            int node = node_rank.first;
            int root = findParent(node);
            cout << root << endl;
            freq[root]++;
            ans = max(ans, freq[root]);
        }
        return ans;
    }


    //for matrix only : if the neighbor cell is out of bound, or NOT YET visited as a valid node
    bool isValid(int m, int n, int x, int y){
        if (x < 0 || x >= m || y < 0 || y >= n || findParent(x*n+y) == INT_MIN) return false;
        return true;
    }
};
```






