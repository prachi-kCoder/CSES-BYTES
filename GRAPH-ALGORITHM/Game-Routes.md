# GAME ROUTES 
- BRUTE FORCE : Normal DFS / BFS (as soon as node == Nth node the cnt increases ) but this method undergoes TLE !

✅ Intuition :
- Since the graph is a DAG, we know there are no cycles, so every node can be ordered such that all its dependencies come before it.
- This ordering — the topological sort — ensures that when we process a node u, all paths leading to u have already been counted.
- This is crucial because we want to compute dp[u] (number of ways to reach u) before propagating it to its neighbors.

```
dp[v] = (dp[u] + dp[v])%mod  # this is should be done only when the dp[u] is finalized and its made possible with TOPOLOGICAL Order !
```
## BFS KAHN'S ALGO
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define mod 1000000007
vector<vector<int>> adj ;
 
int main() {
    int n , m ;
    cin >> n >> m ;
    
    adj.resize(n);
    vector<int> in_deg(n,0) ;
    for (int i = 0 ; i < m ; i++) {
        int a , b ;
        cin >> a >> b ;
        a-- , b-- ;
        adj[a].push_back(b) ;
        in_deg[b]++ ;
    }
    // solve(0 , -1 , n-1) ;
    queue<int> q ;
    for (int i = 0; i < n ; i++) {
        if (in_deg[i] == 0) {
            q.push(i) ;
        }
    }
    vector<int> topo ;
    while (!q.empty()) {
        int u = q.front() ; q.pop();
        topo.push_back(u) ;
        
        for (int v : adj[u]) {
            in_deg[v]-- ;
            if (in_deg[v] == 0) {
                q.push(v);
            }
        }
    }
   
    
    vector<ll> dp(n , 0LL) ; 
    // ways to reach any point: Topo order gurantees the right order as they can be visited 
    dp[0] = 1LL ; // first node 
    for (int u : topo){
        for (int v : adj[u]) {
            dp[v] = (dp[v] + dp[u])%mod ;
        }
    }
    cout << dp[n-1] << endl ;
    
    return  0 ;
}
```
## DFS TOPO
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define mod 1000000007
vector<vector<int>> adj ;
void get_topo(int node , vector<int>& topo, vector<bool>& vis) {
    // dfs for nbr first 
    vis[node] = true ;
    for (int nbr : adj[node]) {
        if (!vis[nbr]) {
            get_topo(nbr , topo, vis) ;
        }
    }
    topo.push_back(node) ;
}
int main() {
    int n , m ;
    cin >> n >> m ;
    
    adj.resize(n);
    for (int i = 0 ; i < m ; i++) {
        int a , b ;
        cin >> a >> b ;
        a-- , b-- ;
        adj[a].push_back(b) ;
    }
    vector<int> topo ;
    
    vector<bool> vis(n , false) ;
    get_topo(0 , topo , vis) ;
    reverse(topo.begin() , topo.end());
    

    
    vector<ll> dp(n , 0LL) ;
    dp[0] = 1LL;
    for (int u : topo) {
        for (int v : adj[u]) {
            dp[v] = (dp[v] + dp[u])%mod ;
        }
    }
    cout << dp[n-1] << endl ;
	return 0 ;

}
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(V+E)    |   BFS Kahn' Algo + DP all v nodes in topological order add to count for all nbr (e edges)   |
| 🧠 SPACE |     O(V+E)       | Adj List , O(n) for Dp table           |
