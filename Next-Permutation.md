# NEXT PERMUTATION 

- INTUITION  : Next permutation can be formed by swapping the rightmost such pair so that we have nums[i] , nums[j] where i < j & nums[i] > nums[j] .
- Here ie in the pair greater element appears before and smaller afterwards (i < j) , and the smallest such i index should be the rightmost possible to ensure we get just the nextgreater permut ,
- After swapping keep in mind since the smaller element is on right so the right part should be in sorted order so that to keep is the smallest possible permutation & next to the given nums

```cpp
class Solution {
public:
    void nextPermutation(vector<int>& nums) {
        int n = nums.size();
        int i = n-1 ;
        while (i > 0) {
            if (nums[i] > nums[i-1]) break ; // rightMost pair
            i-- ;
        }
        if (i == 0) {// complete nums in descending order
            reverse(nums.begin() , nums.end());
            return ;
        }
        int j = n-1 ;
        for (j ; j >= i ; j--) {
            if (nums[j] > nums[i-1]) break;
        }
        swap(nums[i-1] , nums[j]);
        reverse(nums.begin() + i , nums.end());
        
        return ;
    }
};
```


# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N)        |  Traversing the nums array         |
| 🧠 SPACE | O(1)    | No extra space used . |
