- All rows are sorted and we need to retrieve the smallest out of all rows. So we can use K-way merge to keep a rows-sized min heap, for which it stores the min num of each list. And extract K nums from the list. 
- For each element stored in heap, it must have its row and col index attached, so we know the next number to be added.
- Time : Klog(rows).  Space : rows

```cpp

struct numCompare{
  bool operator()(const pair<int, pair<int, int>> &x, const pair<int, pair<int, int>>&y) {
      return x.first > y.first;  
  }
};

int kthSmallest(vector<vector<int>>& matrix, int k) {
  int rows = matrix.size(), cols = matrix[0].size();
  priority_queue<pair<int, pair<int, int>>, vector<pair<int, pair<int, int>>>, numCompare> minHeap;
  for (int i = 0; i < rows; i++) 
    minHeap.push({matrix[i][0], {i, 0}});  // [value : [rows:col]]

  int count = 0;
  while (!minHeap.empty()) {
      auto curr = minHeap.top();
      int val = curr.first, row = curr.second.first, col = curr.second.second;
      minHeap.pop();
      count++;
      if (count == k)
          return val;
      col++; //if next num is within the index then it is added into the heap
      if (col < cols) {
          minHeap.push({matrix[row][col], {row, col}});
      }
  }
  return -1; //if here, then the number of total elements in matrix is less than K
}
```

