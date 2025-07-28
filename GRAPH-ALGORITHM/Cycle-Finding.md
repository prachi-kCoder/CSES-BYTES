# CYCLE FINDING

### THINKING PART :
- Neg Cycle as  soon as name comes in  first we think about is "Bellman ford Algo"
- We this time , we don't have any src , rather we 're concerned about detecting negCycle exist and to print to
- Do relaxations (dist[u] + len < dist[v]) over all edges
    -      - n-1 times (as per bellman ford algo)
           - nth iteration check if any edge still is begin relaxed
- Picking up a src  , may lead up to tle / wrong ans as it may happen that graph is disconnected + any one of unreachable component (from selected src ) hsa the neg Cycle .
- Propagate the node where neg Cycle is detected :
-       Bellman-Ford guarantees the existence of a negative cycle if relaxation occurs during the nth iteration — but the node where this happens (x) may not lie inside the cycle. To ensure we're on the cycle, we trace x backward n times via par[x]. This guarantees reaching a node that’s part of the loop
-       This method works for self-loops (u → u) and disconnected components.
-       As any node of cycle is reached by retracing the par we can print the neg cycle
-       dist[i] = 0 (Activate the whole graph) unlike std way of dist[i] = int_max (that is to detect whether any node is reachable from a src), but here we're concermed about any neg cycle .
```cpp
#include <bits/stdc++.h>
#define ll long long
using namespace std;
int main() {
	int n , m  ;
	cin >> n >> m ;
	vector<vector<int>> edges(m) ;
	for (int j = 0; j < m; j ++) {
	    int a , b , c ;
	    cin >> a >> b >> c ;
	    a-- ; b-- ;
	    edges[j] = {a ,b ,c} ;// a->b with len = c 
	}
	
	// Similar intuition as of Bell Man Ford : Do relaxation of edges
	int x = -1 ;
	vector<ll> dist(n,0) ;
	vector<int> p(n,-1) ;
	for (int i = 0; i < n ; i++) {
	    for (vector<int> e : edges) {
	        
	        int u = e[0] ; int v = e[1] ; int len = e[2] ;
	        
	        if (dist[u] + len < dist[v]){
	            dist[v] = len + dist[u] ;
	            p[v] = u ;
	            if (i == n-1 ) x = v ; // for nth iteration
	        }
	    }
	}
	
	if (x == -1) {
	    cout << "NO" << endl ; 
	}else {
	    // Propagation to ensure the x is in the neg cycle (n times)
	    for (int i = 0; i < n ; i++) {
	        x = p[x] ;
	    }
	    int curr = x ;
	    vector<int> negCycle;
	    do {
	        negCycle.push_back(curr) ;
	        curr = p[curr] ;
	    }while (curr != x) ;
	
	    
	    reverse(negCycle.begin() , negCycle.end()) ;
	    
	    cout << "YES" << endl ; 
	    for (size_t i = 0; i < negCycle.size() ;i++) {
	        cout<< (negCycle[i] + 1) << " " ;
	    }
	      
	    cout << (negCycle[0] + 1) << '\n' ;
	}
	return  0 ;
}

```

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N*M)   | N iteration * {Relaxation of all M edges} |
| 🧠 SPACE |   O(M + N + N)     |    Edges, Dist , Par is used      |
