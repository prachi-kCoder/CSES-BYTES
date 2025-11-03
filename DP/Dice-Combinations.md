# Dice-Combinations
- Complete intuition it :
- 
-  dp[i] = dp[i-1] + dp[i-2] + .. dp[i-6]  ie the sum depends over the last dice thrown
```
dp[i] =  dp[i-1] + dp[i-2] + dp[i-3] + dp[i-4] + dp[i-5] + dp[i-6]
Substituting  : (i -> i-1 ):

dp[i-1] =  dp[i-2] + dp[i-3] + dp[i-4] + dp[i-5] + dp[i-6] + dp[i-7]

{Block = dp[i-2] + dp[i-3] + dp[i-4] + dp[i-5] + dp[i-6] } common in both
rewriting the equation :
dp[i] - dp[i-1] =  Block {1}
dp[i-1] - dp[i-7] =  Block  {2}

Solving it we get 
-  dp[i] = 2LL*dp[i-1] - dp[i-7]

```

- This is Sliding Window Approach in which the block of terms which are repetitive in the consecutive calculation is eliminated wisely .
- dp[i-7] Reduction actually means the as we move forward the dp[i-7] th element will be out of the window {which was present in the cal of prev term dp[i-1]th cal so now for dp[i] it has it be eliminated}


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

TC : O(N)
