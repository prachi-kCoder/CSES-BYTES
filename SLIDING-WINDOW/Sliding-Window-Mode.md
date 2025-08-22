## Sliding-Window-Mode

```cpp
#include <bits/stdc++.h>
using namespace std;
// to get pq->mx heap and for same freq the smaller is given more priority 
struct comp {
    bool operator()(const pair<int,int>& a , const pair<int,int>& b) {
        return a.first == b.first ? a.second > b.second : a.first < b.first ;
    }  
};
int main() {
	int n , k ;
	cin >> n >> k;
	vector<int> a(n) ;
	for (int i = 0 ; i < n ; i++) {
	    cin >> a[i] ;
	}
	map<int,int> mp ;
	priority_queue<pair<int,int>,vector<pair<int,int>>,comp> pq ;
	
	for (int i = 0; i < n ; i++) {
	    mp[a[i]]++ ;
	    pq.push({mp[a[i]] , a[i]}) ;
	    
	    if (i >= k-1) {
	        if (i - k >= 0) {
	            mp[a[i-k]]-- ;
	            if (mp[a[i-k]] == 0) mp.erase(a[i-k]);
	            while (!pq.empty()) {
	                int f = pq.top().first ;
	                int ele = pq.top().second ;
	                if (mp.find(ele) == mp.end() || f > mp[ele]) {
	                    pq.pop();
	                }else {
	                    break ;
	                }
	            }
	        }
	        cout << pq.top().second << " ";
	    }
    }
	cout << endl ;
	return 0 ;
};
```


# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*logN)   |  PQ takes logN at every insertion and deletion       |
| 🧠 SPACE |    O(N)        | Map & PQ maintained      |
