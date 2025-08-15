## Largest Rectangle Histogram

#### APPROACH 1 : 
- Left Smaller Ht index , Right Smaller Ht index
- Take the width , currHt (which is the decider height for the ith index)

```cpp
class Solution {
public:
    vector<int> get_left_smallest(vector<int>& hts) {
        int n = hts.size();
        vector<int> ls(n, -1) ;
        stack<int> stk ;
        for (int i = 0; i < n ; i++) {
            while (!stk.empty() && hts[stk.top()] >= hts[i] ) {
                stk.pop();
            }
            if (!stk.empty()) {
                ls[i] = stk.top();
            }
            stk.push(i) ;
        }
        return ls ;
    }
    vector<int> get_right_smallest(vector<int>& hts) {
        int n = hts.size();
        vector<int> rs(n, n) ;
        stack<int> stk ;
        for (int i = n-1 ; i >= 0 ; i-- ) {
            while (!stk.empty() && hts[stk.top()] >= hts[i] ) {
                stk.pop();
            }
            if (!stk.empty()) {
                rs[i] = stk.top();
            }
            stk.push(i) ;
        }
        return rs ;
    }
    int largestRectangleArea(vector<int>& heights) {
        int n = heights.size();
        vector<int> ls = get_left_smallest(heights) ;
        vector<int> rs = get_right_smallest(heights) ;

        int mx_area = 0 ;
        for (int i = 0 ; i < n ; i++ ) {
            int w = rs[i] - ls[i] - 1 ;
            int h = heights[i] ; // ith height
            mx_area = max(mx_area , w*h);
        }

        return mx_area ;
    }
};
```

