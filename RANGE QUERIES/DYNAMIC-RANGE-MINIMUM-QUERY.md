# Dynamic Range Minimum Queries

```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
#define ll long long
const int N = 2e5 + 1 ;
int arr[N] ;
class SegTree{
    vector<ll> tree ; int n ;
public :
    SegTree(int n) {
        this-> n = n ;
        tree.resize(4LL*n+1) ;
    }
    void build(int l , int r , int node ){
        if(l == r) {
            tree[node] = arr[l] ;
            return ;
        }
        int  mid =  l + (r-l)/2 ;
        build(l , mid , 2*node+1 ) ;
        build(mid + 1 , r , 2*node+2 ) ;
        tree[node] = min(tree[2*node+1] , tree[2*node + 2]) ;
    }
    ll query(int l , int r , int ql , int qr , int node) {
        if (l > qr || r < ql ) return  LLONG_MAX ;
        if (l >= ql && r <= qr ) return tree[node] ;
        int mid = l + (r - l)/2 ;
        ll left = query(l , mid, ql , qr , 2*node + 1);
        ll right = query(mid + 1, r, ql , qr , 2*node + 2);
        return min(left , right);
    }
    void update(int l ,int r ,  int node, int pos , int val) {
        if (l == r) {
            tree[node] = val ;
            return ;
        }
        int mid = l + (r-l)/2 ;
        if (pos <= mid) {
            update( l , mid,  2*node + 1 , pos, val) ;
        }else {
            update( mid+1 , r , 2*node + 2 , pos, val) ;
        }
        tree[node] = min(tree[2*node + 1] , tree[2*node + 2]) ;
    }
};
int main() {
    FASTIO ;
    int n , q ;
    cin >> n >> q ;
    for(int i = 0; i < n ; i++) {
        cin >> arr[i];
    }
    SegTree segtree(n) ;
    segtree.build(0 , n-1 , 0);
    
    for (int j = 0 ; j < q ; j++) {
        int t , x ,y ;
        cin >> t >> x >> y ;
        
        if (t == 1) {
            segtree.update( 0, n-1 ,0, x-1 , y );// pos = x-1 
        }else {
            cout << segtree.query(0 , n-1 , x-1 ,y-1 , 0) << endl ;
        }
    }   
}
```
## COMPLEXICITY ANALYSIS 

| METRIC    |  COMPLEXICITY |  HOW ?  |
|------------|----------------|--------|
|  🧮 TIME   |  O(N + Q logN )| Tree formation + Q*{update / query time of O(logN)} |
| 🧠 SPACE   |  O(4*N + N)     | Array + segTree |
