# CONSTRURCT BST FROM PREORDER

#### SIMPLE INTUITION  : As while forming a BST we look for the root and the par of the root to make decision about the max & minVal in subtree , ie how we can solve thie
- For any node to be in left subtree the max Val = rootVal - 1 ;
- For any node to be in right subtree the min Val = rootVal + 1 ;
```cpp
TreeNode* build( int& i , vector<int>& preorder, int minVal , int maxVal ) {
        if (i >= preorder.size()) return nullptr ;
        int currVal = preorder[i] ;
        if (currVal < minVal || currVal > maxVal) return nullptr ;
        TreeNode* node = new TreeNode(currVal) ;
        i++ ;

        node->left = build(i , preorder , minVal , currVal-1) ;
        node->right = build(i , preorder , currVal + 1 , maxVal );
        return node ;
    }
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        int n = preorder.size() ;
        if (n == 0) return nullptr ;

        int i = 0 ;
        return build(  i ,  preorder , INT_MIN , INT_MAX );        
    }
```

- Min–max range constrains ensure that at every step, the value fits the BST rules without backtracking.
# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(n)     |   Traverse all nodes of preOrder       |
| 🧠 SPACE |   O(H)      | H-> Recursion Stack Height , & For Worst Case : O(h) = O(n) for Skewed Tree      |
