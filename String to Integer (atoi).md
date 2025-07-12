# STRING TO INTEGER (ATOI) 

```cpp
class Solution {
public:
    int myAtoi(string s) {
        int n = s.length() , i = 0; 
        
        long long res = 0 ;
        while (i < n && s[i] == ' ') i++ ;
        if (i == n) return  0 ;

        int sign = 1 ;
        if (s[i] == '-') {sign = -1 ;i++ ;}
        else if (s[i] == '+') i++ ;
        
        while (i < n && isdigit(s[i])) {
            res = res*10 + (s[i]- '0') ;
            if (sign*res > INT_MAX) return INT_MAX ;
            if (sign*res < INT_MIN) return INT_MIN ;
            i++ ;
        }

        return static_cast<int>(sign*res) ;
    }
};
```

# COMPLEXICITY ANALYSIS 
| METRIC   | COMPLEXICITY |   HOW ?  |
|----------|--------------|-----------|
| TIME     |  O(N)        |  Traversal |
| SPACE    |  O(1)        |  No space |
