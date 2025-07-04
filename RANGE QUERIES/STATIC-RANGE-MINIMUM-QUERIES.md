## STATIC-RANGE-MINIMUM-QUERIES 

```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
const int MAX = 1e9 + 5 ;
const int N = 2e5 + 5 ;
int tree[4*N] , arr[N] ; 
int sz ;

void build(int l = 0 , int r = sz-1 , int node = 0) {
        if (l > r) return ;
        if (l == r) {
            tree[node] = arr[l] ;
        }else {
            int mid = l + (r-l)/2 ;
            build( l , mid , 2*node + 1) ;
            build( mid+1 , r , 2*node + 2 ) ;
            tree[node] = min(tree[2*node+1] , tree[2*node + 2]) ;
        }
}
int query( int ql , int qr ,int l = 0 , int r = sz-1 ,int node = 0 ) {
        if ( l > qr || r < ql ) return MAX ;// noOverlap
        if ( l >= ql &&  r <= qr) return tree[node]; // complete overlap
        int mid = l + (r-l)/2 ;
        
        int lMin = query( ql , qr ,l , mid ,2*node + 1 );
        int rMin = query( ql , qr ,mid+1 , r ,2*node + 2 );
        return min(lMin , rMin) ;
    }
 
int main() {
    FASTIO ;
    int n , q ;
    cin >> n >> q ;
    sz = n ;
    
    for (int i = 0 ; i < n ; i++) {
        cin >> arr[i] ;
    }
    build();
    
    for (int j = 0; j < q ; j++) {
        int a, b ;
        cin >> a >> b ;
        a-- , b-- ;
        cout << query(a,b) << endl ;
    }
    
	return 0 ;
}
```
### COMPLEXICITY ANALYSIS AND PROTIPS :-
- If you started with **vector<int>**  , look why array are more efficient than making vector<int> for segment tree
- ![image](https://github.com/user-attachments/assets/31adf665-d59c-4c7e-8524-fb1bffc6659b)

📊 Constraint Pro Tips to Keep IN Mind

|When constraints say| WHAT TO DO ? |
|-------------------|---------------| 
| Up to 1e5  	    | STL (vector, map) is OK |
| Up to 2e5–5e5     | optimize loops and segment tree carefully, prefer arr[] |
| Up to 1e6 or more | use fast I/O, preallocated arrays, and avoid STL containers in inner loops |
| Use FASTIO        | ios_base::sync_with_stdio(0) , cin.tie(0)  for fast I/P & O/P |
