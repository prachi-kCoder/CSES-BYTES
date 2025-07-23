# SHORTEST-ROUTES II

## FLOYD'S WARSHALL ALGORITHM
- Take every node k as a mid node between other 2 nodes(i , j) if the try to minimise the distance b/w i & j

```cpp
#include <bits/stdc++.h>
#define ll long long 
using namespace std;

int main() {
	int n , m , q ;
	cin >> n >>  m >> q ;
	vector<vector<ll>> dist(n , vector<ll>(n , LLONG_MAX )) ;
	
	for (int j = 1 ; j<=m ; j++) {
	    int a , b , c ;
	    cin >> a >> b >> c ;
	    a-- ; b-- ;
	    dist[a][b] = min(dist[a][b] ,(ll)c) ;
	    dist[b][a] = min(dist[b][a] ,(ll)c) ;
	}
	
	for (int i = 0; i < n ; i++) dist[i][i] = 0LL ;
	
	for (int k = 0; k < n ; k++) {
    	for (int i = 0; i < n ; i++) {
	        for (int j = 0 ; j < n ; j++) {
	            if (i == j) continue ;
	            if (dist[i][k] != LLONG_MAX&& dist[k][j] != LLONG_MAX ) {
	                dist[i][j] = min(dist[i][j] , dist[i][k] + dist[k][j]);
	            }
	        }
	    }
	}
	
	for (int i = 0; i <q ; i++) {
	    int x , y ;
	    cin >> x >> y ;
	    x-- ; y-- ;
	    cout << (dist[x][y] == LLONG_MAX ? -1 : dist[x][y]) << endl ;
	}
}
```


# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N^3)     |  Triple nested loop for each intermediate node k, checking all pairs (i, j) to update shortest paths |
| 🧠 SPACE |  O(N^2)    |    Dist matrix stores shortest path between every pair of nodes     |

