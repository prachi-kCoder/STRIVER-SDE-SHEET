# Search a 2D Matrix

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& mat , int target) {
        int m = mat.size() ;
        int n = mat[0].size() ;
        int row = 0 ;
        int up = 0 , down = m-1 ;
        while (up <= down) {
            int mid = up + (down-up)/2 ;
            if (mat[mid][0] <= target) {
                row = mid ;
                up = mid + 1 ;
            }else {
                down = mid - 1 ;
            }
        }
        int l = 0 , r = n-1 ;
        while (l <= r) {
            int mid = l + (r-l)/2 ;
            if (mat[row][mid] == target) return true ;
            if (mat[row][mid] < target) {
                l = mid + 1 ;
            }else {
                r = mid - 1 ;
            }
        }
        return false ;
    }
};
```

### BETTER WAY OF WRTING THIS COULD BE  {Assuming Matrix as flattened array }:
```cpp
bool searchMatrix(vector<vector<int>>& mat , int target) {
        int m = mat.size() ;
        int n = mat[0].size() ;
        int l = 0 , r = m*n-1 ;
        while (l <= r) {
            int mid = l + (r-l)/2 ;
            int j = mid%n ;
            int i = (mid-j)/n ;
            if (mat[i][j] == target) return true ;
            if (mat[i][j] < target) {
                l = mid + 1 ;
            }else{
                r = mid - 1 ;
            }
        }
      return false ;
}
```


# 🔍COMPLEXICITY ANALYSIS

🔁 Comparison Table :
| Approach	| Time Complexity |	Space	 | Notes |
| Flattened Binary Search	|O(log(m * n))	| O(1)	| Treats matrix as 1D |
| Your Two-Level Search	| O(log m + log n)| O(1)	|More intuitive, row-first |
