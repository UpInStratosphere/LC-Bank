- since each rows's elements are sorted, that means if we continually pull out K smallest elements from the min heap and add the next one, we will get the Kth smallest.
    - the sorted columns only ensures if K < total rows, then we don't need to push all the row's first num into the heap. Not a big optimization
    - time : if X = min(K, rows), X + KlogX
    - Note: for each current number, consider this number as the top-left num of a rectangle - all numbers in the rectangle are bigger than the current number. Therefore, when considering the next global smallest number, none of those numbers can be added into the heap until the current number is popped from the heap.
    
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
            minHeap.pop();
            int val = curr.first;
            int row = curr.second.first, col = curr.second.second;
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
