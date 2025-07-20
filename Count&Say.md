# Count&Say

## ITERATIVE 
```cpp
class Solution {
public:
    string countAndSay(int n) {
        if (n == 1) return "1" ;
        string r = "1" ;

        for (int i = 1 ; i < n ; i++) { // n-1 times ;
            stringstream ss ;
            int m = r.length() ;
            int j = 0 ;
            while (j < m) {
                if (j == m-1) {
                    ss << "1" ;
                    ss << r[m-1] ;
                    break ;
                }
                int c = 1 ;
                while (j+1 < m && r[j] == r[j+1]) {
                    j++ ; c++ ;
                }
                ss << (char)(c + '0') ;
                ss << r[j] ;
                j++ ;
            }
            r = ss.str() ;
        }
        return r ;
    }
};
```

## RECURSIVE 
```cpp
string solve(int n ,const string& s) {
        if (n == 1) return s ;
        stringstream ss ;
        int i = 0 ; int m = s.length();

        while ( i < m ) {
            if (i == m-1) {
                ss << '1' ;
                ss << s[i] ;
                break ;
            }
            int c = 1 ;
            while (i + 1 < m && s[i] == s[i+1]) {
                c++ ; i++ ;
            }
            ss << (char)(c + '0') ;
            ss << s[i] ;
            i++ ;
        }
        // string f = ss.str();
        return solve(n-1 , ss.str()) ;
    }
    string countAndSay(int n) {
        if (n == 1) return "1" ;
        
        return solve(n , "1"  );
    }
```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n-1*( 2^(n-1)))      | As for RLE(n-1) times , and in each level in worst case we may get double the character (if all distinct characters) 2*(prevLen) .... upto n-1 level so powers of 2 }|
| 🧠 SPACE |  O(Len of string) = O(2^N)        | String can exponential grow |
