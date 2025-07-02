### SUBORDINATES COUNTING 

## Approach 1 : Simple DFS (+ memoization )
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0), cin.tie(0) , cout.tie(0) 
using namespace std;
int dfs(int node , unordered_map<int,vector<int>>& map , vector<int>& dp) {
    int cnt = 0 ;
    for (int subs : map[node] ) {
        if (dp[subs] == -1) {
            dp[subs] = dfs(subs , map, dp) ;
        }
        cnt += 1 + dp[subs] ;
    }
    return dp[node] = cnt ;
}
int main() {
    FASTIO ;
	int n ;
	cin >> n ;
	unordered_map<int,vector<int>> childMap ;
	for (int i = 2; i <=n ; i++) {
	    int p ;// parent of ith child 
	    cin >> p ;
	    childMap[p].push_back(i) ;
	}
	vector<int> dp(n+1 , -1) ;
	for (int i = 1 ; i <= n ; i++) {
	    if (dp[i] == -1) {
	        dp[i] = dfs(i , childMap , dp) ;
	    }
	   cout << dp[i] << " " ;
	}
	
	return  0 ;
}
```
### COMPLEXICITY ANALYSIS (Appraoch1 ): 
- TC o(N) // DFS {top - down}
- SC o(N) // map 

## Approach 2 : LEVELUp from Leaf to root node 1 (Director) 
## Keep in Mind : if (count[node] == 0 ) then push in the par as the a  
- COMPLEXICITY ANALYSIS :
- TC : O(n)
- SC : O(n)

```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0), cin.tie(0) , cout.tie(0) 
using namespace std;
int main() {
    FASTIO ;
	int n ;
	cin >> n ;
	int par[n+1] = {0};
	par[1] = 0 ;
	vector<int> count(n+1 , 0) ;
	for (int i = 2 ; i <= n ; i++ ) {
	    cin >> par[i] ;
	    count[par[i]]++ ;
	}
	// levelUp fron  leaves 
	queue<int> q ;
	for (int i = 1 ; i <= n ; i++ ) {
	    if (count[i] == 0) q.push(i) ;
	}

	vector<int> subs(n+1 ,0) ;
	while (!q.empty()) {
	    int node = q.front() ; q.pop();
	    
	    int p = par[node] ;
	    if (p == 0) continue ;
	    
	    subs[p] += subs[node] + 1 ;
	    count[p]-- ;
	    if (count[p] == 0) {
	        q.push(p) ;
	        // process only after getting all child Cnt completely
	    }
	}
	
	for (int i = 1 ; i <= n ; i++ ) {
	    cout << subs[i] << endl ;
	}
	
	return  0 ;
}
```
