# SLIDING WINDOW SUM 
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
#define ll long long 
const int N = 1e7 + 1 ;
int v[N] ;
ll pSum[N] ;
 
int main() {
    FASTIO ;
    int n , k ;
    cin >> n >> k ;
    int x , a, b, c ;
    cin >> x >> a >> b >> c ;
    v[0] = x ;
    for (int i = 1 ; i < n ; i++) {
        v[i] = (1LL*v[i-1]*a + b)%c ;
    }
    if (n == 1) {
        cout << 1 << endl;
        return 0;
    }
    ll XOR = 0LL ;
    pSum[0] = v[0] ;
    for (int i = 1 ; i < n; i++) {
        pSum[i] = pSum[i-1] + 1LL*v[i] ;
        
        if (i >= k-1) {
            int l = i-k;
            if(l >= 0) {
                XOR ^= (pSum[i] - pSum[l]) ;
            }else {
                XOR ^= pSum[i] ;
            }
        }
    }
    
    cout << XOR << endl;
	return 0 ;
}
```
## COMPLEXICTY ANALYSIS 
| METRIC    |  COMPLEXICITY   | HOW ?  |
|-----------|------------------|--------|
| TIME      |  O(n + n) = O(2*n) | Formations of v + PrefixSum Traversal |
| SPACE     |  O(n + n) = O(2*n) | Vector for v , prefixSum   |

### SPACE OPTIMISED APPROACH : Without using prefixSum Array  
- Space COMPLEXICITY : O(n)
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
#define ll long long 
const int N = 1e7 + 1 ;
int v[N] ;
int main() {
    FASTIO ;
    int n , k ;
    cin >> n >> k ;
    int x , a, b, c ;
    cin >> x >> a >> b >> c ;
    v[0] = x ;
    
    for (int i = 1 ; i < n ; i++) {
        v[i] = (1LL*v[i-1]*a + b)%c ;
    }
    if (n == 1) {
        cout << 1 << endl;
        return 0;
    }
    ll XOR = 0LL ;
    ll sum = v[0] ;
    
    for (int i = 1 ; i < n ; i++) {
        sum =  sum + 1LL*v[i] ;
        if ( i >= k-1 ) {
            int l = i-k ;
            if(l >= 0) {
                sum -= v[l] ;
            }
            XOR ^= sum ;
        }
    }
    
    cout << XOR << endl;
	return 0 ;
}
```
