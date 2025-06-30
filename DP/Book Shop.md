## Apply 0-1 KNAPSACH APPROACH  (2D OR 1D Dp )

🎯 0/1 Knapsack Complexity Analysis
### ✅ 1. 2D Dynamic Programming
- Time Complexity: For each item (n), you iterate through each capacity (x): → O(n * x)
-Space Complexity: You use a full 2D dp[n+1][x+1] table: → O(n * x)

### ✅ 2. 1D Space-Optimized DP
- Time Complexity: Same double loop structure → still O(n * x)
- Space Complexity: You maintain just a dp[x+1] array: → O(x)

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll ;

int tab(int n ,int x, vector<int>& price, vector<int>& page) {
    vector<vector<int>> dp( n + 1 , vector<int>(x + 1, 0)) ;
    
    for (int i = 1 ; i <= n ; i++) {
        for (int j = 1 ; j <= x ; j++) {
            if (price[i-1] <= j) {
                dp[i][j] =  max(dp[i-1][j] , (page[i-1] + dp[i-1][j-price[i-1]]) ) ;
            }else {
                dp[i][j] = dp[i-1][j] ;
            }
        }
    }
    return dp[n][x] ;
}

int tab1D(int n , int x , vector<int>& price , vector<int>& page ) {
    vector<int> dp(x + 1 , 0 ) ;// 1D Dp 
    
    for ( int i = 0 ; i < n ; i++ ) {
        for (int j = x ; j >= price[i] ;  j--) {
            dp[j] = max(dp[j] , page[i] + dp[j-price[i]] ) ;
            
        }
    }
    return dp[x] ;
}
int main() {
    int n , x ;
    cin  >> n >> x ;
    vector<int> prices(n), pages(n) ;
    
    for (int i = 0; i < n ; i++) cin >> prices[i] ;
    for (int i = 0; i < n ; i++) cin >> pages[i] ; 
    cout << tab(n , x , prices , pages ) << endl ;
    cout << tab1D(n , x , prices , pages ) << endl ;
}

```
