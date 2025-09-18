# Planets-Kindoms

- This is a straight forward implementation of KOSARAJU'S ALGO {Get the cnt of SCC ie kingdoms }
- `Common pitfall : Don't forget the graph can be disconnected !!!`

```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> adj ;
vector<vector<int>> rev_adj ;

void dfs1(int node , stack<int>& stk , vector<bool>& vis) {
    vis[node] = true ;
    for (int nbr : adj[node]) {
        if (vis[nbr]) continue ;
        dfs1(nbr ,stk, vis) ;
    }
    stk.push(node) ;
}
void dfs2(int node , int k , vector<int>& kingdom) {
    kingdom[node] = k ;
    for (int nbr : rev_adj[node]) {
        if (kingdom[nbr] != -1) continue ;
        dfs2(nbr , k ,kingdom) ;
    }
}
int main() {
	int n ,  m;
	cin >> n >> m ;
	adj.resize(n) ;
	rev_adj.resize(n) ;
	
	for (int j = 1 ; j <= m  ; j++) {
	    int a , b ;
	    cin >> a >> b ;
	    a-- , b-- ;
	    adj[a].push_back(b) ;
	    rev_adj[b].push_back(a) ;
	}
	// scc 
	vector<bool> vis(n, false) ;
	stack<int> stk ;

	for (int i = 0; i < n ; i++) {
	    if (!vis[i]) {
	
	        dfs1(i , stk , vis) ;
	    }
	}

	int cnt = 0 ;
	vector<int> kingdom(n , -1) ;
	while (!stk.empty()) {
	    int curr = stk.top() ; stk.pop();
	    if (kingdom[curr] == -1) {
	        cnt++ ;
	        dfs2(curr, cnt , kingdom) ;
	    }
	}
	cout << cnt << endl ;
	for (int i = 0; i < n ; i++) {
	    cout << kingdom[i] << " " ;
	}
	cout << endl ;
	
	return  0 ;
}

```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(V + E)    | 2 Dfs and  Over the adj & rev_adjacency to get their kingdoms |
| 🧠 SPACE |    O(V + E)        | Adj , rev_adj O(V+E) ; vis , kingdom arrays O(V)   & stack, rec_stack        |
