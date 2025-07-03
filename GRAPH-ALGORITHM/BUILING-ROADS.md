# 
### DFS Approach 
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_base(0) , cin.tie(0) , cout.tie(0)
#define pb push_back
using namespace std;
const int N = 1e5 + 5 ;
vector<int> adj[N] ;

void dfs(int node , vector<bool>& vis) {
    vis[node] = true ;
    for (int nbr : adj[node]) {
        if (!vis[nbr]) {
            dfs(nbr , vis) ;
        }
    }
}
int main() {
    int n , m ;
    cin >> n >> m ;
    
    for (int j = 0; j < m ; j++) {
        int u , v ;
        cin >> u >> v ;
        adj[u].pb(v) ;
        adj[v].pb(u) ;
    }
    vector<bool> vis(n+1, false) ;
    vector<int> res ;
    for (int i = 1 ; i<= n ; i++) {
        if (!vis[i]) {
            res.pb(i) ;
            dfs(i , vis) ;
        }
    }
    cout << res.size()-1 << endl ;
    for (int i = 0; i<res.size()-1 ; i++) {
        cout << res[i] << " " << res[i+1] << endl ;
    }
    return 0 ;
}

```
### DISJOINT SET UNION (DSU - Approach)
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_base(0) , cin.tie(0) , cout.tie(0)
using namespace std;
class DSU {
    vector<int> rank , par ;
public :
    DSU (int n ) {
        rank.resize(n+1, 0);
        par.resize(n+1);
        for (int i = 1 ; i <= n ; i++) {
            par[i] = i ;
        }
    }
    int find(int x) {
        if (par[x] == x) return x ;
        return par[x] = find(par[x]) ;
    }
    void unite(int a , int b) {
        int pa = find(a) ;
        int pb = find(b) ;
        if (pa == pb) return ;
        if (rank[pa] > rank[pb]){
            par[pb] = pa ;
        }else if (rank[pb] > rank[pa]) {
            par[pa] = pb ;
        }else {
            rank[pa]++;
            par[pb] = pa ;
        }
    }
};
int main() {
    int n , m ;
    cin >> n >> m ;
    DSU dsu(n) ;
    for (int j = 0; j < m ; j++) {
        int u , v ;
        cin >> u >> v ;
        int pu = dsu.find(u) ;
        int pv = dsu.find(v) ;
        if (pu == pv) continue ;
        dsu.unite(pu , pv) ;
    }
    vector<pair<int,int>> res ;
    for (int i = 1; i <n ; i++) {
        int a = i , b = i+1 ;
        int pa = dsu.find(a) , pb = dsu.find(b) ;
        if (pa == pb) continue ;
        res.push_back({a,b}) ;
        dsu.unite(pa, pb) ;
    }
    cout << res.size() << endl ;
    for (auto e : res) {
        cout << e.first <<" "<< e.second << endl ;
    }
    return 0 ;
}
```
## 🚀 Complexity Analysis

### ⏱ Time Complexity

| Approach | Time Complexity |
|----------|------------------|
| **DFS**  | O(n + m), since each node and edge is visited once |
| **DSU**  | O((n + m) × α(n)), where α(n) is the inverse Ackermann function |

### 📦 Space Complexity

| Approach | Space Breakdown |
|----------|-----------------|
| **DFS**  | adj: O(n + m), vis: O(n), res: O(k) |
| **DSU**  | rank + par: O(2n), res: O(k) |

> ✅ DSU is better when dynamic connectivity is required.
> But for one-time component analysis, DFS is more intuitive and just as efficient.

