# Unique-Paths
## TABULATION 
```cpp
class Solution {
public:
    int dp[101][101] ;
    int uniquePaths(int m, int n) {
        if (m == 1 && n == 1) return 1 ;
        dp[m-1][n-1] = 1 ;
        for (int i = m-2 ; i>= 0 ; i--) {
            dp[i][n-1] =  1 ;
        }
        for (int j = n-2 ; j>= 0 ; j--) {
            dp[m-1][j] =  1 ;
        }
        for (int i = m-2 ; i >= 0  ; i--) {
            for (int j = n-2 ; j >= 0 ; j--) {
                dp[i][j] = dp[i+1][j] + dp[i][j+1] ;
            }
        }
        return dp[0][0] ;
    }
};

```
## MEMOIZATION
```cpp
class Solution {
public:
    int dp[101][101] ;
    int solve(int i , int j , int m , int n) {
        if (i == m-1 && j == n-1) return 1 ;
        if (i == m || j == n) return 0 ;
        if (dp[i][j] != -1) return dp[i][j] ;
        int ways = solve(i+1 , j , m , n) + solve(i , j+1 , m , n) ;
        return dp[i][j] = ways ;
    }
    int uniquePaths(int m, int n) {
        if (m == 1 && n == 1) return 1 ;
        memset(dp , -1, sizeof(dp)) ;
        return solve(0 ,0 , m , n) ;
    }
};

```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |     O(M*N)   |  For all M*N cells we take the sum of right , down paths |
| 🧠 SPACE |  O(M*N)   |   Dp Table |
