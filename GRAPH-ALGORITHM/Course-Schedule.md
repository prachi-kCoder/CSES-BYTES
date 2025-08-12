# COURSE-SCHEDULE
- Here keep in mind don't forget to check cycle (because the nodes in cycle have `in_deg > 0` so they need to be handled !)

## KAHN'S ALGO (BFS)

```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> adj ;
int main() {
    int n , m ;
    cin >> n >> m ;
    adj.resize(n) ;
    
    vector<int> deg(n , 0) ;
    for (int j = 1 ; j <= m ; j++) {
        int a , b ; 
        cin >> a >> b ;
        a-- , b-- ;
        adj[a].push_back(b) ;
        deg[b]++ ;
    }
    
    queue<int> q ;
    for (int i = 0; i < n ; i++){
        if (deg[i] == 0) {
            q.push(i);
        }
    }
    vector<int> order ;
    while (!q.empty()) {
        int c = q.front() ;  q.pop();
        order.push_back(c+1) ;
        
        for (int nbr : adj[c]) {
            deg[nbr]-- ;
            if (deg[nbr] == 0) {
                q.push(nbr) ;
            }
        }
    }
    if (order.size() < n) { 
        cout << "IMPOSSIBLE" << endl ;
    }else {
        
        for(int i = 0; i < n ; i++){
            cout << order[i] << " " ;
        }
    }
    
    return  0 ;
}
```
## DFS TOPO-ORDER APPROACH 
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> adj ;
bool dfs(int curr , vector<bool>& vis , vector<bool>& rec_stk, vector<int>& order) {
    vis[curr] = true ;
    rec_stk[curr] = true ;
    
    
    for (int nbr : adj[curr]) {
        if (!vis[nbr]) {
            if (dfs(nbr , vis , rec_stk , order)){ // cycle from nbr
                return true ;
            }
        } else if (rec_stk[nbr]) {
            return true ;// cycle!
        }
    }
    // first visit nbr and then get the currNode ;
    order.push_back(curr);
    rec_stk[curr] = false ;
    
    return false ; // no cycle
}
int main() {
    int n , m ;
    cin >> n >> m ;
    adj.resize(n) ;
    
    for (int j = 1 ; j <= m ; j++) {
        int a , b ; 
        cin >> a >> b ;
        a-- , b-- ;
        // adj[a].push_back(b) ;
         adj[b].push_back(a) ; // do a before b 
    }
    vector<bool> vis(n , false) ;
    vector<bool> rec_stk(n , false) ;
    vector<int> order ; 
    bool cycle = false ;
    
    for (int i = 0 ; i < n ; i++ ) {
        if (!vis[i]) {
            if (dfs(i , vis , rec_stk , order)) {
                cycle = true ;
                break ;
            }
        }
    }
    if (cycle) {
        cout << "IMPOSSIBLE" << endl ;
    }else {
        for(int i = 0; i < n ; i++){
            cout << (order[i] + 1) << " " ;
        }
    } 
    
    return  0 ;
}
```

# 🔄 Edge Direction Clarification
- Also correctly adjusted the edge direction:
- In `Kahn’s BFS`, we use `a → b` to mean “do a before b”.
- In `DFS`, to ensure a is visited before b, we need `b → a` in the adjacency list. & after doing dfs for all nbr nodes, then add the curr node in order !

# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(V+E)     | Each node is processed once, and each edge is considered once during the BFS traversal. This is standard for Kahn’s algorithm (topological sort).|
| 🧠 SPACE |   O(V+E)   |  You store: adjacency list (O(E)), in-degree array (O(V)), queue (O(V)), and result array (O(V)).         |
