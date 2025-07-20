# SODOKU - SOLVER 

- INTUITION IS TO TRACK USING **BITMASK** : Row mask, col mask , box (sub grid) are to be used

```cpp
class Solution {
public:
    int n ;
    bool dfs(int cell , vector<vector<char>>& board, vector<int>& row , vector<int>& col, vector<int>& box) {
        if (cell >= 81) return true ;

        int fullMask = (1<<9) - 1 ;
        int j = cell%9 ; int i = (cell-j)/9 ;
        if (board[i][j] != '.') return dfs(cell + 1, board , row , col, box) ;

        int bb =  (i/3)*3 + (j/3) ;
        for ( int d = 1 ; d <= 9 ; d++ ) {
            int num = d-1 ;// 0 place marking 
            if ((row[i]&(1<<num)) || (col[j]&(1<<num)) || (box[bb]&(1<<num))) continue ;
                row[i] =  row[i]|(1<<num) ;
                col[j] =  col[j]|(1<<num) ;
                box[bb] =  box[bb]|(1<<num) ;        
                board[i][j] = (char)(d + '0') ;

                if (row[i] == fullMask && col[j] == fullMask && box[bb] == fullMask ) return true ;

                if (dfs(cell + 1 , board , row, col , box )) return true ;

                board[i][j] = '.' ;
                row[i] =  row[i]^(1<<num) ;
                col[j] =  col[j]^(1<<num) ;
                box[bb] =  box[bb]^(1<<num) ;
        }
                    
            
        return false ;
    }
    void solveSudoku(vector<vector<char>>& board) {
        n = board.size();
        vector<int> row(n , 0);
        vector<int> col(n , 0);
        vector<int> box(n , 0); // [0-8]

        for (int i = 0 ; i < n ; i++) {
            for (int j = 0 ; j < n ; j++) {
                if (board[i][j] == '.') continue ;
                int val = board[i][j] - '0' ;
                val-- ;// 0 Based Mapping
                row[i]  = (row[i]|(1<<val)) ;
                col[j]  = (col[j]|(1<<val)) ;
                int k = 3*(i/3) + (j/3) ;
                box[k] =  (box[k]|(1<<val)); 
            }
        }

        dfs( 0 , board , row, col , box ) ;

        return ;
    }
};
```


# 🔍 Complexity Analysis

|  METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N * 9^N)     |  Here N = 81 , as for board of 9*9 = 81 cells , At every cell (1-9) digits , Then 9^N recursive possibilities in worst case .|
| 🧠 SPACE |  O(N) + 3*O(9)   | Recursion Stack of O(cells), here cells = 81 , mask for rows,cols,boxes   |


