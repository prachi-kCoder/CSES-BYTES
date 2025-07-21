# Range - XOR Queries 
```cpp
#include <bits/stdc++.h>
#define ll long long
using namespace std;
class SegTree {
public :
    vector<ll> tree ;
    SegTree(int n) {
        tree.resize(4*n);
    }
    void build(int l, int r , int idx , vector<int>& arr) {
        if (l == r) {
            tree[idx] = arr[l] ;
        }else {
            int mid = l + (r - l)/2 ;
            build(l , mid , 2*idx + 1 , arr) ;
            build(mid+1 , r , 2*idx + 2 , arr) ;
            tree[idx] = (tree[2*idx+1]^tree[2*idx+2]) ;
        }
    }
    ll query(int l , int r , int ql , int qr , int idx ) {
        if (l > qr || r < ql) return 0LL ;
        if ( l >= ql && r <= qr) return tree[idx] ;
        int mid  = l + (r - l)/2 ;
        ll lXor = query(l , mid , ql , qr, 2*idx + 1) ;
        ll rXor = query(mid+1 , r , ql , qr, 2*idx + 2) ;
        
        return (lXor^rXor) ;
    }
};
int main() {
    ios_base::sync_with_stdio(0) ; cin.tie(0) ;
    int n , q ;
    cin >> n >> q ;
    vector<int> a(n) ;
    for (int& x : a) cin >> x ;
    SegTree t(n) ;
    t.build( 0 , n-1 , 0 , a ) ;
    
    for (int j = 0; j < q ; j++) {
        int a , b ;
        cin >> a >> b ;
        cout << t.query(0 , n-1 , a-1 , b-1 , 0 ) << endl ;
    }
    return 0;
}
```
## POINT OF CONFUSION  :
- People gets confused at where to do **tree[idx] = tree[2*idx+1]^tree[2*idx+2]**  , or take the values from the left , right and return **left^right** , on any operation (not necessarily be xor only )
- Keep in mind the difference :
  
 |     tree[idx] = tree[2*idx+1]^tree[2*idx+2]   |     left^right |
 |------------------|-----------------------------|
 |  build() – Bottom-Up Construction  , update() – Modify a Value and Fix the Path {Because when a leaf changes, all affected parents must recompute their merged result.}   |   query partial ranges ans are computed and returned  |



|Operation	   | Use tree[idx] = left ^ right?  | 	Purpose | 
|----------------|------------------------------|------------|
|build()	|✅ Yes	|Construct tree bottom-up |
|update()	|✅ Yes	|Recompute parents after modification |
|query()	|⚠️ No direct assignment	| Return XOR of valid subranges (not raw children) {leftXor^rightXor} |


# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n + q*logn )    | TreeBuilding (Insertion of n values) : O(logn)) , Querying in SegTree : O(logn) for each q query |
| 🧠 SPACE |  O(4*n)   |   Seg Tree take 4*n space     |

