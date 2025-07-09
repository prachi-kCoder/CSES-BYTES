# SHORTEST ROUTE 1 

## We have positive weightes graph -> That is Djiktra 
## Apply Djiktra but wisely so that to remove the redundant entries , 
###  Replace priority_queue <-> set to have no duplicates and erase the prev redundant pair of prev entry !
```cpp
#include <bits/stdc++.h>
using namespace std;
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0)
#define F first 
#define S second 
#define ll long long
#define pll pair<ll, ll>
const int N = 1e5 + 5 ;
ll dist[N] ;
vector<pll> adj[N] ; 

void djiktra(int src) {
    dist[src] = 0LL ;
    
    set<pll> s;
    s.insert({0LL, src});
    
    while (!s.empty()) {
        ll u = s.begin()->second ;
        s.erase(s.begin()) ;
        
        for (auto edge : adj[u]) {
            ll v = edge.first ;// wt
            ll wt = edge.second ;// v 

            if (dist[u] + wt < dist[v]) {
                s.erase({dist[v], v});
                dist[v] = dist[u] + wt;
                s.insert({dist[v], v});
            }
        }
    }
}
int main() {
    FASTIO ;
    int n , m ;
    cin >> n >> m ;
    
    for (int i = 0; i < m ; i++) {
        int a , b , c ;
        cin >> a >> b >> c ;
        a-- , b-- ;
        adj[a].push_back({b,c});
    }
    fill(dist , dist + n , LLONG_MAX) ;
    dist[0] = 0 ;
    djiktra(0) ;
    
    for (int i = 0; i < n ; i++) {
        cout << dist[i] << " " ;
    }
    
    return 0 ;
}
```

## 🧮 Complexity Analysis: Dijkstra with `set<pair<ll, ll>>`

We are implementing Dijkstra's algorithm using an ordered `set` as a min-priority queue substitute. Below is the time and space complexity breakdown.

| Metric    | Complexity       | Explanation                                                                 |
|-----------|------------------|-----------------------------------------------------------------------------|
| **Time**  | O((N + M)·log N) | For each vertex and edge, we perform set insertions/removals (log N time). |
| **Space** | O(N + M)         | `adj[]` stores all edges (O(M)), `dist[]` and `set` hold up to N elements. |

### ⏱ Why Time is O((N + M)·log N)
- There are up to **N** nodes and **M** edges.
- Each node can be inserted into the set multiple times due to updates.
- Insert, erase, and find operations in a set each take **O(log N)**.
- In total, each edge is considered once, and we may insert a node into the set O(deg(node)) times.

So, total operations ≈ O((N + M) log N)

### 📦 Why Space is O(N + M)
- `adj[N]`: Adjacency list to store edges → O(M)
- `dist[N]`: Stores shortest path estimate → O(N)
- `set<pair<ll, int>>`: At most N elements at any time → O(N)

Hence, space complexity = O(N + M)
