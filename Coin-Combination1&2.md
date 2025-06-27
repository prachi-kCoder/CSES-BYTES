# COIN COMBINATION (1 V/S 2) :
## Notice a slight difference in how these are different and how does it absolutely changes the answer ? 

### 🔄 Coin Combinations I – Permutations Allowed (Order Matters)
In this variation, we are finding the number of ways to make a sum where the order of coins matters. That means [1, 2] and [2, 1] are counted as two different ways.

### 💡 Intuition
You're trying out every possible coin sequence that sums to the target. Think of it like arranging coins in all possible orders to reach the goal.

### 🔍 Code Insight
The outer loop goes over the target sum, and the inner loop iterates through each coin:

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll ;

int main() {
    // Coin comb 1 : Targets are ordered 
	int n , x ;
	cin >> n >> x ;
	vector<int> coins(n) ;
	for ( int i = 0 ; i < n ; i++) {
	    cin >> coins[i] ;   
	}
	
	vector<ll> dp(x + 1 , 0LL) ;
	dp[0] = 1LL ;
	for ( int j = 0 ; j <= x ; j++ ) {
	    for (int i = 0 ; i < n ; i++ ) {
	        if ( j + coins[i] <= x ) {
	            dp[j + coins[i]] += dp[j] ;// target made in order 
	        }
	    }
	}
	cout << dp[x] << endl ;
}
```
### Example : n = 3 , x = 9 , coin = {2,3,5} 
Coin Comb1 : 
Here dp = [1 0 1 1 1 3 2 5 6 8 8] 
As j = 0 , j <= x smaller sum are used to make larger ones regardless of what coins we used to make the smaller sum .

## 🔁 Coin Combinations II – Combinations Only (Order Doesn’t Matter)
Here, we’re counting the number of distinct combinations regardless of coin order. So [1, 2] and [2, 1] are considered the same.

### 💡 Intuition
We're preventing rearrangements of the same coins from being counted multiple times by fixing the order in which coins are considered.

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll ;

int main() {
    int n , x ;
    cin >> n >> x ;
    vector<int> coins(n) ;
    
    for ( int i = 0 ; i < n ; i++) {
        cin >> coins[i] ;
    }
    // Now to keep the coins in Ordered fashion (pick coin in ordered way )
    vector<ll> dp(x + 1 , 0LL ) ;
    dp[0] = 1LL ;
    for (int i = 0 ; i < n ; i++) {
        for (int j = 0 ; j <=x ; j++) {
            if (j +  coins[i] <= x) {
                dp[j + coins[i]] += dp[j] ;
            }
        }
    }
    cout << dp[x] << endl ;
}
```

Here dp  = [1 0 1 1 1 2 2 2 3 3] 
As smaller coins are picked first to make any improvement in the sum if possible then increasing targets .

