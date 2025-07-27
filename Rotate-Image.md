## ROTATE-IMAGE 
- Here we need to make complete cyclic rotation for elements to be placed correctly after 90 deg rotation
- if n = 5 so  (0,0) -> (0,4) -> (4,4) -> (4,0) -> (0,0)   Ie CLOCKWISE DIRECTION
- Now to move in clockwise direction we actually fill up the other way round , ie Move backWard
  - Take temp = start (0,0)
  - Then change (0,0) with (4,0)
  - Then change (4,0) with (4,4)
  - Then change (4,4) with (0,4)
  - Then change (0,4) with (0,0) ie what we stored in Temp (as we have changed it already !)

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& mat) {
        int n = mat.size();   
        int m = mat[0].size();   

        for (int i = 0; i < n/2 ; i++) {
            for (int j = i ; j < n-1-i ; j++) {
                int temp = mat[i][j] ;

                mat[i][j] = mat[n-1-j][i]  ;
                mat[n-1-j][i] = mat[n-1-i][n-1-j];
                mat[n-1-i][n-1-j] = mat[j][n-1-i] ;
                mat[j][n-1-i] = temp ;
            }
        }
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N*N)  | i ranges [0,N/2) and  j from [i ,n-1-i]| 
| 🧠 SPACE |       O(1)     |     No extra space       |
