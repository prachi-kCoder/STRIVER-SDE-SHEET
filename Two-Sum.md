# TWO-SUM 
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int n = nums.size();
        unordered_map<int,int> mp ;
        
        for ( int i = 0 ; i < n ; i++) {
            int e2 = target - nums[i];
            if (mp.find(e2) != mp.end()) return {i , mp[e2]} ;
            mp[nums[i]]= i;
        }
        return vector<int>();
    }
};
```

## 🔧  COMPLEXICITY ANALYSIS
| METRIC   | COMPLEXICITY   |  HOW ?  |
|----------|----------------|---------|
| TIME     |   O(N)         |  single pass |
| SPACE     |   O(N)         |  HashMap |
