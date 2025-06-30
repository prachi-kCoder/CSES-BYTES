
## Complexicity :
- Time Complexicty : O(n)
- Space Complexicty : O(1) , no extra space

  ```cpp
  #include <bits/stdc++.h>
  #define FASTIO() ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
  using namespace std;
 
  int main() {
    FASTIO();
    
    int n , x ;
    cin >> n >> x ;
    vector<int> w(n) ;
    for (int &x : w) cin >> x ;
    
    sort(w.begin() , w.end()) ;
    int l = 0 , r = n-1 ;
    int cnt = 0 ;
    while (l <= r) {
        if (w[l] + w[r] <= x) l++ ;
        r-- ;
        cnt++ ;
    }
    
    cout << cnt << endl ;
    return 0 ;

  ```
