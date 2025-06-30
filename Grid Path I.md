# GRID PATH I 
- Simply memoize results while finding path from top left to btm right and take care of Edge cases

```cpp
#include <bits/stdc++.h>
using namespace std;
const int mod = 1e9 + 7 ;
typedef long long ll ;
ll solve(int i , int j , int n , vector<vector<char>>& grid, vector<vector<ll>>& dp) {
    if ( i == n-1 && j == n-1) return 1LL ;
    if (grid[i][j] == '*') return 0LL ;
    if (dp[i][j] != -1) return dp[i][j];
    
    ll right = 0LL, down = 0LL ;
    if (j + 1 < n) {
        right = solve(i , j+1 , n , grid, dp);
    } 
    if (i + 1 < n) {
        down = solve(i+1 , j , n , grid, dp);
    }
    
    return dp[i][j] = (right + down)%mod ;
}
int main() {
    int n  ;
    cin >> n ;
    vector<vector<char>> grid(n , vector<char>(n)) ;
    vector<vector<ll>> dp(n , vector<ll>(n , -1)) ;
    
    for (int i = 0; i < n ; i++) {
        for (int j = 0; j < n ; j++) {
            cin >> grid[i][j] ;
        }
    }
    if (grid[0][0] == '*' || grid[n-1][n-1] == '*') {
        cout << 0 << endl ;
    }else {
        cout << solve( 0,  0, n ,grid , dp) << endl ;
    }
}

```
## COMPLEXICITY ANALYSIS : 
### ⏱ Time Complexity:  O(N^2) + Function Call Overhead 
### 🧠 Space Complexity:  O(N^2 + n) AS Recursion Stack at most 2n in Worst Case  
## TABULATION APPROACH : (Sum up the right and down paths )
```cpp
#include <bits/stdc++.h>
using namespace std;
const int mod = 1e9 + 7 ;
typedef long long ll ;
int main() {
    int n  ;
    cin >> n ;
    vector<vector<char>> grid(n , vector<char>(n)) ;
    for (int i = 0; i < n ; i++) {
        for (int j = 0; j < n ; j++) {
            cin >> grid[i][j] ;
        }
    }
    
    if (grid[0][0] == '*' || grid[n-1][n-1] == '*') {
        cout << 0 << endl ;
        return 0 ;
    }
    
    vector<vector<ll>> dp(n , vector<ll>(n , 0LL )) ;
    dp[0][0] =  1LL ;
    for (int i = 0 ; i < n ; i++) {
        for (int j = 0; j < n ; j++) {
            if (grid[i][j] == '*') continue ;
            if (i > 0) dp[i][j] = (dp[i][j] + dp[i-1][j]) %mod ;
            if (j > 0) dp[i][j] = (dp[i][j] + dp[i][j-1]) %mod ;
        }
    }
    
    cout << dp[n-1][n-1] << endl ;

}

```

## COMPLEXICITY ANALYSIS : 
### ⏱ Time Complexity:  O(N^2) 
### 🧠 Space Complexity:  O(N^2 ) 
