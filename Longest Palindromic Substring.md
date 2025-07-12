# Longest Palindromic Substring

```cpp
class Solution {
public:
    int expand(string &s , int l ,int r) {
        int n = s.length();
        while (l >= 0 && r < n) {
            if (s[l] != s[r]) break;
            l-- ;
            r++ ;
        }
        return r - l - 1 ;
    }
    string longestPalindrome(string s) {
        // Expand around center 
        int n = s.length();
        if (n <= 1) return s ;
        int maxLen = 0 ;
        string res = "" ;

        for (int i = 0 ; i < n-1 ; i++) {
            int odd = expand(s , i, i) ;
            int even = expand(s , i, i+1) ;
            if (max(odd, even) <= maxLen) continue ;
            if (odd > even) {
                int half = odd/2 ;
                res = s.substr(i-half , odd);
                maxLen = odd ;
            }else {
                int half = even/2 ;
                res = s.substr(i-half+1 , even) ;
                maxLen = even ;
            }
            if (maxLen == n) break ;
        }

        return res ;
    }
};
```
- LESS OPTIMISED BUT A GOOD APPROACH TO MAKE YOUR FUNDAMENTALS STRONGER
```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.length() ;
        if (n <= 1) return s ;

        int maxLen = 0 , li = -1 , ri = -1;

        vector<vector<bool>> dp(n , vector<bool>(n,false)) ;
        // len=1
        for (int l = 0 ; l < n ; l++) dp[l][l] = true ;
        // len = 2
        for (int i = 0; i <n-1 ; i++) {
            if (s[i] == s[i+1]) {
                dp[i][i+1] = true ;
                if (maxLen < 2) {
                    maxLen = 2;
                    li = i , ri = i+1 ;
                }
            }
        }
        for (int len = 3 ; len <= n ; len++) {
            for (int l = 0; l <= n-len ; l++) {
                int r = l + len - 1 ;
                if (s[l] == s[r] && dp[l+1][r-1]) {
                    dp[l][r] = true ;
                    if (maxLen < len) {
                        maxLen = len;
                        li = l , ri = r ;
                    }
                }
            }
        }
        if (li == -1) return s.substr(0,1) ;
        return s.substr(li , ri-li+1) ;
    }
};
```
## COMPLEXICITY ANALYSIS 
- Expand Around center :- 
| METRIX  |  COMPLEXICITY   | HOW ?  |
| --------|-----------------|---------|
| TIME    |   O(n*n)        | For every i , expand to whole n , but optimise if every you get n = maxLen break out of loop |
| SPACE   |    O(1)         | No space |

- DP Approach :- 
| METRIX  |  COMPLEXICITY   | HOW ?  |
| --------|-----------------|---------|
| TIME    |   O(n*n)        | For all lengths dp[i][j] check to be palindrome or not |
| SPACE   |    O(n*n)         | Dp Table |

