- treat total sum pair as a cartesian sum matrix: row = first num in pair, column = second num in pair
  - each row's num is the sorted list1, and each col's num is the sorted list2
  - each row's element (pair sum) is sorted because the column number is increasing from left to right 
  - each col's element (pair sum) is also sorted because the row number is increasing from top to bottom


```cpp
struct Compare {
    //tuples : [nums1[i], nums2[j], and j] so we can use j to determine the number to be added into the heap
    bool operator()(tuple<int, int, int>& t1, tuple<int, int, int>& t2) {
        return ((get<0>(t1) + get<1>(t1)) > (get<0>(t2) + get<1>(t2)));
    }
};
    
vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
    vector<vector<int>> res;

    if(nums1.size() == 0 || nums2.size() == 0 || k == 0) return res;

    priority_queue<tuple<int, int, int>, vector<tuple<int, int, int> >, Compare> min_heap;

    int limit = min((int)nums1.size(), k);
  
    for(int i = 0; i < limit; i++) 
        min_heap.push(make_tuple(nums1[i], nums2[0], 0));

    while(!min_heap.empty()) {
        tuple<int, int, int> top = min_heap.top();
        min_heap.pop();
        res.push_back({get<0>(top), get<1>(top)});
        if (res.size() == k) 
            return res;
        if(get<2>(top) + 1 < nums2.size())
            min_heap.push(make_tuple(get<0>(top), nums2[get<2>(top)+1], get<2>(top)+1));
    }
    return res;
}
```
