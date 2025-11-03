# Prime-Multiples

-  .The Core Intuition: Fixing OvercountingThe problem is to count numbers that are in at least one group.
-  Group A: Multiples of Group B: Multiples of `p_2`...and so on.
-  The simplest approach is to just add them all up:total = (n/p1) + (n/p2) + (n/p3) + ...Problem: As you noted, a number like $p_1 \times p_2$ (a multiple of both) got counted twice.The Fix (Your Intuition):
-  "Okay, I'll subtract all the pairs.
-
-
```
-  total = (n/p1) + (n/p2) + (n/p3)
-  total -= (n / (p1*p2))
-  total -= (n / (p1*p3))
-  total -= (n / (p2*p3))

But consier a number like p1 =5 , p2 = 11 , p3 = 13
n upto 2000 ,
For a number = 715
Count by 5 ,11, 13 all -> +3 counts
Then sub by (5,11) pair -1
Then sub by (11,13) pair -1 
Then sub by (5,13) pair -1

Hence 715 completely vanieshed from cnt so to include it we need to add its count
That is where the intuition of INCLUSION-EXCLUSION comes in
```

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
int main() {
    ll n , k ;
    cin >> n >> k ;
    vector<ll> a(k);
    for (ll j = 0 ; j < k ; j++) {
        cin >> a[j] ;
    }
    ll total = 0LL ;
    
    // all non-empty sets 
    for (ll mask = 1 ; mask < (1<<k) ; mask++) {
        ll prod = 1LL ;
        bool no_need = false ;
        ll cnt = 0; 
        for (int j = 0 ; j < k ; j++) {
            if (mask&(1<<j)) {
                if (prod > (n/a[j])) {// to  check for overflow 
                    no_need = true ;
                    break ;
                }
                prod = 1LL*a[j]*prod ;
                cnt++ ;
            }
        }
        if (no_need) continue ;
        // odd cnt of factors
        if (cnt%2) {
            total  +=  (n/prod) ;
        } else {
            total  -=  (n/prod) ;
        }
    }
        
    cout << total << endl ;
    
    return 0 ;
}

```
