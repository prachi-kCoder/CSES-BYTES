# Two-Sets ii

- In this ques the standard pattern of subset sum works to make half of the total sum of all [1.n]
- Modulo Arithmetic is crucial
- While divi : {As no division exits in mod arithmetic rather take the mult with mod_inv of (2)} and take the mod at every step of cal to avoid as integer overflow !
- 

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
const ll mod = (ll)1e9 + 7 ;
ll mod_expo(ll base , ll expo) {
    ll res = 1LL ;
    while (expo > 0) {
        if (expo&1) res = (1LL*res*base)%mod ;
        base = (1LL*base*base)%mod ;
        expo >>= 1 ;
    }
    return res ;
}
ll mod_inv(ll num) {
    return mod_expo(num , mod-2) ;
}
int main() {
    ll n ;
    cin >> n ; 
    ll total = (1LL*n*(n+1))/2 ;
    // cout << total << endl ;
    if (total%2) {
        cout << 0 << endl ;
        return 0 ;
    }
    
    ll target = total / 2 ;
    
    vector<ll> dp(target + 1 , 0LL) ;
    dp[0] = 1LL ;
    
    for (int i = 1 ; i <= n ; i++) {
        for ( int j = target ; j >= i ; j-- ) {
            if (dp[j-i] > 0) {
                dp[j] = (dp[j-i] + dp[j])%mod ;
            }
        }
    }
    
    ll inv2 = mod_inv(2) ;
    
    cout << (1LL*dp[target]*inv2) % mod << endl ;
    
    
    return 0 ;
}

```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY	  |  🧩 EXPLANATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N  x SUM)      | Sum = Half of total sum  as with every n val we check all possible sum  |
| 🧠 SPACE |     O( SUM )       | 1D - DP           |
