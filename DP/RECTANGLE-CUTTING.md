# RECTANGLE CUTTING 
## TABULATION 
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int a , b ;
    cin >> a >> b ;
    vector<vector<int>> dp(a + 1 , vector<int>(b+1 , 1e9)) ;
    for (int i = 1 ; i <= a ; i++) {
        for (int j = 1 ;j<= b ; j++) {
            if (i == j) {
                dp[i][j] = 0 ;
            }else {
                // vertical cuts 
                for (int k = 1 ; k < i ; k++) {
                    dp[i][j] = min(dp[i][j] , 1 + dp[k][j] + dp[i-k][j]);
                }
                // horizontal cuts 
                for (int k = 1 ; k < j ; k++) {
                    dp[i][j] = min(dp[i][j] ,1 + dp[i][k] + dp[i][j-k]);
                }
            }
        }
    }
    cout << dp[a][b] << '\n' ;
    return 0 ;
}
```
## MEMOIZATION
```cpp
#include <bits/stdc++.h>
using namespace std;

int dp[501][501] ;
int minMoves(int a , int b) {
    if (a == b) return 0 ;
    if (a == 1) return b-1 ;
    if (b == 1) return a-1 ;
    if (dp[a][b] != 0) return dp[a][b];
    if (dp[b][a] != 0) return dp[b][a];
    
    int vertical = 501 ;
    for (int l = 1 ; l < a ; l++) {
        int left = minMoves(l , b) ;
        int right = minMoves(a - l , b) ;
        vertical = min(1 + left + right , vertical) ;
    }
    int hori = 501 ;
    for (int h = 1 ; h < b ; h++) {
        int up = minMoves(a , h ) ;
        int down = minMoves(a , b - h) ;
        hori = min(1 + up + down , hori) ;
    }
    return dp[a][b] = min(vertical , hori);
}
int main() {
    int a , b ;
    cin >> a >> b ;
    cout << minMoves(a , b) << endl ;
    
    return 0 ;
}
```

### 📊 Complexity Analysis
| APPROACH  | TIME COMPLEXICITY   | SPACE COMPLEXICITY        | HOW ? |
|------------|--------------------|---------------------------|--------|
|MEMOIZATION | O(a^2 * b + a * b^2 ) |  O(501 * 501)         |O(a × b) unique states.,For each (a, b) {a-1 Vertical , b-1 Horizontal cuts} = O(a + b) time 
|            |                       |  + Recursion (a + b)  |Total Time = O(a*b*(a+b)) = O(a^2 * b + a*b^2) => Cubic Complexicity , but acceptable as a <= 500 and b <= 500
|TABULATION  | O(a^2 * b + a * b^2 ) |  O(a * b)             | Same as above |

### > Tabulation is more recommended to avoid recursion overhead and cache-friendly and no possibilities of Stack Overflow .
