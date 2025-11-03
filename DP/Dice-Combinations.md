# Dice-Combinations

```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
const ll mod = (ll)1e9 + 7 ;

int main() {
    ll n ;
    cin >> n ;
    vector<ll> dp(n+1, 0LL) ;
    dp[0] = 1 ;
    dp[1] = 1 ;
    
    for (ll i = 2 ; i <= n ; i++) {
        dp[i] = (2LL*dp[i-1]) % mod ;
        if (i - 7 >= 0) {
            dp[i] = (dp[i] - dp[i-7] + mod)%mod ;
        }
    }
    
    cout << dp[n] << endl ;
    
    
    return 0;
}
```
