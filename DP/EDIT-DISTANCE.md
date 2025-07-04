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

## 🚀 Complexity Analysis

### ⏱ Time Complexity

| Approach    | Time Complexity  |
|-------------|------------------|
| **BTM-UP**  | O(n*m)           |


### 📦 Space Complexity

| Approach | Space Breakdown |
|----------|-----------------|
| **BTM-UP**  | O(n*m)       |
