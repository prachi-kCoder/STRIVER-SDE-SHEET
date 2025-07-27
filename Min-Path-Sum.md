# MIN-PATH-SUM
### BOTTOM - UP  APPROACH
```cpp
class Solution {
public:
 
    int minPathSum(vector<vector<int>>& grid) {
        int n = grid.size() ; int m = grid[0].size() ;

        vector<vector<int>> dp(n , vector<int>(m  , 200)) ;
        dp[n-1][m-1] = grid[n-1][m-1] ;
        for (int i = n-2 ; i >= 0 ; i--) {
            dp[i][m-1] = grid[i][m-1] + dp[i+1][m-1] ;
        }
        for (int j = m-2 ; j >= 0 ; j--) {
            dp[n-1][j] = grid[n-1][j] + dp[n-1][j+1] ;
        }
        for (int i = n-2 ; i >= 0 ; i--) {
            for (int j = m-2 ; j >= 0 ; j--) {
                dp[i][j] = grid[i][j] + min(dp[i+1][j] , dp[i][j+1]) ;
            }
        }

        return dp[0][0] ;
    }
};
```


## TOP - DOWN APPROACH
```cpp
  int solve(int i , int j , int n , int m ,vector<vector<int>>& grid , vector<vector<int>>& dp) {
        if (i == n-1 && j == m-1) return grid[i][j] ;
        if (i >= n || j >= m) return INT_MAX ;
        if (dp[i][j] != -1) return dp[i][j] ;
        int d = solve(i+1 , j , n , m , grid , dp);
        int r = solve(i , j+1 , n , m , grid , dp);
        int choice = min(d , r) ;
        if (choice == INT_MAX)  return INT_MAX ;
        return dp[i][j] = grid[i][j] + choice;
    }
    int minPathSum(vector<vector<int>>& grid) {
        int n = grid.size() ; int m = grid[0].size() ;

        vector<vector<int>> dp(n , vector<int>(m  , -1)) ;
        

        return solve(0 ,0, n , m, grid , dp) ;
    }
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  | O (N*M)       | Each cell is computed once; whether bottom-up or memoized top-down, total operations are proportional to grid size.|
| 🧠 SPACE |  O(N*M)     |  dp[n][m] table plus recursion stack (if using top-down memoization).    |
