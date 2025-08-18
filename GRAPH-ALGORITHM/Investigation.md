## Investigation

```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
const int mod = 1000000007 ;
class Pair{
public :
    ll d ; int mnf ; int mxf ; ll cnt ;
    Pair(ll d ,int mnf , int mxf , ll cnt) : d(d) , mnf(mnf) , mxf(mxf) , cnt(cnt) {} 
 
};
vector<vector<pair<int,int>>> adj ;
 
int main() {
	int n , m ;
	cin >> n >> m ;
	adj.resize(n) ;
 
	
	for (int j = 1 ; j <= m ; j++) {
	    int a , b , c ;
	    cin >> a >> b >> c ;
	    a-- , b-- ;
	    adj[a].push_back({b,c});
	}
	// min_flight ,mxflight cnt 
	// bfs 
	priority_queue<pair<ll,int>,vector<pair<ll,int>>, greater<pair<ll,int>>> pq ;
	pq.push({0LL , 0}); 
	vector<Pair*> dist(n)  ;
	// init 
	for (int i = 0 ; i < n ; i++) {
	    dist[i] = new Pair(LLONG_MAX , m , 0 , 0LL) ;
	}
	
	dist[0] = new Pair(0LL , 0 , 0 , 1LL)  ;
	
	while (!pq.empty()) {
	    auto [curr_dist,u] = pq.top() ; pq.pop();
	    
	    if (curr_dist > dist[u]->d) continue ;
	    
	    for (auto [v,wt] : adj[u]) {
	        if (dist[v]->d > dist[u]->d + wt ) {
	            dist[v]->d = dist[u]->d + wt ; // dist 
	            dist[v]->mnf = dist[u]->mnf + 1 ;
	            dist[v]->mxf = dist[u]->mxf + 1 ;
	            dist[v]->cnt = dist[u]->cnt ; // new min_dist 
 
	            pq.push({dist[v]->d , v }) ;
	        }else if (dist[v]->d == dist[u]->d + wt ) {
	            dist[v]->mnf = min(dist[u]->mnf + 1 , dist[v]->mnf) ;
	            dist[v]->mxf = max(dist[u]->mxf + 1 ,dist[v]->mxf) ;
	            dist[v]->cnt = (dist[v]->cnt + dist[u]->cnt )%mod ;
	        }
	    }
	}
	
	cout << dist[n-1]->d << " " << dist[n-1]->cnt << " " << dist[n-1]->mnf << " " <<  dist[n-1]->mxf  << endl ;
	
	return  0 ;
}
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |  O(ElogV) | Each edges can cause PQ push , Since the queue is keyed by vertex distance , so each operation is LogV . O(ElogV) as for each edges can cause push in PQ, Total O(E) , Each push/pop O(logV) |
| 🧠 SPACE |    O(V+E)      | Priority queue + AdjList + dist[N] |

