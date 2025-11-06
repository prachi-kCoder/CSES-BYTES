- Can do it using inv_fact array or byt mod_inv function to get `nCr`
  - Formula used  : `C ( n + g - 1 , g-1)` is to get the ways to distribute n items in g groups so that empty groups are also allowed
  - Stars & bars principle applied :
  - N stars  , to distribut in `g` groups -> g-1 bars
  - Total positions = `n+ g-1` ie stars  + bars
  - And since emtpy allowed so all combinations of g-1 bars from n + g - 1 total positions
    
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll mod = (ll)1e9 + 7;
const ll N = (ll)1e6 ;
ll fact[N+1] ;
void precompute() {
    fact[0] = 1LL ;
    for (ll i = 1 ; i <= N ; i++) {
        fact[i] = (1LL * i * fact[i-1]) % mod ;
    }
}
ll mod_expo(ll base , ll expo) {
    expo %= mod ;
    ll res = 1LL ;
    while (expo > 0) {
        if (expo&1) res = (1LL * res * base ) % mod ;
        base = (base * base) % mod ;
        expo >>= 1 ;
    }
    return res ;
}
ll mod_inv (ll b ){
    return mod_expo (b , mod - 2) ;
}
ll nCr(ll n , ll r) {
    if ( r > n || n == 0 ) return 0LL ;
    ll num = fact[n] ;
    ll deno_inv = 1LL * mod_inv((1LL * fact[r] * fact[n-r]) % mod) % mod ;
    return (1LL * num * deno_inv ) % mod ;
}
 
int main() {
	ll n , g ;
	cin >> g >> n ;
	// n items in g groups {empty / non empty both}
    // C (n + g-1 , g-1) 
    precompute(); 
    ll res = nCr( n + g - 1 , g - 1) ;
    cout << res << endl ;
}

```
