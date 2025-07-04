### EDIT DISTANCE 

### TABULATION (btm - up)
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0), cout.tie(0)
#define pb push_back
using namespace std;
int edit(string& s , string& t) {
    int n = s.length() , m = t.length();
    vector<vector<int>> dp(n+1 , vector<int>(m+1 , 5001 )) ;
    for (int j = 0; j <= m ; j++) {
        dp[0][j] = j ;
    }
    for (int i = 0; i <=n ; i++){
        dp[i][0] = i ;
    }
    for (int i = 1; i <=n ; i++) {
        for (int j = 1; j <=m ; j++) {
            if (s[i-1] == t[j-1]) {
                dp[i][j] = dp[i-1][j-1];
            }else {
                int insert = 1 + dp[i][j-1] ;
                int del = 1 + dp[i-1][j] ;
                int rep = 1 + dp[i-1][j-1] ;
                dp[i][j] = min({insert , del , rep});
            }
        }
    }
    return dp[n][m];
}
int main() {
    FASTIO ;
    string s , t ;
    cin >> s ;
    cin >> t ;
    cout << edit(s, t) << endl ;
    return  0 ;
}
```
### MEMOIZATION (TOP-DOWN)
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0), cout.tie(0)
#define pb push_back
using namespace std;
int M ;
 
int solve(int i , int j , string& s, string& t ,  vector<vector<int>>& dp) {
    if (i >= s.length()) return t.length() - j ;
    if (j >= t.length()) return s.length() - i ;
    if (dp[i][j] != -1) return dp[i][j];
    
    if (s[i] == t[j]) {
        return dp[i][j] = solve(i+1 , j+1, s, t, dp);
    }else {
        int insert = 1 + solve(i , j+1 , s , t , dp) ;
        int del = 1 + solve(i+1 , j , s , t , dp);
        int repl =  1 + solve(i+1 , j+1 , s , t , dp) ;
        
        return dp[i][j] = min({insert , del , repl});
    }
}
int edit(string& s , string& t) {
     int n = s.size(), m = t.size();
    vector<vector<int>> dp(n + 1, vector<int>(m + 1, -1));
    
    return solve(0 ,0, s, t , dp);
}
int main() {
    FASTIO ;
    string s , t ;
    cin >> s ;
    cin >> t ;
    M = t.length() ;
    
    cout << edit(s, t) << endl ;
    return  0 ;
}
```
## 🚀 Complexity Analysis

### ⏱ Time Complexity

| Approach      | Time Complexity  |
|-------------  |------------------|
| **BTM-UP**    | O(n*m)           |
| **TOP-DOWN**  | O(n*m)           |


### 📦 Space Complexity

| Approach      | Space Breakdown |
|---------------|-----------------|
| **BTM-UP**    | O(n*m)        |
| **TOP-DOWN**  | O(n*m) {DP} + Recursive Stack O(n+m)       |

> **TOP-DOWN** : For n,m >= 10^4 then STACK-OVERFLOW is commonly observed , Not recommended for large n, m values
> **BTM-UP** : More recommended , specifically in case of large n, m.
