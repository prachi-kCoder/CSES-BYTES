# COURSE-SCHEDULE
- Here keep in mind don't forget to check cycle (because the nodes in cycle have `in_deg > 0` so they need to be handled !)
  
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


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(V+E)     | Each node is processed once, and each edge is considered once during the BFS traversal. This is standard for Kahn’s algorithm (topological sort).|
| 🧠 SPACE |   O(V+E)   |  You store: adjacency list (O(E)), in-degree array (O(V)), queue (O(V)), and result array (O(V)).         |
