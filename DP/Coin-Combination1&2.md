# COIN COMBINATION (1 V/S 2) :
## Notice a slight difference in how these are different and how does it absolutely changes the answer ? 

### 🔄 Coin Combinations I – Permutations Allowed (Order Does not Matters)
In this variation, we are finding the number of ways to make a sum where the order of coins matters. That means [1, 2] and [2, 1] are counted as two different ways.

### 💡 Intuition
You're trying out every possible coin sequence that sums to the target. Think of it like arranging coins in all possible orders to reach the goal.

### 🔍 Code Insight
```Outer loops is over the previously formed target saying "No matter how the previously formed targets were they are further be used to for the jth curr target value .```

> Hence All possible ways covered
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll mod = (ll)1e9 + 7 ;

int main() {
    ll n , x ;
    cin >> n >> x;
    vector<ll> coins(n);
    for (ll i = 0; i < n ; i++) {
        cin >> coins[i] ;
    }
    ll mn = *min_element(coins.begin() , coins.end()) ;
    if (mn > x) {
        cout << 0 << endl ;
        return 0 ;
    }
    
    sort(coins.begin() , coins.end()) ;
    vector<ll> dp(x+1 , 0LL) ;
    
    dp[0] = 1 ;
    for (ll j = mn ; j <= x ; j++) {
        for (ll c : coins) {
            if (c > j) break ;
            dp[j] = ( dp[j] + dp[j-c] )% mod;
        }
    }
    cout << dp[x] << endl ;   
    return 0 ;
}

```
## 🔁 Coin Combinations II – Combinations Only (Order  Matter)
### 💡 Intuition
```
We're preventing rearrangements of the same coins from being counted multiple times by fixing the order in which coins are considered.
- Focus is over the coins being used if the coins used in ordered way then the cnt of target by a prev coin {obviously smaller coins } will only be included maintaining the sorted order of permutation .
```
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const ll mod = (ll)1e9 + 7 ;

int main() {
    ll n , x ;
    cin >> n >> x;
    vector<ll> coins(n);
    for (ll i = 0; i < n ; i++) {
        cin >> coins[i] ;
    }
    ll mn = *min_element(coins.begin() , coins.end()) ;
    if (mn > x) {
        cout << 0 << endl ;
        return 0 ;
    }
    
    sort(coins.begin() , coins.end()) ;
    vector<ll> dp(x+1 , 0LL) ;
    
    dp[0] = 1 ;
    
    for (ll c : coins) { // coins in ordered ways
        for (ll j = c ; j <= x ; j++) {
            dp[j] = ( dp[j] + dp[j-c] )% mod;
        }
    }
    cout << dp[x] << endl ;
    return 0 ;
}

```



