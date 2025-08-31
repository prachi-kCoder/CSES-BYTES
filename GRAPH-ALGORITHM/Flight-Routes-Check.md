# FLIGHT-ROUTES-CHECK
- Apply kosaraju algorithm

```cpp
#include <bits/stdc++.h>
using namespace std;
vector<vector<int>> adj ;
vector<vector<int>> rev_adj ;
void dfs1(int node , int n , stack<int>& stk ,  vector<bool>& vis) {
    vis[node] = true ;
    for (int nbr : adj[node]) {
        if (!vis[nbr]) {
            dfs1(nbr , n , stk , vis) ;
        }
    }
    stk.push(node) ;
}
void dfs2(int node , int n , vector<bool>& vis) {
    vis[node] = true ;
    for (int nbr : rev_adj[node]) {
        if (!vis[nbr]) {
            dfs2(nbr , n  , vis) ;
        }
    }
}
int main() {
    int n , m ;
    cin >> n >> m ;
    adj.resize(n) ;
    rev_adj.resize(n) ;
    
    for (int j = 1 ; j <= m ; j++) {
        int a , b ;
        cin >> a >> b ;
        a-- , b-- ;
        adj[a].push_back(b) ;
        rev_adj[b].push_back(a) ;
    }
    
    vector<bool> vis(n , false) ;
    int c = 0 ; // to check if the graph is disconnected or not 
    stack<int> stk ;
    int prev = -1 , sec = -1 ;
    for ( int i = 0 ; i < n ; i++) {
        if (!vis[i]) {
            if (c >= 1) {
                sec = i ;// disconnection
                break ;
            }else {
                c++ ;
                prev = i ;
                dfs1(i , n ,stk , vis);
            }
        }
    }
    if (sec != -1) {
        cout << "NO" << endl ;
        cout << prev+1 <<" " << sec+1 << endl ;
    }else {
        vis.assign(n , false) ;
        int start = stk.top() ; stk.pop(); 
        
        dfs2(start , n , vis) ;
        int unreachable = -1 ;
        
        
        while (!stk.empty()) {
            int c = stk.top() ; stk.pop();
            if (!vis[c]) {
                unreachable = c ;
                break ;
            } 
        }
        if (unreachable != -1) {
            cout << "NO" << endl ;
            cout << unreachable+1 <<" "<<start+1 << endl ;
        }else {
            cout << "YES" << endl ;
        }
    }
    
    return 0 ;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(V+E)      |   2 pass -dfs {for all n nodes} |
| 🧠 SPACE |    O(V+E)       |  Stack, Recursion-stack ,Vis :`O(V)` &  Adj , RevAdj : `O(V+E)`    |
