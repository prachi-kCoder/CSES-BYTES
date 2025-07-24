## HIGH SCORE 
- Keep in mind don't forget to check for the nodes are reachable from start / end or not before doing relaxation , ie in order to maximise score[v] = score[u] + x , then first check u is reachable from start & v reaachable to end
- APPLY BELLMAN FORD
- Do check for arbitrarily infinite score /
```cpp
#include <bits/stdc++.h>
#define ll long long
const ll INF = 1e18 ;
using namespace std;
 
vector<vector<pair<int,int>>> adj ;
vector<vector<int>> rev_adj ;
vector<bool> reachable_from_start ;
vector<bool> reachable_to_end ;
 
void dfs_from_start(int node) {
    reachable_from_start[node] = true ;
    for (auto nxt : adj[node]) {
        int v = nxt.first ;
        if (!reachable_from_start[v]) {
            dfs_from_start(v) ;
        }
    }
}
void dfs_from_end(int node) {
    reachable_to_end[node] = true ;
    for (int v : rev_adj[node]) {
        if (!reachable_to_end[v]) {
            dfs_from_end(v);
        }
    }
}
int main() {
	int n , m ;
	cin >>  n >> m ;
	adj.resize(n);
	rev_adj.resize(n);
	
	for (int  j = 1 ; j <= m ; j++) {
	    int a , b , x ;
	    cin >> a >> b >> x ;
	    a-- ; b-- ;
	    adj[a].push_back({b, x}) ;
	    rev_adj[b].push_back(a) ;
	}
	
	reachable_from_start.resize(n , false );
	reachable_to_end.resize(n , false );
	
	dfs_from_start(0);
	dfs_from_end(n-1);
	
	vector<ll> score(n, -INF) ;
	score[0] = 0LL ;
	
	for (int i = 0 ;i < n-1 ; i++) {
	    for (int u = 0;  u < n ; u++) {
	        if (score[u] == -INF) continue ;
	        
	        for (auto p : adj[u]) {
	            int v = p.first ; int x = p.second ;
	            if (score[u] + x > score[v]) {
	                score[v] = score[u] + x  ;
	            }
	        }
	    }
	}
	// check for -1 
	bool infiniteScore = false ;
	
	for (int u = 0;  u < n ; u++) {
	   if (score[u] == -INF) continue ; 
	   
	   for (auto p : adj[u]) {
	       int v = p.first ; int x = p.second ;
	       if (score[v] < score[u] + x) {
	            if (reachable_from_start[u] && reachable_to_end[v]) {
	                infiniteScore = true ;
	                break ;
	            }
	        }
	   }
	   if (infiniteScore) break ;
    }
    if (infiniteScore) {
        cout << -1 << endl ;
    }else {
        if (score[n-1] == -INF) {
            cout << -1 << endl;
        }else {
            cout << score[n-1] << endl;
        }
    }
    return 0 ;	
}
```


# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O( 2*(n + m) + (n-1)*(n+m))   | dfs (From start & end) ,  n-1 Interations , All reachable node visit the reachable edges |
| 🧠 SPACE |   O(2*(n + m))  + 2*O(n)  | Adj + revAdj +  reachable bool arrays   |
