# RESTAURANT CUSTOMERS : Keep max count of customers at any time 


## APPLY SWEEP - LINE APPROACH : 
```cpp
#include <bits/stdc++.h>
#define ll long long
#define M 1000000009
using namespace std;

int main() {
    int n ;
    cin >> n ;
    // sweep line ;
    map<ll,ll> mp ;
    for (int i = 0; i < n ; i++) {
        ll a , b ;
        cin >> a >> b ;
        mp[a]++ ; mp[b]-- ;
    }
    
    ll ans = 0 , curr = 0 ;
    for (auto p : mp){
        curr += mp[p.first] ;
        ans = max(ans , curr) ;
    }
    cout << ans << endl ;
    return 0;
}

```
### Complexicity Analysis :
## 🕓 Time Complexity : O(nlogn) 
## 💾 Space Complexity : O(n)


## APPROACH 2 : Sorting the events based on start time  :-
```cpp
#include <bits/stdc++.h>
#define ll long long
using namespace std;

int main() {
    int n ;
    cin >> n ;
    vector<pair<ll,int>> events ;
    for (int i = 0; i < n ; i++) {
        ll a , b ;
        cin >> a >> b ;
        events.push_back({a,+1});
        events.push_back({b,-1});
    }
    sort(events.begin() , events.end()) ;
    
    ll ans = 0 , curr = 0 ;
    for (auto p : events) {
        curr += p.second ;
        // +1 if any event started , -1 on end of event 
        ans = max(ans , curr) ;
    }
    cout << ans << endl ;
    
    return 0;
}

```
### COMPLEXICITY ANALYSIS :
- Slightly faster than map because sort() has less overhead than log-time insertions.
- ## 🕓 Time Complexity : O(nlogn) 
## 💾 Space Complexity : O(n)
- 

