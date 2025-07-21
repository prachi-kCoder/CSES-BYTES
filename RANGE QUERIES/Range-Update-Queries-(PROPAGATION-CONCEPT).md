# RANGE UPDATE QUERIES 
- Unlike the standard segment tree in which range queries are asked and point updates are made
- This topic includes Range Updates {ie the whole range is to be updated} & point queries are asked , ie any value after making the range updates before querying hence the point (position k ) has to be updated .

- Now for efficiently processing we use **LAZY PROPAGATION** this concept says make the updates only of asked , until just keep a mark down so that if the query is made on any idx {the updates can be made} & then only updated value is returned .
- Make 1 tree (normal segment tree) , no holding any range values (as it used to in the standard segTree) rather is is used to make the updates when the query is made on the idx , and keep the change that time .
- **LAZY tree** to keep a values to be updated over any idx .
  
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
class  SegTree{
public :
    vector<ll> tree, lazy ;
    SegTree(int n) {
        tree.resize(4*n , 0LL) ;
        lazy.resize(4*n , 0LL) ;
    }
    void build(int l , int r , int idx , vector<int>& a) {
        if (l == r) {
            tree[idx] = a[l] ;
            return  ;
        }
        int mid = l + (r - l)/2 ;
        build(l , mid , 2*idx + 1 , a) ;
        build(mid + 1 , r , 2*idx+ 2 , a) ;
        tree[idx] = 0 ; // lazy propagation
    }
    void push(int idx) {
        
        if (lazy[idx] != 0) {
            // Propagate to children
            lazy[2 * idx + 1] += lazy[idx];
            lazy[2 * idx + 2] += lazy[idx];
            lazy[idx] = 0LL; // Reset current node's lazy tag
        }
    }
    ll query(int l , int r , int pos , int idx ){
        if (l == r) {
            return tree[idx] + lazy[idx]; 
        } 
        // Propagate lazy value down before recursing
        push(idx);
        int mid = l + (r - l)/2 ;
        if (pos <= mid) return query( l, mid , pos , 2*idx + 1);
        else return query(mid +1 , r , pos , 2*idx + 2) ;
    }
    void update(int l , int r ,int val , int ql , int qr , int idx) {
        if (l > qr || r < ql ) return  ;
        if ( l >= ql && r <= qr ) {
            lazy[idx] += val ;
            return ;
        }
        // If partial overlap, push lazy down before recursing
        // This is crucial: ensure lazy values are pushed down before children are processed
        push(idx); // Propagate lazy value from current node to children
        int mid = l + (r - l) / 2;
        update(l, mid, val, ql, qr, 2 * idx + 1);
        update(mid + 1, r, val, ql, qr, 2 * idx + 2);
    }
};
int main() {
	ios_base::sync_with_stdio(0) ;
	cin.tie(0) ;
	int n , q ;
	cin >> n >> q ;
	vector<int> a(n) ;
	for (int& x : a) cin >> x ;
	
	SegTree t(n);
	t.build(0 , n-1, 0 , a);
	
	for (int j = 0 ; j < q ; j++) {
	    int type ;
	    cin >> type ;
	    if (type == 1) {
	        int a , b , x ;
	        cin >> a >> b >> x ;  a-- ; b-- ;
	        t.update( 0 , n-1 , x , a , b , 0 ) ;
	    }else {
	        int k ;
	        cin >> k ; k--;
	        cout << t.query(0 , n-1 , k , 0) << '\n' ;
	    }
	}

}

```

# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    WHY ? |
|-----------|-------------|------------|
| 🧭 TIME  | O(n + q*logn )     | Build for n values , and Quering take O(logn) as push are to be made , Updates take O(logn) marking  lazy for nodes |
| 🧠 SPACE |  O(4*n + 4*n) = O(n)   | Tree + Lazy  |

