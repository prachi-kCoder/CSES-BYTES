# N-GRID & K-TURNS

# - USING :
- stars&bars combination principle :
- For n idential items to distribute in k non-empty groups :  `C(n-1 , k-1)`

- To get all count of moves from (0,0) -> (n-1,n-1)  with exactly K-TURNS
  
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll N_MAX = 1000005;
const ll mod = 1e9 + 7 ;
ll fact[N_MAX] ;
void precompute_fact() {
    fact[0] = 1 ;
    for (int i = 1 ; i < N_MAX ; i++) {
        fact[i] = (i*fact[i-1])%mod ;
    }
}
ll mod_expo(ll base , ll expo) {
    ll res = 1LL ;
    base %= mod ;
    while( expo > 0) {
        if (expo&1) res = (1LL*res*base)%mod ;
        base = (1LL * base * base )%mod ;
        expo >>= 1 ;
    }
    return res ;
}
ll mod_inv(ll num) {
    return mod_expo(num , mod-2) ;
}
ll nCr(ll n , ll r ){
    if (r > n || r < 0) return 0 ;
    if (n == r || r == 0 ) return 1 ;
    ll num = fact[n] ;
    ll deno = (1LL * fact[r] * fact[n-r] ) % mod ;
    return (1LL * num * mod_inv ( deno ) ) % mod ;
}
// N-1 items -> M Blocks  C(n-2 , M-1)
ll solve(ll n , ll k) {
    if (n == 1) {
        return (k == 0) ? 1 : 0;
    }
    if (k < 1 || k > 2 * n - 3) {
        return 0;
    }
    if (k % 2) { // odd turns 
        // even consec blocks = ( k+1 )
        ll M = (k + 1)/2 ;
        ll single = nCr(n-2 , M-1) ; // RDRD ... or DRDR ...
        
        ll total = ( 2LL * single * single ) %mod ;
        return total ;
        
    }else {// even turns 
        // odd consec blocks : 
        ll M = k / 2 ;  // other M + 1 blocks 
        // N-1 items to M blocks 
        ll sm = nCr(n-2 , M-1);
        // N-1 items to M+1 blocks 
        ll lg = nCr(n-2 , M) ;
        
        ll total = (2LL*sm*lg) %mod ; // one of then M+1 , and other M
        
        return total ;
    }
}
int main() {
    precompute_fact() ;
    ll n , k ;
    cin >> n >> k ;
    ll ways = solve(n , k) ;
    cout << ways << endl ;
    
    return 0 ;
}

```
