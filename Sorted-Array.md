# SORTED - ARRAY 

```cpp
class Solution {
public:
    TreeNode* build(vector<int>& nums ,int l , int r) {
        if (l > r) return NULL ;
        int mid = (l + r)/2 ;

        TreeNode* node = new TreeNode( nums[mid] ) ;
        node->left = build(nums ,l , mid - 1 );
        node->right = build(nums , mid + 1 , r );
        return node ;
    }
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        int n = nums.size();
        
        return build(nums ,0, n-1) ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N)    |   All elements are processed at max once |
| 🧠 SPACE |   O(logN)    | Recursion stack depth equals tree height, which is log N for a balanced BST |

