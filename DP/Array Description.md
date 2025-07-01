# ARRAY DESCRIPTION 
### Yes this  one is tricky because we are are taking decision based on prev and next values and fill in the 0 places so that no 2 adjacent pair have a diff > 1 

### INTUITION is to keep the prev valids and make the current valid 
- 2 scenarios a[i] == 0 {decide based on all prev value possibilities [1,m]} / a[i] != 0 {curr {act as prev for the nxt i will only have a[i]-1 , a[i] , a[i] + 1 as valid possibilities}}

- ```cpp
  #include <bits/stdc++.h>
  #define M 1000000007
  #define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
  #define ll long long 
  using namespace std;
  bool valid(vector<int>& a) {
    for (int i = 0; i < a.size()-1 ; i++) {
        if (abs(a[i] - a[i+1]) > 1) return false ;
    }
    return true ;
  }
  int main() {
    FASTIO ;
    int n , m ;
    cin >> n >> m ;
    vector<int> a(n) ;
    
    bool noZero = true ;
    
    for ( int i = 0 ; i < n ; i++ ) {
        cin >> a[i] ;
        if ( noZero && a[i] == 0 ) {
            noZero = false ;
        }
    }
    if (noZero) {
        if (!valid(a)) cout << 0 << endl ; 
        else {
            cout << 1 << endl ;
        }
        return  0 ;
    }
   
    
    ll dp[m+2] = {0} ;
    ll dpp[m+2] = {0} ;
    if (a[0] == 0) {// 0 start 
        for (int i = 1 ; i <= m ; i++) {
            dp[i] = 1 ;
        }
    }else {
        dp[a[0]] = 1 ;// fixed prev determines the nxt 
    }
    
    for (int i = 1; i <n ; i++) {
        if (a[i] == 0) {
            // present 
            for (int i = 1; i <= m ; i++) {
                dpp[i] = dp[i-1] + dp[i] + dp[i+1] ;
                dpp[i] %= M ;
            }
        }else {// nonZero so fixed 
            
            dpp[a[i]] = dp[a[i] - 1] + dp[a[i]] + dp[a[i] + 1] ;
            dpp[a[i]] %= M ;
        }
        for (int i = 0 ; i<= m ; i++) {
            dp[i] = dpp[i] ;
            dpp[i] = 0 ;// clear for nxt 
        }
    }
    ll res = 0 ;
    for (int i = 0; i <= m ; i++) {
        res += dp[i] ;
        res %= M;
    }
    cout << res << endl ;
  }
```
