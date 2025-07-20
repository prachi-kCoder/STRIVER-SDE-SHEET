## DIAMETER OF BINARY TREE

```cpp
class Solution {
public:
    pair<int,int> find(TreeNode* node) {
        if (!node) return {0,0} ;
        // lD / rD / self D
        auto lp = find(node->left) ;
        int lDia = lp.first ; int lHt = lp.second ;

        auto rp = find(node->right) ;
        int rDia = rp.first ; int rHt = rp.second ;
        int selfDia = lHt + rHt + 1 ;

        return {max({selfDia , lDia , rDia}) , 1 + max(lHt , rHt)};
    }
    int diameterOfBinaryTree(TreeNode* root) {
        if (!root) return 0 ;

        auto p = find(root) ;
        return p.first -1  ;
    }
};
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N)         |  All tree n nodes traversed during post order traversal. |
| 🧠 SPACE |    O(H)  | Recursion Stack Height of H {In worst case of Skewed Trees O(N)= O(H)} |

