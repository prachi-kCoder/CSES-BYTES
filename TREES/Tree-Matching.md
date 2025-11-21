# Tree-Matching
```
- Get all matching pairs starts to form by Post order traversal ,
- and iff the any next child may be a leaf node or a non-leaf unpaired nbr/child is available to make a pair make one
-  else return false if couldn't form a pair for any ith node .
```

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define pll pair<ll,ll> 
vector<vector<ll>> adj ;
vector<pll> p ;
bool dfs(ll node , vector<bool>& vis) {
    vis[node] = true ; 
 
    ll single = -1 ;
    for (ll v : adj[node]) {
        if (!vis[v]) {
            if (!dfs(v , vis ) && single == -1) {
                // couldn't make a pair!
                single = v ;
            }
        }
    }
    if (single != -1) {
        vis[single] = true ;
        // cout << "for node :" << node+1 << endl ;
        // cout << "pair :" << single+1 << endl ;
        p.push_back({node , single});
        return true ; // ie successfully made a pair !
    }
    return false ; //couldn't make a pair !
}
int main() {
	ll n ;
	cin >> n ;
	adj.resize(n);

	for (ll i = 0; i < n-1 ; i++) {
	    ll a , b ;
	    cin >> a >> b ;
	    a-- , b-- ;
	  
	    adj[a].push_back(b);
	    adj[b].push_back(a);
	}
	
	vector<bool> vis(n , false) ;
	dfs(0 , vis ) ;
	ll c = p.size() ;// all pairs your can simple take a counter as well 
	cout << c << endl ;
	return 0 ;

}
```

## TC : O(N)
## SC : O(N)
