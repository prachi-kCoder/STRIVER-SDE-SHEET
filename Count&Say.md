# Count&Say

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

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n-1*( 2^(n-1)))      | As for RLE(n-1) times , and in each level in worst case we may get double the character (if all distinct characters) 2*(prevLen) .... upto n-1 level so powers of 2 }|
| 🧠 SPACE |  O(Len of string) = O(2^N)        | String can exponential grow |
