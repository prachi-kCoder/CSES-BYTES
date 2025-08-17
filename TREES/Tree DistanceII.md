# TREE-DISTANCE II 

- RE-ROOT TREE DP
- `dfs1 : POST-ORDER` :-
-  To compute the distance with the nodes within the subtree , so it depends in the sum of dist from children nodes , hence first go deep and them compute the distance using them  just by adding cnt
- `subtree-size` : Gives the cnt of nodes including itself to compute for the +1 distance for each node within subtree of v to u (par)
- `dfs1 POST-ORDER` : dp[v] = dp[v] + subtree_size[v]  , ie adding +1 for all the nodes {v (itself), its subtree node cnt }

- Observe if we started with 0th node so it par = -1 , so it computed the distance sum with all other nodes rightly but its child nodes have distances computed with the nodes only within their subtree not with other nodes outside
- To compute distance whose connection with any u node is via the par node  {which was skipped in dfs1}

- `DFS2 :PRE ORDER` :
- To compute the distance with the nodes outside the subtree
- as the 0th node {that we started our dfs1 with !} the same node : has the correct sum of distance with all ohter nodes so using it we compute for the other nodes
- `dp[v] = dp[u] - subtree_size[v] + (n- subtree_size[v])`
- dp[v] : Right sum of dist value for child node v
- dp[u] : Right sum of dist values for par u
- From u -> v the dist with the nodes within  subtree of v and v itself be decreased by (+1) {with all individual nodes v, and subnodes of v} hence  `dp[u] - (subtree_size[v])`
- And the dist with all other nodes be increased by +1  , outside nodes cnt :  `{n - subtree_size[v]}`
- hence u can adjust for distance changes -1 (v , and its subnodes) &  +1 (other than the v & its subnodes) & we get the sum of dist for any v (child node of u) ;
- 
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
vector<ll> dp , subtree_size ;
vector<vector<int>> adj ;
int n ;
// post_order
void dfs1(int u , int par) {
    subtree_size[u] = 1 ;
    
    for (int v :adj[u]){
        if (v == par) continue ;
        dfs1(v ,u) ;
        subtree_size[u] += subtree_size[v] ;
        dp[u] += dp[v] + subtree_size[v] ;
    }
}
void dfs2(int  u, int par) {
    for (int v : adj[u]) {
        if (v == par) continue ;
        
        dp[v] = dp[u] - subtree_size[v] + (n - subtree_size[v]) ;
        dfs2(v , u);
    }
}
int main() {
    cin >> n ;
    adj.resize(n) ;
    dp.resize(n) ;
    subtree_size.resize(n) ;
    
    for (int i = 0 ; i<n-1 ; i++) {
        int a , b ;
        cin >> a >> b ;
        a-- ,b--;
        adj[a].push_back(b) ;
        adj[b].push_back(a) ;
    }
    dfs1(0 , -1) ;
    dfs2(0 , -1) ;
    
    for (int i = 0; i < n;i++) {
        cout << dp[i] << " " ;
    }
    cout << endl ;
    return 0 ;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(V+E)      |  Two DFS traversals: one post-order to compute subtree sizes and initial distances, and one pre-order to reroot and propagate distances.    |
| 🧠 SPACE |  O(V+E) |    ADJ list , dp[]  , subtree_size[]  , recursion stack  |

