```cpp
#include <bits/stdc++.h>
using namespace std;
 
int main() {
    int n , m , k ;
    cin >> n >> m >> k ;
    
    vector<int> a(n) ,b(m) ;
    for (int i = 0; i < n ; i++) {
        cin >> a[i] ; // desired
    }
    for (int i = 0; i < m ; i++) {
        cin >> b[i] ;
    }
    int cnt = 0;
    sort(a.begin() , a.end());
    sort(b.begin() , b.end());
    int j = 0;
    
    for (int i = 0 ; i < n ; i++) {
        while (j < m && a[i] > b[j] && a[i] - b[j] > k) j++ ;
        if (j >= m) break ;
        if (abs(a[i] - b[j]) <= k) {
            cnt++ ;
            j++ ;
        }
    }
    cout << cnt << endl ;
    
 }
```
## COMPLEXICITY ANALYSIS 
- Time Complexicity : Sorting : O(nlogn + mlogm) + O(n)  for traversal
- Space : O(n+m) for the linear arrays

### Or write it as :-
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n , m , k ;
    cin >> n >> m >> k ;
    
    vector<int> a(n) ,b(m) ;
    for (int &x : a) cin >> x ;
    for (int &x : b) cin >> x ;
    
    sort(a.begin() , a.end());
    sort(b.begin() , b.end());
    int cnt = 0 ,i = 0, j = 0;
    
    
    while (i < n && j < m) {
        if (abs(a[i] - b[j]) <= k) {
            i++ ; j++ ; cnt++ ;
        }else if (a[i] - k > b[j]) {
            j++ ;
        }else {
            i++ ;
        }
    }
    cout << cnt << '\n' ;
    return 0 ;

}

```
