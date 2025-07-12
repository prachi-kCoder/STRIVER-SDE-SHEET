# 3 SUM {TRIPLET}

```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        if (n < 3) return {} ;
        int mn = *min_element(nums.begin() , nums.end());
        if (mn > 0) return {} ;
        vector<vector<int>> res ;
        
        sort(nums.begin() , nums.end()) ;
        int l = 0 , r = n-1 ;
        for (int i = 0; i < n-2 ; i++) {  
            if (nums[i] > 0) break ;// smallest can't be +ve 
            if (i > 0 && nums[i] == nums[i-1]) continue ;

            int l = i+1 ; int r = n-1 ;
            while (l < r) {
                int sum = nums[i] + nums[l] + nums[r] ;
                if (sum > 0) {// positive sum so look so more -ve values towards left 
                    r-- ;
                }else if (sum < 0) { // -ve sum so look for +ve values towards right
                    l++ ;
                }else {
                    res.push_back({nums[i] , nums[l] , nums[r]});

                    int prev_left = nums[l] ;
                    int prev_right = nums[r] ;
                    while (l < n-1 && nums[l] == prev_left) l++ ;
                    while (r > l && nums[r] == prev_right) r-- ;
                }
            }
        }
        
        return res ;
    }
```
## COMPLEXICITY ANALYSIS 
| METRIC   |  COMPLEXICITY    |   HOW ?  | 
|----------|-------------------|----------|
|   TIME   |    O(nlogn + n*n)  | SORTING + 2 Pointer : In total, across all n - iterations, the two-pointer method ensures that each element is visited at most once per i. So the inner loop runs at most O(n) times for each outer i, but NOT O(n^2) overall |
| SPACE    |    O(K)     |  k Traiplets in res |
