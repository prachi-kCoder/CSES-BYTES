# ROUND - TRIP 
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
const int N = 1e5 + 5 ;
vector<int> adj[N] ;
bool vis[N] ;
bool cyclic(int node , int par, vector<int>& path) {
    path.push_back(node) ;
    vis[node] = true ;
    
    for (int nbr : adj[node]) {
        if (nbr == par) continue ;
        if (vis[nbr] ) {
            path.push_back(nbr) ;
            return true ;
        }else if (!vis[nbr]) {
            if (cyclic(nbr ,node, path)) return true ;
        }
    }
    path.pop_back();
    return false ;
}
int main() {
    FASTIO ;
    int n , m ;
    cin >> n >> m;
    for (int i = 0; i < m ; i++) {
        int a ,  b ;
        cin >> a >> b;
        adj[a].push_back(b) ;
        adj[b].push_back(a) ;
    }
    
    // For print any cyclic component !
    bool found = false ;
    for (int i = 1 ; i <= n ; i++) {
        if (!vis[i]) {
            vector<int> path ;
            if (cyclic( i, -1 ,path)) {
                int k = path.size() , i = 0 ;
                int stNode = path[k-1] ;
                while (i < k && path[i] != stNode) i++ ;
                cout << k - i << endl;
                for (int j = i ; j < k ; j++) {
                    cout << path[j] << " " ;
                }
                cout << endl ;
                found = true ;
                break ;
            }
        }
    }
    if (!found) {
        cout << "IMPOSSIBLE" << endl ;
    }
    
    return  0 ;
}
```

## COMPLEXICITY ANALYSIS 
|  Metric  | Complexicity     |  HOW ?    |
|----------|------------------|-----------|
| TIME     |  O(n + m)        | O(n) for construction , O(n) for recursion depth |
| SPACE    |  O(n + n + n)    | Adj List O(n) , vis -> O(n) , path (O(n)) |
