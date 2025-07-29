# Detonate-Max-Bombs

```cpp
class Solution {
public:
    vector<vector<int>> adj ;
    int dfs(int node ,  int n , vector<bool>& vis ){
        // mask = (mask|(1<<node));
        vis[node] = true;
        int c = 1 ;

        for (int nbr : adj[node]) {
            if (!vis[nbr]) {
                c += dfs(nbr, n, vis);
            }
        }
        return c ;
    }
    int maximumDetonation(vector<vector<int>>& bombs) {
        int n = bombs.size();
        if (n <= 1) return n; 
        adj.resize(n);
        int mxCnt = 0 ;

        for (int i = 0; i < n-1 ; i++) {
            for (int j = i+1 ; j < n ; j++) {
                if (i == j) continue ;
                vector<int> b1 = bombs[i] ; 
                int x1 = b1[0] , y1 = b1[1], r1 = b1[2] ; 
                vector<int> b2 = bombs[j] ; 
                int x2 = b2[0] , y2 = b2[1], r2 = b2[2] ; 

                long long dist = (1LL*(x2-x1)*(x2-x1)) + (1LL*(y2-y1)*(y2-y1)) ; 
                if ((1LL*r1*r1) >= dist) {
                    adj[i].push_back(j) ;
                }
                if ((1LL*r2*r2) >= dist) {
                    adj[j].push_back(i) ;
                }
            }
        }

        for (int i = 0; i < n ; i++) {
            // long long mask = 0 ;
            vector<bool> vis(n,false);
            mxCnt = max(mxCnt , dfs(i , n , vis)) ;
            if (mxCnt == n) break ;
        }
        
        return mxCnt ;
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N²)       |Building the adjacency graph takes O(N²); DFS from each bomb (N times) can visit up to N nodes in worst case. |
| 🧠 SPACE |    O(N²)     |   Adjacency list stores up to N² edges; DFS recursion stack may grow to depth N in worst-case chain detonation.      |
