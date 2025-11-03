# Minimizing-Coins

```cpp
#include <iostream>
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
const ll mod = (ll)1e9 + 7 ;
void print(vector<ll>& a) {
    for (ll e : a) {
        cout << e << " " ;
    }
    cout << endl ;
}
int main() {
    ll n , x;
    cin >> n >> x;
    vector<ll> dp(x+1, -1LL) ;// get the min coin cnt ;
    dp[0] = 0 ;
    
    ll mn = 1e9 + 5 ;
    vector<ll> coins(n);
    for (ll i = 0; i < n ; i++) {
        cin >> coins[i] ;
        mn = min(coins[i],  mn) ;
    }
    if (mn > x) {
        cout << -1 << endl ;
        return 0 ;
    }
    
    sort(coins.begin() , coins.end()) ;
    for (ll i = 0 ; i < n ; i++) {
        ll c = coins[i] ;
        
        for (ll j = c ; j <= x ; j++) {
            if (dp[j-c] != -1) {
                if (dp[j] == -1 ) {
                    dp[j] = dp[j-c] + 1 ;
                }else {
                    dp[j] = min(dp[j] , dp[j-c] + 1 );
                }
            }
        }
    }
    
    cout << dp[x] << endl ;
    
    
    return 0;
}
```

- TC : O(n x x) as n <= 100 so O(100 * 10^6) = O(10^8) ie feasible in 1 sec
