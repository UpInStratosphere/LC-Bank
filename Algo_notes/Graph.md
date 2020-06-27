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
    unordered_map<string,string>parent; // all valid nodes -> end root
    unordered_map<string,int>rank;   // all valid nodes -> rank
    int components;
public:
    //if nodes given, use below
    DSU(unordered_set<string>nodes){ //initialize for each node appeared in the given data
        for (auto node : nodes){
            parent[node] = node;
            rank[node] = 0;
        }
        components = nodes.size();
    };
    
    //if not given, then process each edge separately.
    DSU(){
        parent = {};
        rank = {};
        components = 0;
    };
    
    //finding the root of the node
    int find(int x){
        if (parent[x] != x)
            parent[x] = find(parent[x]);
        return parent[x];
    }
    
    
    //Add a new node into the graph
    bool setParent(int x){
        if (parent.find(x) != parent.end()) return false;
        parent[x] = x;
        rank[x] = 0;
        components++;
        return true;
    }
    
    //combine the sets if they are not in the same component.
     bool merge(int x, int y){
        int rootx = find(x);
        int rooty = find(y);
        
        if (rootx == rooty) return false; //in the same component, no need to merge
        
        if (rank[rootx] > rank[rooty])
            parent[rooty] = rootx;
        else if (rank[rootx] < rank[rooty])
            parent[rootx] = rooty;
        else{
            parent[rooty] = rootx;
            rank[rootx]++;
        }
        components--;
        return true; //two components are merged into one, decrease total component count by 1
    }
    
    int getCount(){ //use a class getter function to return the total count
        return components;
    }
};
```






