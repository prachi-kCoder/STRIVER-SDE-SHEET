# Flood-Fill 

- Here just don't forget to check whether the new-color is different from the orignalcolor of image[sr][sc] ,then do BFS (flood-fill)
- BFS is the best option for flood fill. {As level order traversal is the need this time !}

```cpp
class Solution {
public:
    vector<pair<int,int>> dir = {{-1,0},{0,1},{1,0},{0,-1}};
    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int color) {
        // bfs 
        
        int orig = image[sr][sc] ;
        if (orig == color) return image ;
        queue<pair<int,int>> q ;
        int m = image.size() ;
        int n = image[0].size();
        q.push({sr,sc}); 
        image[sr][sc] = color ;

        while (!q.empty()) {
            auto p = q.front() ; 
            q.pop();
            int r = p.first , c = p.second ;

            for (auto d : dir) {
                int nr = r + d.first , nc = c + d.second ;
                if (nr >= 0  && nc >= 0 && nr < m  && nc < n && image[nr][nc] == orig ) {
                    image[nr][nc] = color ;
                    q.push({nr , nc});
                }
            }
        }

        return image ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*N)     | Worst Case : If all cells are to be coloured |
| 🧠 SPACE |     O(N*N)       |  Queue (May take up all n*n cells) ,Image itself    |
