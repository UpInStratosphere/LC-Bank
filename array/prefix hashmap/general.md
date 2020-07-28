Typically involves using each number as an end of the current subarray
- there is a cumulatve counter that is used to store the entire subarray from the start to the current i element
- for each of the prev number as end, the counter for that subarray is saved in a hashmap
- for each curr number as the end, all the subarrays for that number as the end can be implicitly calculated by using the current cumulative counter - each of the saved counter in the hashmap
- **each next number will form i+1 new subarrays** 
