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
## APPROACH 2 : MONOTONIC STACK 
- Here also the intuition is same ie we need left smaller and right smaller but here we won't precompute them rather we will keep track of them in the single pass using (Monotonic stack)
- Monotonic increasing heights ensures if on the left the heights are going to be smaller as left smaller can be traced and for every left smaller the max area on the smaller ht in monotonic stack can be computed well .
- As soon as monotonicity breaks , ie heights[i] < heights[stk.top()] so the rightSmaller height is reached and until we have heights [stk.top()] > height[i] (ith index where monotonicity broke !) we will calculate the areas for all heights and then with rest of hts < hts[i] , we move on to keep monotonic stack !

```cpp
int largestRectangleArea(vector<int>& hts) {
        // Monotonic Stack
        hts.push_back(0) ;// last set of increasing ht to be checked 
        int n = hts.size();
        int mx_area = 0 ;
        stack<int> stk ;
        
        for (int i = 0; i < n ; i++) {
            while (!stk.empty() && hts[stk.top()] > hts[i]) { // right smaller ht found
                int h = hts[stk.top()] ;
                stk.pop();
                int w = stk.empty() ? i : i - stk.top() - 1 ;
                mx_area = max(mx_area , w*h);
            }
            stk.push(i) ;
        }   
    return mx_area ;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC   | 📈 COMPLEXITY | 🧩 EXPLANATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N)    |  Single pass , every element will go inside the stack at max once  keeping the complexicity linear (Each ele is process while iteration and once while stack operation .pop())  |
| 🧠 SPACE |    O(N)         |  In the worst case (e.g., strictly increasing heights), all elements may be in the stack simultaneously. Hence, space usage is linear due to the stack.  |
