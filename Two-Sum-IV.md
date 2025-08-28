# TWO-SUM-IV

```cpp
class BSTIterator {
public :
    bool is_left ;
    stack<TreeNode*> stk ;
    BSTIterator(TreeNode* node , bool is_left) {
        this->is_left = is_left ;
        push_all(node) ;
    }
    int next() {
        TreeNode* node  = stk.top() ; stk.pop();
        int val = node->val ;
        if (is_left) {
            push_all(node->right) ;
        } else push_all(node->left) ;

        return val ;
    }

private :
    void push_all(TreeNode* node) {
        while (node) {
            stk.push(node);
            node = (is_left) ? node->left : node->right ;
        }
    }
};
class Solution {
public:

    bool findTarget(TreeNode* root, int k) {
        BSTIterator l(root , true); // left it
        BSTIterator r(root , false); // right it
        int i = l.next() ;
        int j = r.next() ;

        while (i < j) {
            int sum = i+j ;
            if (sum == k) return true ;
            if (sum < k) {
                i = l.next();
            }else {
                j = r.next();
            }
        }
        return false ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N)      |  As in worst case the 2 pointer may need to visite all nodes |
| 🧠 SPACE |     O(H)     |   Each iterator maintains a stack of height H, where H is the tree’s height   |

