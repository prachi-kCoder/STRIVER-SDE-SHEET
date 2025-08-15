# Set Matrix Zeroes

- Keep Space Complexicity `O(1)`
- Take `first_row `& `first_col` are marker col , and prior to it do check that whether they need to be made 0 or not
- Now for non - zero i , j , by looking at markers  mat[0][j] & mat[i][0] make the cell 0 if its row /col needs to be made 0
- Then handle 1st row and 1st col separately !

### Steps :
     - First pass to mark rows/columns.
      - Second pass to zero out based on markers.
      - Final pass to handle first row and column.
  
```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& mat ) {
        int m = mat.size();
        int n = mat[0].size();

        bool first_col = false ;
        bool first_row = false ; 
        for (int i = 0; i <m ; i ++) {
            if (mat[i][0] == 0) first_col = true ;
        }
        for (int j = 0; j <n ; j++) {
            if (mat[0][j] == 0) first_row = true ;
        }
        for (int i = 1 ; i < m ; i++) {
            for (int j = 1 ; j < n ; j++) {
                if (mat[i][j] == 0) {
                    mat[i][0] = 0 ;
                    mat[0][j] = 0 ;
                }
            }
        }
        for (int i = 1 ; i < m ; i++) {
            for (int j = 1 ; j< n ; j++) {
                if (mat[0][j] == 0 || mat[i][0] == 0) {
                    mat[i][j] = 0 ;
                }
            }
        }
        if (first_col) {// lastrow is also 0
            for (int i = 0; i < m; i++) mat[i][0] = 0 ;
        }
        if (first_row) {
            for (int j = 0; j < n; j++) mat[0][j] = 0 ;
        }
        
    }
};
```


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |     O(M*N)        |  Matrix traversal         |
| 🧠 SPACE |     O(1)       | No extra space           |
