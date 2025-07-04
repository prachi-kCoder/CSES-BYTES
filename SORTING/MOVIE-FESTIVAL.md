## MOVIE-FESTIVAL 
### Apply Greedy  : Watch those movied which ends soon !

```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
#define pb push_back
#define S second
#define F first
using namespace std;

int main() {
	FASTIO ;
	int n ;
	cin >> n ;
	vector<pair<int,int>> v ;
	for (int i = 0 ; i< n ; i++) {
	    int s , e ;
	    cin >> s >> e ;
	    v.pb({s,e});
	}
	sort(v.begin() , v.end() ,[](const pair<int,int>& a , const pair<int,int>& b) {
	    return a.S < b.S ;
	});
	
	int ans = 0 ;
	int t = 0 ;
	for (int i = 0 ; i < n ; i++) {
	    if (v[i].F >= t ) {
	        t = v[i].S ;
	        ans++ ;
	    }
	}
	cout << ans << endl ;

};
```

## 🚀 Complexity Analysis

### ⏱ Time Complexity

| Approach     | Time Complexity  |
|--------------|------------------|
| **SORTING**  | O(n + n + nlogn) = O(nlogn), since insertion + iteration + sorting |

### 📦 Space Complexity

| Approach     | Space Breakdown |
|--------------|-----------------|
| **SORTING**  | O(n)            |

