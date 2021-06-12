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
    
    
    //single node check/creation
    
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
    
    //core operation: find/merge
    //path compression for merging: Olog*(V)
    //finds and updates all the group's nodes parent to the same node.
    int findParent(int x){
        if (parent.find(x) == parent.end()) return INT_MIN; //doesn't exist in the graph
        if (parent[x] != x) 
            parent[x] = findParent(parent[x]);
        return parent[x];
    }
    
    //merge nodes if they are in separate sets. do nothing already in the same set. O(Log*(V))
    //merge sets by changing the rep of one group to the rep of the other group's rep. 
    //But doesn't necessarily align all the merged set's node's rep to the same rep. 
    //components are updated, but not all the nodes in the merged set will have the same parent via merge function alone 
    //parents hashmap doesn't reflect the group status 
    bool merge(int x, int y){ //O(log*(V))
        type rootx = findParent(x);
        type rooty = findParent(y);
        
        if (rootx == rooty) return false;
        
        //only reset the parent node for the set's rep node
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
    
    int getMax(){ //Amortized this is O(Vlog*(V)), so O(V).
        int ans = 0;
        unordered_map<int,int>freq; 
        for (auto node_rank: parent){
            int node = node_rank.first;
            int root = findParent(node); //used to fix the parents hashmap to reflect the component state
            freq[root]++;
            ans = max(ans, freq[root]);
        }
        return ans;
    }
};
```






