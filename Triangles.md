#118/119/120 Pascal's Triangle I/II/Triangle
- logic
	- All 3 problems can be thought as DP problems. The triangles created in these problems can be thought as below:
		i = 0 [1]  j = 0
		i = 1 [1][1]  j = 1
		i = 2 [1][2][1]  j = 2
		i = 3 [1][3][3][1]  j =3 
	- Each row is a different vector indicated by i, and j is the column associated with each row.
	- How to get the value for each element: vector[i][j] = vector[i-1][j-1] + vector[i-1][j]
		
- code sample below
```cpp

	
		


