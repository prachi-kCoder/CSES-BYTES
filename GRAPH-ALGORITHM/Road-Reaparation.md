# Road-Reaparation

###### VERY IMPORTANT POINTS TO KEEP IN MIND :
- vertex > n-1 is not a safe early termination condition , done fall in this trap , Because connected graph->`MST` has exactly n-1 edges , but if graph is Disconnected ever reach n-1 edges, and early termination will miss valid edges that belong to other components.
-✅ Why you must process all edges (or until n-1 edges are added)
 1) Kruskal’s algorithm sorts edges by weight and greedily adds them if they connect different components.
 2) DSU ensures you don’t form cycles.
 3) You `must attempt every edge` (in sorted order) to ensure:
    - All components are connected as much as possible.
    - You don’t miss valid edges in disconnected graphs.

4) 🔍 Why `vertex < n-1` is essential for final check, not early exit :
5) This check ensures you don’t falsely report MST when the graph is disconnected & using it for early termination is flawed—because you might reach vertex == n-1 in a disconnected graph with multiple small components, and still have unprocessed edges that matter. 
6) DSU : Handles cycle detection

- In c++ use `ranking` rather than rank as it has special meaning in c++ {rank is a standard type trait in <type_traits> used for template metaprogramming.}
- 
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
vector<int> par ;
vector<int> ranking ;

void init(int n) {
    ranking.resize(n ,0) ;
    par.resize(n) ;
    for(int i = 0 ; i < n ; i++) {
        par[i] = i ;
    }
}
int find(int u) {
    if (par[u] == u) return u ;
    return par[u] = find(par[u]) ;
}
void unite(int a , int b) {
    int pa = find(a)  , pb = find(b) ;
    if (pa == pb) return ;
    
    if ( ranking[pa] < ranking[pb] ) {
        par[pa] = pb ;
    }else if (ranking[pa] > ranking[pb]) {
        par[pb] = pa ;
    }else {
        ranking[pb]++ ;
        par[pa] = pb ;
    }
}
int main() {
    int n , m;
    cin >> n >> m ;
    init(n) ;
    vector<vector<int>> edges(m) ;
    for (int j = 1;  j<=m ; j++) {
        int a,  b , c ;
        cin >> a >> b >> c ;
        a-- , b-- ;
        edges[j-1] = {c , a , b} ;
       
    }
    sort(edges.begin() , edges.end()) ;// based on cost 
    // get mst 
    int vertex = 0 ;
    ll min_cost = 0LL ;
    
    for (vector<int> e : edges) {
        int u = e[1] , v = e[2] ;
        ll w = e[0] ;
        int pu = find(u) ;
        int pv = find(v) ;
        if (pu == pv) {
            continue ;
        }
        unite(pu , pv) ;
        vertex++ ;
        min_cost += w ;
    }
    
    
    if ( vertex < n-1 ) { // n-1 edges 
        cout << "IMPOSSIBLE" << endl ;
    }else {
        cout << min_cost << endl ;
    }
    
    return  0;
}

```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(α(N) + M*(LOGM))     |    Sorting edges O(M*LOGM) , Find par O(α(N)) per DSU operation (inverse Ackermann via path compression), total DSU cost is nearly linear. |
| 🧠 SPACE |   O(N + M)     | Par, Ranking , Edges           |
