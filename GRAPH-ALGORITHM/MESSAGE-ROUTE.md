## MESSAGE - ROUTE 

```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0), cout.tie(0)
#define pb push_back
#define F first
#define S second
using namespace std;
const int N = 1e5 + 5 ;
vector<int> adj[N] ;
bool vis[N] ;
int main() {
	FASTIO ;
	int n , m ;
	cin >> n >> m ;
	
	for (int i = 0; i < m ; i++) {
	    int u , v;
	    cin >> u >> v ;
	    adj[u].pb(v) ;
	    adj[v].pb(u) ;
	}
	if (n == 1) {
	    cout << 1 << endl ;
	    return 0 ;
	}
	vector<int> par(n+1) ;
	
	queue<int> q ;
	par[1] = -1 ;// topMost
	vis[1] = true ;
	q.push(1) ;
	bool found = false ;
	
	while (!q.empty()) {
	    int sz = q.size() ;
	    
	    for (int i = 0 ; i < sz ; i++) {
	        int c = q.front();
	        q.pop();
	        
	        for (int nbr : adj[c]) {
	            if (vis[nbr]) continue ;
	            vis[nbr] = true ;
	            par[nbr] = c ;
	            cout << "Making " << c << " parof" << nbr << endl ;
	            if (nbr == n) {
	                found = true;
	                break ;
	            }else {
	                q.push(nbr);
	            }
	        }
	        if (found) break ;
	    }
        if (found) break ;
	}
	if (!found) {
	    cout << "IMPOSSIBLE" << endl ;
	}else {
	    vector<int> path ;
	    for (int i = n ; i != -1 ; i = par[i]) {
	        path.pb(i) ;
	    }
	    reverse(path.begin() , path.end()) ;
	    cout << path.size() << "\n";
        for (int node : path) cout << node << " ";
        cout << "\n";
	}
	return 0 ;
}
```
