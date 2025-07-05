# BUILDING TEAMS 
### INTUITION : Check for the bipartiteness of the graph 
### Code should be such that it could handle disconnected graphs as well .
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
#define pb push_back 

const int N = (int)1e5 + 5 ;
vector<int> adj[N] ;
bool bipartite(int node , vector<int>& team) {
    queue<int> q ;
	q.push(node)  ;
	team[node] = 1 ;
	bool possible = true ;
	
	while (!q.empty()) {
	    int c = q.front();
	    q.pop();
	    for (int v : adj[c]) {
	        if (team[v] == 0) {
	            team[v] = team[c] == 1 ? 2 : 1 ;
	            q.push(v) ;
	        }else if (team[v] == team[c]) {
	            possible = false ;
	            break;
	        }
	    }
	    if (!possible) break ;
	}
	return possible ;
}
int main() {
	FASTIO ;
	int n , m ;
	cin >> n >> m ;
	// 2 Team division-> Check Bipartite or not 
	for (int j = 0; j < m ; j++) {
	    int u , v ;
	    cin >> u >> v ;
	    adj[u].pb(v);
	    adj[v].pb(u);
	}
	if (n == 1) {
	    cout << 1 << endl ;
	    return 0 ;
	}
	vector<int> team(n+1 , 0) ;// unAssigned
	bool possible = true ;
	for (int i = 1 ; i <= n ; i++) {
	    if (team[i] == 0) {
	        possible = bipartite(i , team) ;
	        if (!possible) break ;
	    }
	}
	
	if (!possible) {
	    cout << "IMPOSSIBLE" <<endl ;
	}else {
	    for (int i = 1; i<= n;i++) {
	        cout << team[i] << " " ;
	    }
	    cout << endl ;
	}
	
}
```
| Complexity Analysis | BigO  | HOW ? |
| ⏱️ Time  | O( n + m ) |  n vertices , m edges |
| 🧠 Space  | O( n + m ) |  n vertices , m edges |
