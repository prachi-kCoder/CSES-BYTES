# TREE-DIAMETER

- INTUITION : Get farthest to reach one extreme and then dfs to reach the other farthest extreme end .

```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> adj ;
int dfs(int node , int par  ) {
    int d = 0 ;// start
    for (int v : adj[node]) {
        if (v != par) {
            d = max(d , dfs(v , node)) ;
        }
    }
    return 1 + d ;
}
int main() {
	int n ;
	cin >> n ;// [1,n]
	adj.resize(n);
	
	for (int i = 0; i < n-1 ; i++) {
	    int a , b ;
	    cin >> a >> b ;
	    a-- ; b-- ;
	    adj[a].push_back(b); 
	    adj[b].push_back(a); 
	}
	// reach one farthest end and from
	vector<bool> vis(n , false) ;
    int farthest = -1 ;
    queue<int> q ;
    q.push(0) ;
    while (!q.empty()) {
            int u = q.front() ; q.pop();
            vis[u] = true ;
            farthest = u ;
            for (int v : adj[u]) {
                if (vis[v]) continue ;
                farthest = v ;
                q.push(v) ;
            }
    }
    // cout << "farthest Node :" << farthest << endl ; 
    int dia = dfs(farthest , -1  ) ;
    cout << dia-1 << endl ; // Edges = nodes - 1
	return 0 ;
}

```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N+N)    | worst case you may start looking from one farthest end to another end , then again visit all N nodes to reach to the this extreme where you actually started .         |
| 🧠 SPACE |   O(N)     |  Recursion Stack + Queue  {Specially for Skewed Tree}    |
