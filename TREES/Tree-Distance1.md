# Tree-Distance1

```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> adj ;
void dfs1(int curr , int d , int& farthest, int& mx_dist1, vector<bool>& vis) {
    if (d > mx_dist1) {
        mx_dist1 = d ;
        farthest = curr ;
    }
    vis[curr] = true ;
    for (int nbr : adj[curr]) {
        if (!vis[nbr]) {
            dfs1(nbr , d+1 , farthest , mx_dist1 , vis) ;
        }
    }
    
}
void dfs2(int curr , int d , int& right_end, int& mx_dist2, vector<int>& left, vector<bool>& vis) {
    if (d > mx_dist2) {
        mx_dist2 = d ;
        right_end = curr ;
    }
    vis[curr] = true ;
    left[curr] = max(left[curr] , d) ;
    
    for (int nbr : adj[curr]) {
        if (!vis[nbr]) {
            dfs2(nbr , d+1 , right_end , mx_dist2 , left , vis) ;
        }
    }
    
}
void dfs3(int curr , int d ,  vector<int>& right, vector<bool>& vis) {
    
    vis[curr] = true ;
    right[curr] = max( right[curr] , d ) ;
    for (int nbr : adj[curr]) {
        if (!vis[nbr]) {
            dfs3(nbr , d+1 , right , vis) ;
        }
    }
    
}
int main() {
	int n ;
	cin >> n ;

	adj.resize(n); 
	
	for (int i = 1 ; i < n ; i++) { // n-1 edges
	    int a , b ;
	    cin >> a >> b ;
	    a-- , b-- ;
	    adj[a].push_back(b);
	    adj[b].push_back(a);
	}
	int farthest = 0 , mx_dist1 = 0 ;
	vector<bool> vis(n , false);
	
	dfs1(0 , 0 , farthest, mx_dist1 , vis) ;
	vis.assign(n , false) ;
	vector<int> left(n, 0) ; // mx left dist from left End 
	
	int right_end = 0 , mx_dist2 = 0 ;
	
	dfs2(farthest , 0 , right_end , mx_dist2 , left , vis ) ;
	
	vis.assign(n , false) ;
	vector<int> right(n, 0) ; // mx left dist from left End 
	dfs3(right_end , 0 , right , vis) ;
	
	for (int i = 0; i < n ; i++) {
	    cout << max(left[i] , right[i]) << " " ;
	}
	cout << endl ;
	
	return  0 ;
}
```


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(N)         | 3 DFS passes - Diameter bases approach , to get the max_dist from each node from 2 ends fo the longest diameter|
| 🧠 SPACE | O(N + E) → O(N) for trees | `adj` stores both directions of each edge; `left`, `right`, and `vis` are all O(N) |
