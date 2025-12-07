# Re-Root-DP

- TREED-DISTANCE1 CSES EXAMPLE QUES :
### 1. Downwards Pass (Initial DP: dfs1)
- Goal: Calculate DP_sub[u] , the maximum distance from node $u$ to any node within the subtree rooted at u .
- Simply `Dp_sub[u] = among all child nodes v : max(dp_sub[v]) + 1`
  
- Upwards Pass (Rerooting: dfs2) :
- This pass calculates the maximum path length from a node upwards to any node in the rest of the tree (the "outside" component).
- Transition (from parent `p` to child `u`):
- Dp_up[v] =  1 + max(dp_up[p] , L_other[p])
- where `L_other[p]` is the maximum path starting at `p` and going down to any child other than `u`.
```
- In rerooting we have 2 paths
- Path 1: Dp_up[p]+1  ie One option for u is to go to p (distance 1) and then take the maximum path from p upwards
- Path2 from Siblings (Downward): The other option for `u` is to go to `p` (distance 1)
 and then go down into any of u's sibling branches. The maximum length of these sibling paths is equivalent to L_other[p]

```

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

// Store the max distance from a node to any node in its subtree
vector<ll> dp_sub; 
// Store the max distance from a node to any node outside its subtree
vector<ll> dp_up; 
vector<vector<int>> adj;

// Helper struct to store the top two longest paths from children
struct PathInfo {
    ll max1_dist = 0;
    ll max2_dist = 0;
    int max1_child = -1; // To identify which child gave the longest path
};
vector<PathInfo> path_info;

void dfs1(int u, int par) {
    ll current_max1 = 0;
    ll current_max2 = 0;
    int max1_child = -1;

    for (int v : adj[u]) {
        if (v == par) continue;
        dfs1(v, u);
        
        ll child_dist = dp_sub[v] + 1;

        if (child_dist > current_max1) {
            current_max2 = current_max1;
            current_max1 = child_dist;
            max1_child = v;
        } else if (child_dist > current_max2) {
            current_max2 = child_dist;
        }
    }
    
    dp_sub[u] = current_max1;
    path_info[u] = {current_max1, current_max2, max1_child};
}

void dfs2(int u, int par) {
    for (int v : adj[u]) {
        if (v == par) continue;
        
        // 1. Get the max distance from u that DOES NOT go through v
        ll path_from_u_not_v;
        
        // If v was on the longest path from u (path_info[u].max1_child == v)
        if (path_info[u].max1_child == v) {
            // Use the second longest path from u (max2_dist)
            path_from_u_not_v = path_info[u].max2_dist;
        } else {
            // Otherwise, use the longest path from u (max1_dist)
            path_from_u_not_v = path_info[u].max1_dist;
        }

        // 2. The new 'up' path for v is the max of:
        //    a) The path from u that came from the outside (dp_up[u])
        //    b) The max path from any of u's siblings of v (captured in path_from_u_not_v)
        // Add +1 for the edge (u, v)
        dp_up[v] = max(dp_up[u] + 1, path_from_u_not_v + 1);

        dfs2(v, u);
    }
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    int n;
    if (!(cin >> n)) return 0;
    
    adj.resize(n);
    dp_sub.assign(n, 0);
    dp_up.assign(n, 0);
    path_info.resize(n);

    for (int i = 0; i < n - 1; i++) {
        int u, v;
        cin >> u >> v;
        u--, v--;
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    if (n == 0) return 0;

    // Root at 0 for initial pass
    dfs1(0, -1);
    
    // Rerooting pass
    // dp_up[0] is initialized to 0 because the root has no "outside" component.
    dfs2(0, -1);
    
    for (int i = 0; i < n; i++) {
        cout << max(dp_sub[i], dp_up[i]) << (i == n - 1 ? "" : " ");
    }
    cout << "\n";
    
    return 0;
}
```
