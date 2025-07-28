# FLIGHT-DISCOUNT

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define inf 1e18
vector<vector<pair<int,int>>> adj , revAdj;
vector<ll> d, dRev ;
void djiktra(int node) {
    d[node] = 0LL ;
    // priority_queue<pair<ll,int>, vector<pair<ll,int>> , greater<pair<ll,int>>> pq ;
    set<pair<ll,int>> pq ;
    pq.insert({0LL , node});
    
    while (!pq.empty()) {
        // auto [cost , u] = pq.top(); pq.pop();
        int u = pq.begin()->second ;
        pq.erase(pq.begin());
        
        if (d[u] == inf) continue ;
        for (auto [v ,wt] : adj[u]) {
            if (d[v] > d[u] + wt) {
                pq.erase({d[v], v});
                d[v] = d[u] + wt ;
                pq.insert({d[v] , v});
            }
        }
    }
}
void djiktraRev(int node) {
    dRev[node] = 0LL ;
    // priority_queue<pair<ll,int>, vector<pair<ll,int>> , greater<pair<ll,int>>> pq ;
    set<pair<ll,int>> pq ;
    pq.insert({0LL ,node});
    while (!pq.empty()) {
        // auto [cost , u] = pq.top(); pq.pop();
        int u = pq.begin()->second;  
        pq.erase(pq.begin());

        if (dRev[u] == inf) continue ;
        for (auto [v ,wt] : revAdj[u]) {
            if (dRev[v] > dRev[u] + wt) {
                pq.erase({dRev[v] , v}) ;
                
                dRev[v] = dRev[u] + wt ;
                pq.insert({dRev[v] , v});
            }
        }
    }
}
int main() {
    int n , m;
    cin >> n >> m ;
    adj.resize(n) ; revAdj.resize(n) ;
    for (int j = 1 ; j <= m ; j++) {
        int a , b , c ;
        cin >> a >> b >> c ;
        a-- ; b-- ;
        adj[a].push_back({b,c});
        revAdj[b].push_back({a,c});
    }
    d.assign(n, inf);
    dRev.assign(n, inf);
    djiktra(0);
    djiktraRev(n-1);
    
    ll res = inf ;
    for (int u = 0; u < n ; u++) {// all edges start from [0-u] to edges 
        if (d[u] == inf) continue ;
        for (auto [v,wt] : adj[u]) {
            if (dRev[v] == inf) continue ;
            res = min(res , d[u] + wt/2 + dRev[v]) ;
        }
    }
    cout << res << endl ;
    return  0 ;
}

```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |    2*O( N+M) + 2*((N+M)*logN) + O(N+M)  = O((N+M) * logN)   | Adj, RevAdj formations + Djiktra over N,M edges + Final coupona appliying |
| 🧠 SPACE |   O(N+M) + O(N)  = O(N+M)  |  Adj Lists + dist & revDist |

- Djiktra Complexicity  =   O((N+M)*logN) Graph elements = N+M and insertions / deletion in PQ/SET(Balanced BST) is log N per operation .
