## FILLING BOOKCASE SHELVES 

```cpp
class Solution {
public:
    int n ; 
    // every shelf starting 
    int solve(int start , vector<vector<int>>& books , int shelfWidth , vector<int>& dp){
        if (start >= n) return 0 ;// all shelves done
        if (dp[start] != -1) return dp[start] ;

        int shelf_t = 0 ; 
        int shelf_h = 0 ; 
        int mx_ht = INT_MAX ;

        for (int i = start ; i < n ; i++ ){
            int book_t = books[i][0] ,book_h = books[i][1] ;

            if (shelf_t + book_t <= shelfWidth ) {
                shelf_h = max(shelf_h , book_h) ;
                shelf_t += book_t ;
                int nxt_ht = shelf_h + solve(i + 1 , books, shelfWidth , dp) ;
                mx_ht = min(mx_ht , nxt_ht) ;
            }else {
                break ;
            }
        }
        return dp[start] = mx_ht ;
    }
    int minHeightShelves(vector<vector<int>>& books, int shelfWidth) {
        n = books.size();
        if (n == 1) return books[0][1] ;
        vector<int> dp(n + 1 , -1) ;// miniPossible ht

        return solve(0 , books , shelfWidth , dp );
        
    }
};
```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N*N)  | For every ith start , we may check rest n-1 books on the same shelf (if shelfWidth allows) |
| 🧠 SPACE |     O(N)       |  Recusion Depth + Dp Table |
