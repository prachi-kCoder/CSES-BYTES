# Creating-Strings
- Here mod expo important can get the fact and inv fact as huge no. and fact are to be calculated repetedly!

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll mod = (ll)1e9 + 7;
const ll N = (ll)1e6 ;
ll fact[N+1] , inv[N+1]  ;

ll mod_expo(ll base , ll expo) {
    ll res = 1LL ;
    while (expo > 0) {
        if (expo&1) res = (1LL* res * base)%mod ; 
        base = (1LL* base * base) % mod ;
        expo >>= 1 ;
    }
    return res ;
}
void precompute() {
    fact[0] = 1LL ;
    for (ll i = 1 ; i <= N ; i++ ) {
        fact[i] = ( 1LL * i * fact[i-1]) % mod ;
    }
    inv[N] = mod_expo( fact[N] , mod-2 ) ;
    for (ll i = N-1 ; i >= 0 ; i--) {
        inv[i] = ( 1LL * (i + 1) * inv[i+1]) % mod ;
    }
}

int main() {
	string s ;
	cin >> s ;
	if ( s.length() == 1 ) {
	    cout << 1 << endl ;
	    return 0 ;
	}
	ll n = s.length() ; 
	sort(s.begin() , s.end()) ;
	
	precompute() ; 
    ll last = 0LL ;
    ll res = fact[n] ;
    for (ll i = 1 ; i < n ; i++) {
        if (s[i-1] != s[i]) {
            res = (1LL * res * inv[i - last] ) % mod ;
            last = i ;
        }
    }
    res = (1LL * res * inv[n - last]) % mod ;
    // cout <<"last :" << last << " : " <<res << endl ;
    
    cout << res << endl ;
}

```
