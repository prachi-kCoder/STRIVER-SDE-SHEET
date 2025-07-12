# Longest Common Prefix
## APPROACH 1 : Take common of all strs 
```cpp
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if (strs.size() == 1) return strs[0] ;
        string pre = strs[0] ;
        for (int i = 1 ; i < strs.size() ; i++) {
            int j = 0 ; int k = 0 ;
            while (j < pre.length() && k < strs[i].length()) {
                if (pre[j] != strs[i][k]) break ;
                j++ ; k++ ;
            }
            pre = pre.substr(0 , j);
        }
        return pre ;
    }
};
```
## APPROACH 2 : SORTING (Head , Tail Deciders)
```cpp
string longestCommonPrefix(vector<string>& strs) {
        if (strs.size() == 1) return strs[0] ;
        sort(strs.begin() , strs.end());
        string f = strs[0] ;
        string l = strs[strs.size()-1] ;
        string res= "" ;
        for (int i = 0; i < min(f.length() , l.length()) ; i++) {
            if (f[i] == l[i]) {
                res += f[i] ;
            }else break ;
        }
        return res ;
    }
```
# COMPLEXICITY ANALYSIS 
- APPROACH 1 :
| METRIC  | COMPLEXICITY  | HOW ? |
|---------|---------------|--------|
|  TIME   |   O(n*maxlength(strs[i])) | Traverse through each string |
|  SPACE  |   O(1)       |  No space |

- APPROACH 2 :
| METRIC  | COMPLEXICITY  | HOW ? |
|---------|---------------|--------|
|  TIME   |   O(nlogn + m ) | Sorting  , m = min( Len(1st) , Len(Last)) |
|  SPACE  |   O(1)       |  No space |
