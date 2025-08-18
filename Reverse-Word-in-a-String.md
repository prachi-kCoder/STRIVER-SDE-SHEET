# Reverse-Word-in-a-String
- In this using vector<string> for words is more recommended so that you can efficiently join in a go
- Directly making res is also possible but u need to prepend the words and overall it will  O(N*N) as new string will be created every time with the prepend of new words
  
```cpp
class Solution {
public:
    string reverseWords(string s) {
        string res = "";
        int n = s.length();
        int i = 0 ;
        vector<string> v ;
        while (i < n ) {
            while (i < n && s[i] == ' ') i++ ;
            stringstream ss ;
            while  (i < n && s[i] != ' ')  {
                ss << s[i] ;
                i++ ;
            }
            
            string t = ss.str();
            if (!t.empty()) {
                v.push_back(t) ;
            }
            // if (res.empty()) {
            //     res = ss.str() ;
            // }else {
            //     res = ss.str() + ' ' + res ;
            // }
        }
        for (int j = v.size()-1 ; j >= 0 ; j--) {
            if (!res.empty()) res += " " ;
            res += v[j] ;
        }
        return res ;
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N)         |      joining in a go is considered efficient |
| 🧠 SPACE |    O(N)        |   vector for words         |
