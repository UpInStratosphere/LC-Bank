#118/119/120 Pascal's Triangle I/II/Triangle
- logic
	- All 3 problems can be thought as DP problems. The triangles created in these problems can be thought as below:
		i = 0 [1]  j = 0
		i = 1 [1][1]  j = 1
		i = 2 [1][2][1]  j = 2
		i = 3 [1][3][3][1]  j =3 
	- Each row is a different vector indicated by i, and j is the column associated with each row.
	- How to get the value for each element: vector[i][j] = vector[i-1][j-1] + vector[i-1][j]. Each of the current element is the sum of the vector[top][left col] + vector[top][curr col] 
    - A more intuitive way to write the code is to divide into 2 scenarios, whenever the current element is the first, last, or in the middle of its row.
  - If we are trying to minimize space and use a single vector to store both the previous row's value and current row's elements and re-using the previous elements vectors values to get the current row's elements value, we have to update the value backwards, **from the end to the front**. Because each of the current row's elements depends on the previous row's left value, so we want to preserve the previous row's original left element value UNTIL we are done with it, which is whenever we are done updating the current element
		
- code below
  - Pascal's triangle 
  ```cpp
  class Solution {
  public:
      vector<vector<int>> generate(int numRows) {
          vector<vector<int>>res;
          if (numRows <= 0) return res;
          vector<int>temp{1};
          res.push_back(temp);
          for (int i = 1; i < numRows; i++){ //construct rows starting from the first index row
              vector<int>curr; int num = 0;
              for (int j = 0; j <= i; j++){ //if we are using one vector to store previous row's values, then we can construct the current row's values from the left to the right
                  if (j == 0) curr.push_back(1);
                  else if (j == i) curr.push_back(1);
                  else{
                      num = temp[j-1] + temp[j];
                      curr.push_back(num);
                  }
              }
              res.push_back(curr);
              temp = curr;
          }
          return res;
      }
  };
  ```
  - Pascal's Triangle II
  ```cpp
  class Solution {
  public:
    vector<int> getRow(int rowIndex) {
        vector<int>ans(rowIndex+1,0);
        ans[0] = 1;
        for (int i = 1; i <=rowIndex; i++){ 
            for (int j = i; j >=0; j--){ //build the current values from the end to the front because we need the original upper left element's value to derive the current element's value. 
                if (j == i) ans[j] = 1;
                else if (j == 0) ans[j] = 1;
                else ans[j] += ans[j-1];
            }
        }
        return ans;
    }
  };
  ```
  - Triangle 
  ```cpp
  class Solution {
  public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n = triangle.size();
        vector<int>res(triangle[n-1].size(), triangle[0][0]); 
        for (int i = 1; i < n; i++){ 
            for (int j = i; j >= 0; j--) { //similar to above, since we are using one vector to store the previous row's value and current row's value. We need to maintain the previous row's left value until we are done with it 
                if (j == 0) 
                    res[0] += triangle[i][j];
                else if (j == i) 
                    res[j] = triangle[i][j] + res[j-1];
                else            
                    res[j] = triangle[i][j] + min(res[j-1], res[j]); 
            }
        }
        int ans = INT_MAX;
        for (int i = 0; i < res.size(); i++)
            ans = min(ans, res[i]);
        return ans;
    }
  };
  ```


	
		


