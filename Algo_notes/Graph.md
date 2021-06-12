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
    //constructors
    
    //if nodes given, use below
    DSU(unordered_set<type>nodes){ //initialize for each node appeared in the given data
        for (auto node : nodes) 
            createNode(node);
    };
    
    //if not given, then build DSU on the fly while processing each edge
    DSU(){
        parent = {};
        rank = {};
        components = 0;
    };
    
    
    //find if a node exists in the set
    bool findNode(int x){
        if (parent.find(x) != parent.end()) return true;
        return false;
    }
    
    //create new node in the component if it doesnt exist 
    void createNode(int x){ //O(1)
        if (findNode(x)) return;
        parent[x] = x;
        rank[x] = 0;
        components++;
    }
    
    //find the identity of the group that the node belongs
    //path compression: standardization that updates and fix any inconsistency of all nodes in the set
    int findParent(int x){
        if (parent[x] != x) parent[x] = findParent(parent[x]);
        return parent[x];
    }
    
    //merge nodes if they are in separate sets. do nothing already in the same set. 
    //merge does not standardize all nodes of the new set, only changing the rep of the merging group into the merged group
    //all nodes in the merging group besides the rep still have their old info (inconsistency still exist)  
    bool merge(int x, int y){ //O(log*(V))
        type rootx = findParent(x); 
        type rooty = findParent(y);
        
        if (rootx == rooty) return false;
        
        //merge two groups by reseting the info of rep node of the merging set to the info of the rep node of the merged set 
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
    
    
    //component information
    
    int getCount(){ //O(1)
        return components;
    }
    
    int getMaxComponent(){ //Amortized this is O(Vlog*(V)), so O(V).
        int ans = 0;
        unordered_map<int,int>freq; 
        for (auto node_rank: parent){
            int node = node_rank.first;
            int root = findParent(node); //used to fix the inconsistency of all the nodes that were left behind after merging
            freq[root]++;
            ans = max(ans, freq[root]);
        }
        return ans;
    }
};
```






