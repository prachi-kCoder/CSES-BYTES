# MONEY SUMS 

```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0)
using namespace std;
#define ll long long 
const int N = 1e5 + 1 ;// max Total 
bool dp[N] ;
int c[101] ;
int main() {
    FASTIO ;
    int n ;
    cin >> n ;
    ll total = 0LL; 
    for (int i = 0 ; i < n ; i++) {
        cin >> c[i] ;
        total += c[i] ;
    }
    sort(c , c + n) ;
    dp[0] = true ;
    int cnt = 0 ;
    for (int i = 0; i < n ; i++) {
        int coin = c[i] ;
        for(int j = total ; j>= coin ; j--) {
            if (!dp[j]) {
                dp[j] = (dp[j]|dp[j-coin]) ;
                cnt += dp[j] ;
            }
        }
    }
    cout << cnt << endl ;
    for (int j = 1 ; j<=total ; j++) {
        if (dp[j]) {
            cout << j << " ";
        }
    }
    cout << endl ;   
    return 0 ;
}
```


```cpp
#include <bits/stdc++.h>
#include <bitset>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0)
using namespace std;
#define ll long long 
const int N = 1e5 + 1 ;// max Total 
bitset<N> dp ;
int c[101] ;
int main() {
    FASTIO ;
    int n ;
    cin >> n ;
    ll total = 0LL; 
    for (int i = 0 ; i < n ; i++) {
        cin >> c[i] ;
        total += c[i] ;
    }
    sort(c , c + n) ;
    dp.set(0) ;
    for (int i = 0; i < n ; i++) {
        int coin = c[i] ;
        for(int j = total ; j >= coin ; j--) {
            if (dp.test(j-coin)) {
                dp.set(j) ;
            }
        }
    }
    
    cout << dp.count()-1 << endl ;
    for (int j = 1 ; j<=total ; j++) {
        if (dp.test(j)) {
            cout << j << " ";
        }
    }
    cout << endl ;
    
    return 0 ;
}
```

# COMPLEXICITY ANALYSIS
|  METHOD                | METRIC    |   COMPLEXICITY   |    HOW ?  |
|------------------------|------------|-----------------|-----------|
| Method 1  (Bool array) |  ⏱️ Time   |    O(n*totalSum)| for all n coins , check for totalSum |
| M1                     | 🧠 Space  |   O(n + total)  | Array  + Dp Bool Array |
| Method  2 (Bit Set)  |    ⏱️ Time  |   O(n*totalSum) but faster | Bit level operations than of the bool array operations |
| M2                   |    🧠 Space |  O(n + total)  | Array +  DP BitSet |


