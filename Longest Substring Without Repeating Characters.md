# Longest Substring Without Repeating Characters

## INTUITION : SLIDING WINDOW  , Keep track of the last occ of all characters (no duplicates in substring allowd and accounding adjust the left pointer)
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.length();
        if (n <= 1) return n ;

        vector<int> occurence(128,-1) ; //{0 - 127} : All covered
        int res = 1 ;
        int l = 0; 
        for (int r = 0 ; r<n ; r++) {
            if (occurence[ s[r] ] != -1) {   
                l = max(l, occurence[ s[r] ] + 1) ;// nxt of prevOcc
            }
            occurence[ s[r] ] = r ;// update to currOccurence
            res = max(res, r-l+1) ;
        }
        return res ;
    }
};
```

# COMPLEXICITY ANALYSIS 
| METRIC   | COMPLEXICITY   | HOW ? |
| TIME     |  O(N)          | String traversal |
| SPACE    |  O(128)        | (0-127) ASCII values of {Digit (0-9) , (A-Z) {65-90} , (a-z) {97-122} , (all special characters (included under 127 ASCII values))} |
