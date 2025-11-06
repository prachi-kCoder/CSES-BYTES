# Christmas-Party

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll mod = (ll)1e9 + 7;
const ll N = (ll)1e6 + 5;
ll fact[N+1] ,inv_fact[N+1] ;
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
ll mod_inv (ll b){
    return mod_expo (b , mod - 2) ;
}
void precompute() {
    fact[0] = 1LL ;
    for (ll i = 1 ; i <= N ; i++) {
        fact[i] = (1LL * i * fact[i-1]) % mod ;
    }
    inv_fact[N] = mod_inv( fact[N] ) ;
    for (ll i = N - 1 ; i >= 0 ; i--) {
        inv_fact[i] = (1LL * (i + 1) * inv_fact[i+1]) % mod ;
    }
}

 
int main() {
	ll n ;
	cin >> n ;
// 	n! x ( 1 - 1/1! + 1/2! - ..)

	ll ans = fact[n] ;
	ll even = 0LL, odd = 0LL ;
	for (ll i = 0 ; i <= n ; i++) {
	    if (i % 2 == 0) {
	        if (i == 0 ) {
	            even = (even + 1 ) % mod ;
	        }else {
	            even = (even + inv_fact[i]) % mod ;
	        }
	    }else {
	       odd = (odd + inv_fact[i]) % mod ;
	    }
	}
	ans = (1LL * ans * (( even - odd + mod ) % mod)) % mod ;
	cout << ans << endl ;
	
	
	return 0;
	
}

```
