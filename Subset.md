# SUBSET

### APPROACH-1 BITMASKING 
- Subset masks can be created from  (0,(1<<n)) 
```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ans ;
        int n = nums.size() ;

        for (int mask = 0 ;  mask< (1<<n) ; mask++) {
            vector<int> s ;
            for (int i = 0; i <n ; i++) {
                if (mask&(1<<i)){
                    s.push_back(nums[i]);
                }
            }
            ans.push_back(s) ;
        }
        return ans ;
    }
};
```

### APPROACH-2 BACKTRACKING {DFS}
```cpp
void solve(int i , vector<int>& curr , vector<int>& nums, vector<vector<int>>& ans) {
        if ( i >= nums.size()) {
            ans.push_back(curr) ;
            return ;
        }

        curr.push_back(nums[i]) ;
        solve(i+1 , curr , nums , ans) ;
        curr.pop_back();
        solve(i+1 , curr , nums , ans) ;
    }
vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> ans ;
        int n = nums.size() ;
        vector<int> curr ;
        solve(0 , curr , nums , ans ) ;
         return ans ;
    }
```


## 🔍COMPLEXICITY ANALYSIS
- ✅ `Bitmasking`
| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |      O(2^n * n)      | There are 2^𝑛 masks, and each mask takes up to n time to construct the subset.  |
| 🧠 SPACE |    O(2^N * N)     | To store subsets  |

- `BACKTRACKING - DFS`
| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |      O(2^n * n)  | Each element has two choices (include/exclude), leading to 2^𝑛 recursive paths. Each path builds a subset of up to 𝑛 elements. |
| 🧠 SPACE |    O(2^N * N)     | To store subsets(2^N) with each subset of O(n) {space for full subset} + Recusiong Stack , Curr Array |
