
- compare each string pair and update the longest prefix as the longest matching substring of each pair
- longest prefix is also how strings are sorted: it is determined by the first unmatching char of the string pair
- the longest prefix is also bounded by the length of the shortest string 

```cpp 
    string longestCommonPrefix(vector<string>& strs) {
        //match each string pair and keep the max matching substring
        if (strs.empty()) return "";
        string res = strs[0];
        int n = strs.size();
        for (int i = 1; i < n; i++){
            int len = min(res.size(), strs[i].size());
            int index = -1;
            //stop at the first mismatch chars btw the two strings and that is the new result 
            for (int j = 0; j < len; j++){
                if (strs[i][j] == res[j]){
                    index+=1;
                }
                else
                    break;
            }
            res = res.substr(0, index+1); //length = index-0+1
        }
        return res;
    }
    ```
