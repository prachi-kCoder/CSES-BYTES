## SUM OF 2 VALUES 

```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0), cin.tie(0) , cout.tie(0)
using namespace std;
#define pb push_back
#define F first
#define S second
const int N = (int)2e5 + 5 ;

int main() {
    FASTIO ;
    int n , x ;
    map<int,vector<int>> mp;
    cin >> n >> x ;
    for (int i = 1 ; i<= n ; i++) {
        int e ;
        cin >> e ;
        mp[e].pb(i) ;
    }
    for (auto p : mp) {
        int e1 = p.F ;
        if (mp.find(x - e1) == mp.end()) continue ;
        if ( x-e1 == e1 ) {
           if (mp[e1].size() == 1) continue ;
           cout << mp[e1][0] << " " << mp[e1][1] << endl ;
           return 0;
        }else {
           cout << mp[e1][0] << " " << mp[x - e1][0] << endl ;
           return 0;
        }
    }
    cout << "IMPOSSIBLE" << endl ;
    return 0 ;
}

```
