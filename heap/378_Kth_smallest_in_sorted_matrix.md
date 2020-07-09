- since all rows's elements are sorted, and all columns are sorted, that means the each row can be treated as a sorted sequence, and can use min heap to extra K smallest out of all .
    - the sorted columns ensures the fact that if K < total rows, then we don't need to push all the row's first num into the heap.
    - time : if X = min(K, rows), X + KlogX

```cpp
class Solution {
private:
    //create a min heap that contains K smallest and the heap top is smallest
    struct comp{
        bool operator()(const pair<int, pair<int, int>> &x, const pair<int, pair<int, int>>&y) {
            return x.first > y.first; //bigger number has higher priority 
        }
    };
    
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        int rows = matrix.size(), cols = matrix[0].size();
        priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, comp> minHeap;
        
        for (int i = 0; i < rows; i++) 
            minHeap.push({matrix[i][0], {i, 0}}); //[value : rows : col]
        
        int count = 0;
        while (!minHeap.empty()) {
            auto curr = minHeap.top();
            int val = curr.first, row = curr.second.first, col = curr.second.second;
            minHeap.pop();
            count++;
            if (count == k)
                return val;
            
            col++; //push in the next num after current in the row if possible
            if (col < cols) {
                minHeap.push({matrix[row][col], {row, col}});
            }
        }
        return -1; //never reach here if k <= n
     }
};
```
