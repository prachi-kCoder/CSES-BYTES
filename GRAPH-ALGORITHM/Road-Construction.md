# ROAD CONSTRUCTION
```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> par ;
vector<int> cmp_size ;
int max_size ;
int component_cnt ;
void init(int n) {
    par.resize(n) ;
    cmp_size.assign(n,1) ;
    max_size = 1 ;
    component_cnt = n ;
    for (int i = 0; i < n ; i++) par[i] = i ;
}
int find(int x) {
    if (par[x] == x) return x ;
    return par[x] = find(par[x]) ;
}
void unite(int a , int b) {
    int pa = find(a) ;
    int pb = find(b) ;
    if (pa == pb) return ;
    if (cmp_size[a] < cmp_size[b]) swap(pa, pb) ;
    
    component_cnt--;
    par[pb] = pa ;
    
    cmp_size[pa] += cmp_size[pb] ;
    max_size = max(max_size , cmp_size[pa]) ;
}
int main() {
	int n, m;
    cin >> n >> m;
    init(n);
    
    for (int j = 1  ; j <= m ; j++) {
        int a,  b ;
        cin >> a >> b ;
        a-- , b-- ;
        unite(a ,b) ;
        cout << component_cnt << " " << max_size << endl ;
    }
    return  0 ;
}
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N × α(N))   |  init: O(N), find: amortized O(α(N)) per call due to path compression, unite: constant time with union by size     |
| 🧠 SPACE |    O(N)       |    Par, Componenct size array {unite is size based}       |

- α(N) is the inverse Ackermann function, which grows extremely slowly—effectively constant for all practical input sizes.
- It’s used in DSU analysis because it bounds the number of times a node’s parent pointer needs to be updated during find() operations with path compression.
- When you use path compression in find() and union by size/rank in unite(), the amortized time per operation becomes:

       O(N × α(N))  per operation
So for 𝑁 operations, the total time is: `O(N × α(N))`
This is nearly linear — and practically constant.
 
