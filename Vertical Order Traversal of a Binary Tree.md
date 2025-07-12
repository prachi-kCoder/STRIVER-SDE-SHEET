# Vertical Order Traversal of a Binary Tree

## INTUITION  : 
- Core Idea
Traverse the tree using DFS (preOrder traversal) while recording:
-Column index: to group vertical slices.
-Row index: to preserve top-to-bottom ordering.
-Node value: to resolve tie-breaking.

### Use a min-heap (priority queue) to sort nodes first by column, then by row, then by value.
- Process the queue and group nodes column-wise.

## VERY IMPORT DIFFERENCE TO KEEP IN MIND  : 
|   Context	  | Meaning of < / >	 | Interpretation  |
|-------------|--------------------|------------------|
|  std::sort()|< means "comes before"	| Sort in ascending order by default |
| priority_queue| < means "lower priority"| So larger elements come first |

Hence for minHeap we say a.first > b.first to make a minHeap  {To get more priority to lower values}
Effectively, you're creating a min-heap behavior inside the max-heap structure by reversing logic.

## compare comparator :
```cpp
if (a.first == b.first) { // equals cols
    if (a.second.first == b.second.first) { // equal row
        return a.second.second > b.second.second; // if same row , col  then smaller val is given priority
    }
    return a.second.first > b.second.first; // smaller col given priority
}
return a.first > b.first;
\
```


## CODE :
```cpp
class Solution {
public:
    struct compare{
        bool operator()(const pair<int,pair<int,int>>& a, const pair<int,pair<int,int>>& b) {
            if (a.first == b.first) { // same col
                auto ab = a.second ; auto cb = b.second ;
                // same row
                return ab.first == cb.first ? ab.second > cb.second : ab.first > cb.first ;
            }else {
                return  a.first > b.first ;
            }
        }
    };
    void preOrder(TreeNode* root , int row , int col,  priority_queue<pair<int,pair<int,int>>, vector<pair<int,pair<int,int>>>,compare>& pq ) {
        if (root == nullptr) return ;

        pq.push({col , {row , root->val}});
        preOrder(root->left , row+1 , col-1, pq);
        preOrder(root->right , row+1 , col+1, pq);
    }
    vector<vector<int>> verticalTraversal(TreeNode* root) {
        // BFS 
        vector<vector<int>> res ;
        if (root == nullptr) return res ;
        priority_queue<pair<int,pair<int,int>>, vector<pair<int,pair<int,int>>>,compare> pq ;

        preOrder(root , 0 , 0, pq) ;
        while (!pq.empty()) {
            int col = pq.top().first ;

            vector<int> nodes ;
            while (!pq.empty() && pq.top().first == col) {
                auto p = pq.top().second ;
                nodes.push_back({ p.second }) ;
                pq.pop() ;
            }
            res.push_back(nodes) ;
        }
        return res ;
    }
};
```

# COMPLEXICIT ANALYSIS  
|  METRIC  |  COMPLEXICITY  | HOW ? | 
| TIME     |  O(2*n*logn)   | n nodes -> Insertion and Deletion from PQ |
| SPACE    |  O(3*n)        | n nodes values , row, col in  PQ |
