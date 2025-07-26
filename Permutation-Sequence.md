# PERMUTATION-SEQUENCE

- **Important** things to take care :
  - Digits used at a place is not to be used again, keep track of used digits 
  - Take the right digits , calculating the permutation that will be covered will moving we move from d = 1 to n on any position .
  - At any position : With a digit the permutations covered = fact[n-pos] , so the position determines the count fo permuation that will be covered .

```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        vector<int> fact(n+1) ;
        fact[0] =1 ;
        vector<int> nums ;
        for (int i = 1; i <= n ; i++) {
            fact[i] = i*fact[i-1] ;
            nums.push_back(i) ;
        }
        // get the right digit for the rightPlace 
        // 0-indexed k
        k-- ;
        string s = "";
        for (int pos = 1 ; pos <= n ; pos++){
            int idx = k / fact[n-pos] ; // divide using the permutation cnt

            s += (char)(nums[idx] + '0') ;
            nums.erase(nums.begin() + idx);
            k %= fact[n-pos] ;
        }
        return s ; 
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N*N)    |  Calculating fact + N position traversal with erasing (O(n*n)) |
| 🧠 SPACE |  O(N)      |   Vector of fact for fact upto n value |


### This is brute force not recommnended but :
```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        string s = "" ;
        for (int d = 1 ; d <= n ; d++) {
            s += (char)(d + '0') ;
        }

        int f = 0 ;
        do {
            f++ ;
            if (f == k) break ;
        } while (next_permutation(s.begin() , s.end()));
        return s ;
    }
};
```
| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(K*N)    |  Each next_permutation() takes O(N) time and we run it K times in worst-case and K range[1, N!] |
| 🧠 SPACE |  O(N)      |   Just a string of length N |
