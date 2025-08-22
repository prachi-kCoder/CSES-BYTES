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


# MORE OPTIMISED 
- Use multiset in place of PQ (as it does lazy deletion ) may be inefficient as we can't make the updates as soon as the left element is removed !
- BUT KEEP IN MIND :
	1)  Make update for the left value and their left_Value freq , and if after decrementing the left_val_freq -1 if > 0 then again insert in multiset (to keep the update freq of the left val)
    2)  Do update the new_val freq in multiset by replacement as new_value is newly inserted and if it is already present with an old_freq then do delete the old freq pair and insert the new_value with a new_freq . **removing the stale data is important here**


```cpp
#include <bits/stdc++.h>
using namespace std;

struct comp {
    bool operator()(const pair<int,int>& a , const pair<int,int>& b) const {
        if (a.first != b.first) {
            return a.first > b.first ;
        }
        return a.second < b.second ;
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
    multiset<pair<int,int>,comp> ms ;
    // freq based sort ->desc otherwise asc

	for (int i = 0; i < n ; i++) {
	    
	    
	    if (i - k >= 0) {
	       int old_val = a[i-k];
	       int old_f = mp[old_val];
           ms.erase(ms.find({old_f, old_val}));
	       
	       mp[old_val]-- ;
	       if (mp[old_val] > 0) {
	           ms.insert({mp[old_val] , old_val});
	       }else {
	           mp.erase(old_val);
	       }
	    }
	    int new_val = a[i] ;
	    if (mp.count(new_val)) {
	        int old_freq = mp[new_val] ;// oldfreq of new_val 
	        ms.erase(ms.find({old_freq,new_val}));
	    }
	    mp[new_val]++ ;
	    ms.insert({mp[new_val] , new_val});
	    
	    if (i < k-1) {
	        continue ;
	    }
	    auto it = ms.begin() ;
	    int e = it->second ;// element with mx freq 
	    cout << e << " ";
    }
	cout << endl ;
	return 0 ;
};

```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N*logN)   |  Multiset takes logN at every insertion and deletion, But efficiently updating of right freq, No lazy updates|
| 🧠 SPACE |    O(N)        | Map & Multiset maintained      |
