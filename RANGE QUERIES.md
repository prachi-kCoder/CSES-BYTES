
## APPROACH 1 
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
#define ll long long 
#define M 1000000009
using namespace std;

int main() {
    FASTIO ;
    int n , m ;
    cin >> n >> m ;
    vector<ll> pre(n) ;
    for (int i = 0; i < n ; i++) {
        ll e ;
        cin >> e ;
        pre[i] = ( i==0 ) ? e : pre[i-1] + e ;
    }
    
    for (int j = 0; j < m ; j++) {
        int a , b ;
        cin >> a >> b ;
        a-- , b-- ;
        cout << (pre[b] - (a > 0 ? pre[a-1] : 0 )) << endl ;
    }
    
    return 0 ;
}
```
## APPROACH 2 

### USE SEGMENT TREE : It may seem a bit overwhelming in the first go , but it over efficient specifically in those cases when updation are also made 
```cpp
#include <bits/stdc++.h>
using namespace std;
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
#define ll long long 
class SegTree {
    int n ; vector<ll> tree ;
public :
    SegTree(int n) {
        this->n = n ;
        tree.resize( 4*n , 0LL) ;
    }
    void build(vector<ll>& a, int node , int l , int r) {
        if(l == r) {
            tree[node] = a[l] ;
        }else {
            int mid = l + (r-l)/2 ;
            build(a , 2*node + 1 , l, mid) ;
            build(a , 2*node + 2 , mid + 1 , r) ;
            tree[node] = tree[2*node+1] + tree[2*node + 2] ;
        }
    }
    ll query(int node , int l , int r , int ql , int qr) {
        if ( qr < l || ql > r ) return 0LL ;
        if ( l >= ql && r <= qr ) return tree[node] ;
        int mid = l + (r - l)/2 ;
        return query(2*node + 1 , l , mid , ql , qr) + query(2*node + 2 , mid + 1 , r , ql, qr) ;
    }
    void update(int l , int r , int node , int idx , int val) {
        if (l == r) {
            tree[node] = val ;
        }else {
            int mid = l + (r-l)/2 ;
            if (idx <= mid) {
                update(l , mid , 2*node + 1 , idx , val);
                update(mid , r , 2*node + 2 , idx , val);
            }
        }
    }
    void build(vector<ll>& a) {
        build(a , 0, 0, n-1 );
    }
    ll query(int l , int r) {
        return query(0 , 0 , n-1 , l , r) ;
    }
    void update(int idx , ll val) {
        update(0 , 0 , n-1 , idx , val) ;
    }
};
int main() {
    FASTIO ;
    int n , m ;
    cin >> n >> m ;
    SegTree st(n);
    
    vector<ll> a(n) ;
    for (int i = 0; i < n ; i++) cin >> a[i] ;
    
    st.build(a) ;
    
    for (int j = 0; j < m ; j++) {
        int l , r ;
        cin >> l >> r ;
        cout << st.query(l-1 , r-1) << endl ;
    }
    return 0 ;
}
```

### COMPLEXICITY ANALYSIS : (ONLY FOR QUERING IN ARRAY) 
![image](https://github.com/user-attachments/assets/bab825bb-b93a-4314-889e-e015518fbf47)


##
