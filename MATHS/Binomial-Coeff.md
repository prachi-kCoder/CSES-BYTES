# BINOMIAL-COEFFICIENT

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
const ll mod =(ll)(1e9 + 7) ;
const ll N =(ll)(1e6 + 1) ;

ll mod_expo(ll base , ll expo) {
    ll res = 1LL ;
    while (expo > 0) {
        if (expo&1) res = (res*base)%mod ;
        base = (base*base)%mod ;
        expo >>= 1 ;
    }
    return res ;
}
ll mod_inv(ll b) {
    return mod_expo(b , mod - 2) ;
}
int main() {
    
    ll t ;
    cin >> t ;
    
    ll fact[N+1] ;
    fact[0] = 1 ; fact[1] = 1 ;
    for (ll i = 2 ; i <= N ; i++) {
        fact[i] = (1LL*i*fact[i-1] )%mod ;
    }
    
    while (t-- > 0) {
        ll n , r ;
        cin >> n >> r ;
        
        cout << (1LL * fact[n] * mod_inv(( fact[r] * fact[n-r]) % mod )) %mod<< endl ;
        
    }
    
    return 0 ;
}

```
