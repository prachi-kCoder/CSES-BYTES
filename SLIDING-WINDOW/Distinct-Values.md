# Distinct-Values

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n , k ;
	cin >> n >> k ;
	vector<int> v(n) ;
	for (int i = 0; i < n ; i++) {
	    cin >> v[i] ;
	}
	map<int,int> map;

	for (int i = 0 ; i < n ; i++) {
	    map[v[i]]++ ;
	    
	    if ( i >= k-1 ) {
	        int l = i - k  ;
	        if (l >= 0) {
	            map[v[l]]-- ;
	            if (map[v[l]] == 0) {
	                map.erase(v[l]);
	            }
	        }
	        cout << map.size() << " " ;
	    }
	}
	cout << endl ;
	return 0 ;
}
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(1)       |    unordered_map is more optimised here |
| 🧠 SPACE |     O(K)    |   Map holds freq of k values       |
