# EDIT DISTANCE 
#### BOTTOM-UP
```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();
        vector<vector<int>> dp(n+1 , vector<int>(m+1 , 0));
        // w1 empty by w2 not ->Insert
        for (int j = 1 ; j <= m ; j++ ) dp[0][j] = j;
        // w2 empty by s1 not ->Delete
        for (int i = 1 ; i <= n ; i++ ) dp[i][0] = i;

        for (int i = 1 ; i<= n ; i++) {
            for (int j = 1 ; j<= m ; j++) {
                if (word1[i-1] == word2[j-1]) {
                    dp[i][j] = dp[i-1][j-1] ;
                }else {
                    int insert = dp[i][j-1] ;
                    int del = dp[i-1][j] ;
                    int replace = dp[i-1][j-1] ;
                    dp[i][j] = 1 + min({insert, del , replace}) ;
                }
            }
        }

        return dp[n][m];
    }
};
```

### MEMOIZATION
```cpp
int solve(int i , int j , int n , int m , string& word1 , string& word2, vector<vector<int>>& dp) {
        if ( i == n ) return m-j ;// insertion Length
        if ( j == m ) return n-i ;// deletion Length
   
        if (dp[i][j] != -1) return dp[i][j] ;

        if (word1[i] == word2[j]) {
            return dp[i][j] = solve(i+1 , j+1 , n , m , word1 , word2, dp);
        } else {
            int insert =  solve(i , j+1 , n , m , word1 , word2, dp);
            int del =  solve(i+1 , j , n , m , word1 , word2, dp) ;
            int rep =  solve(i+1 , j+1 , n , m , word1 , word2, dp) ;
            int c = min({insert , del , rep}); 

            return dp[i][j] = (c == INT_MAX ? c : c + 1) ;
        }
        
    }
    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();
        vector<vector<int>> dp(n , vector<int>(m , -1));

        return solve( 0 ,0, n , m , word1 , word2 , dp);
    }
```
- REVERSED WAY OF WRITING THE SAME (MEMOIZATION):
```cpp
int solve(int i , int j , int n , int m , string& word1 , string& word2, vector<vector<int>>& dp) {
        if ( i < 0 ) return j+1 ;// insertion Length
        if ( j < 0 ) return i+1 ;// deletion Length
   
        if (dp[i][j] != -1) return dp[i][j] ;

        if (word1[i] == word2[j]) {
            return dp[i][j] = solve(i-1 , j-1 , n , m , word1 , word2, dp);
        } else {
            int insert =  solve(i , j-1 , n , m , word1 , word2, dp);
            int del =  solve(i-1 , j , n , m , word1 , word2, dp) ;
            int rep =  solve(i-1 , j-1 , n , m , word1 , word2, dp) ;
            int c = min({insert , del , rep}); 

            return dp[i][j] = (c == INT_MAX ? c : c + 1) ;
        }
        
    }
    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();
        vector<vector<int>> dp(n , vector<int>(m , -1));

        return solve( n-1 ,m-1, n , m , word1 , word2 , dp);
    }
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*M)     |  Check all (i,j) pairs to match and get minOperation req , in worst non of the character matches hence all pair of character are tried|
| 🧠 SPACE |     O(N*M)  |  dp TABLE           |

