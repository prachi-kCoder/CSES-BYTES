# REMOVING DIGITS : Optimal digit to be reduced to get the minOperation count to reach n 
### Imagine you're standing on a number line at position n, and your goal is to reach 0. At each step, you're allowed to subtract one of the digits of your current number—any non-zero digit.
🧮 Key Insight
Let dp[i] represent the minimum number of steps to reach i from 0. We build the answer incrementally from the ground up:
For every number i from 1 to n, we do the following:
  Look at each digit d in i.
Try subtracting d to reach a smaller number i - d.
Update dp[i] by choosing the minimum of all such paths:
### dp[i] =  min( dp[i] , dp[i-d] + 1 )

By the time you reach n, dp[n] holds the optimal answer—the fewest number of steps to reduce it to 0

```cpp

#include <bits/stdc++.h>
using namespace std;
typedef long long ll ;
int main() {
    int n ;
    cin >> n ;
    vector<ll> dp(n + 1 , 1e9 + 7);
    dp[0] = 0LL ;
    
    for (int i = 1 ; i <= n ; i++) {
        int num = i ;
        while (num > 0) {
            int d = num%10 ;
            if (d > 0) {
                dp[i] = min(dp[i] , dp[i-d] + 1);
            }
            num /= 10 ;
        }
    }
    cout << dp[n] << endl ;
    
}
```


