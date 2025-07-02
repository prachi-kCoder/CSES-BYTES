# LABYRIYNTH : (A  to B) reach with min Steps while display the moves takes to reach B from  A

### Here we will form B to A rather that A to B :- 
```cpp
#include <bits/stdc++.h>
#define ll long long 
#define F first 
#define S second 
#define pb push_back 
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) ,cout.tie(0)
#define pii pair<ll,ll>
using namespace std;

string s[1005] ;
pii par[1005][1005] ;// par coordinate pairs 
bool vis[1005][1005];
int dir[1005][1005] ;

int dx[] = {-1,1,0,0};
int dy[] = {0,0,-1,1};

char dd[] = {'D','U','R','L'};

int main() {
    FASTIO ;
    int n , m ;
    cin >> n >> m ;
    for (int i = 0; i< n ; i++) {
        cin >> s[i] ;
    }
    
    pii st , en ;
    for (int i = 0 ; i < n ; i++) {
        for (int j = 0; j < m ; j++) {
            if (s[i][j] == 'B') st = {i , j};
            else if (s[i][j] == 'A') en = {i , j};
        }
    }
    
    // From B to A 
    queue<pii> q ;
    q.push(st) ;
    vis[st.F][st.S] = true ;
    
    while (!q.empty()) {
        auto u = q.front();
        q.pop();
        
        for (int k = 0 ; k < 4 ; k++) {
            int vx = u.F + dx[k] , vy = u.S + dy[k] ;
            if (vx >= 0 && vx < n && vy >= 0 && vy < m && s[vx][vy] !='#' && !vis[vx][vy]) {
                
                vis[vx][vy] = true ;
                par[vx][vy] = u ;
                dir[vx][vy] = k ;
                
                q.push({vx , vy});
            }
        }
        
    }
    
    if (!vis[en.F][en.S]) {
        cout << "NO" << endl ;
        return 0 ;
    }
    
    cout << "YES" << endl ;
    
    int steps = 0 ;
    string path = "" ;
    int x = en.F , y = en.S ;// 'A' to 'B'
    
    while (x != st.F or y != st.S) {
        steps++ ;
        auto p = par[x][y] ;
        path += dd[dir[x][y]] ;
        x = p.F , y = p.S  ;
    }
    cout << steps << endl ;
    // From A tp B 
    cout << path << endl; 
    
    return 0 ;
}

```
## COMPLEXICITY ANALYSIS :- 
💡 Time Complexiicty  = O(n × m × 4) = O(n × m)
📦 Space Complexity : Space = O(n × m)  {At max with }
