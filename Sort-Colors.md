# SORT-COLORS 
```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        // Dutch National Flag Algo 
        int n = nums.size();
        int low = 0 , mid = 0 , high = n-1 ;
        
        while (mid <= high) {
            if (nums[mid] == 0) {
                swap(nums[mid] , nums[low]) ;
                low++ ;
                mid++ ;
            }else if (nums[mid] == 2) {
                swap(nums[mid] , nums[high]) ;
                high-- ;
            }else{
                mid++ ;
            }
        }
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |       O(N)    |  Single Traversal     |
| 🧠 SPACE |     O(1)       |    No extra space       |
