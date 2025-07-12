# VALID PARENTHESIS 
```cpp
class Solution {
public:
    bool isValid(string s) {
        vector<char> v(s.length()) ;
        int i = -1;
        for (char c : s) {
            if (c == '(' || c== '[' || c == '{') {
                i++;
                v[i] = c ;
            } else {
                if (i < 0) return false ;
                if ((v[i] == '(' && c == ')') ||
                    (v[i] == '[' && c == ']') ||
                    (v[i] == '{' && c == '}')) i-- ;
                else return false ;
            }
        }
        return i < 0 ;
    }
};
```
|  METRIC  |  COMPLEXICITY  | HOW ?  |
|----------|-------------------|-----|
| TIME   | O(n)  | Traversal |
| SPACE   | O(n)  | Vector |
