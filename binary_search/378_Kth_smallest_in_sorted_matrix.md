Use Binary Search to get the hypothetical mid and track how many cells are <= this value.
- hardest explain is why set ans to actual mid when count > K
    - when actual mid value is a duplicate value, and the next smaller is too small, and next larger is too big
    - [1,2][1,3], k = 1, 

```cpp
int kthSmallest(vector<vector<int>>& matrix, int k) {
    int res = matrix[0][0];
    int rows = matrix.size(), cols = matrix[0].size();
    int left = matrix[0][0], right = matrix[rows-1][cols-1]; //min and max 
    while (left <= right){
        int mid = left + (right-left)/2;
        int numsSmaller = 0, actualMid = matrix[0][0]; //the closest actual value <= hypothetical mid
        for (int i = 0; i < rows; i++){
            for (int j = 0; j < cols; j++){
                if (matrix[i][j] <= mid){
                    numsSmaller+=1;
                    actualMid = max(maxLeft, matrix[i][j]);  
                }
            }
        }
        if (numsSmaller == k)
            return actualMid;
        else if (numsSmaller > k){ // Actual mid could be a candidate if it is a repeated value
            res = ActualMid;
            right = mid-1;
        }
        else 
            left = mid+1;   
    }
    return res;
}
```
