# WORD - BREAK

- INTUITION :
  - Focus on ending Index of any substring found in dictionary .
  - dp[i] signifies that the substr ending at (i-1)th index  can be formed using the words in my dictionary
  - Base case dp[0] = true as substring ending at (-1)th index ie empty string can always be formed !
  - j set the starting index upto ith (ending index) to check for all substring possibly make the substring ending at ith index can  be achieved !

## TABULATION
```cpp
class Solution {
  public:
    bool wordBreak(string &s, vector<string> &dict) {
        unordered_set<string> set(dict.begin() , dict.end());
        int n = s.size();
        vector<bool> dp(n+1 , false) ;
        dp[0] = true ;
        
        for( int i = 1 ; i <= n ; i ++) {
            for (int j = 0 ; j < i ; j++) {
                if ( dp[j] && set.find(s.substr(j , i - j )) != set.end()) {
                    dp[i] = true ;
                    break ;
                }
            }
        }
        return dp[n] ;
    }
};
```

# MEMOIZATION 
```cpp
class Solution {
  public:
    bool solve(int ei ,string &s, unordered_set<string>& set, vector<int>& dp){
        if (ei < 0) return true ;
        
        if (dp[ei] != -1) return dp[ei];
        
        for (int si = 0 ; si <= ei ; si++ ) {
            if (solve(si-1 , s , set , dp) && set.find(s.substr(si,ei - si + 1)) != set.end()) {
                return dp[ei] = 1 ;
            }
        }
        
        return dp[ei] = false ;
    }
    bool wordBreak(string &s, vector<string> &dict) {
        unordered_set<string> set(dict.begin() , dict.end());
        int n = s.size();
        vector<int> dp(n+1 , -1) ;
        
        return solve(n-1 , s, set , dp) ;
    }
};
```
# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n*n)   | For all ending index i , all starting index j are checked in worst case |
| 🧠 SPACE |  O(n + m )  |  O(n) => DP Table + O(m) => set of words in dictionary , set lookups take O(1)time , but set formation from vector took O(m)|

