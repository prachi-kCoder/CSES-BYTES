# BUILDING TEAMS 
### INTUITION : Check for the bipartiteness of the graph 
-  Code should be such that it could handle disconnected graphs as well .
## BFS APPROACH 
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
## DFS APPROACH 
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
#define pb push_back 

const int N = (int)1e5 + 5 ;
vector<int> adj[N] ;
bool dfs(int node ,int par, vector<int>& team) {
    bool possible = true ;
    team[node] = par == -1 ? 1 : (team[par] == 1 ? 2 : 1) ;
    for (int nbr : adj[node]) {
        if (team[nbr] == 0) {
            if (!dfs(nbr ,node, team)){
                possible = false ;
                break ;
            }
        }else if (team[nbr] == team[node]) {
            possible =false ;
            break ;
        }
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
	        possible = dfs(i, -1 , team) ;
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
| Complexity Analysis  | BigO       | HOW ?  |
|----------------------|------------|-------|
| BFS                  |            |       |
| ⏱️ Time 	       | O( n + m ) |  n vertices , m edges |
| 🧠 Space  	       | O( n + m ) |  n , m + Queue O(n) |
| DFS                  |            |       |
| ⏱️ Time 	       | O( n + m ) |  n vertices , m edges  |
| 🧠 Space  	       | O( n + m ) |  n , m + Rec-Stack O(n)|

## ⚠️ When to Prefer One Over the Other
- Use DFS: when problem needs recursive intuition, or you’re chaining DFS into another logic (like tree DP, bridge finding, etc.)
- Use BFS: when you expect deep graphs, or want iterative safety under large input sizes (e.g. CSES constraints ~1e5+)
