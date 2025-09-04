# LIS OF AN ARRAY :

- This gives `TLE` :Although intuition is right but O(N*N) complexicity is not optmal way

```cpp
#include <bits/stdc++.h>
using namespace std;
 
int main() {
	int n ;
	cin >> n ;
	vector<int> a(n) ;
	for (int i = 0; i <n ; i++) {
	    cin >> a[i] ;
	}
	vector<int> dp(n, 1) ;
	// len
	int mx_len = 1 ;
	for (int i = 1 ; i < n ; i++) {
	    for (int j = 0; j < i ; j++) {
	        if (a[j] < a[i]) {
	            dp[i] = max(dp[j] + 1 , dp[i]) ;
	        }
	    }
	    mx_len = max(mx_len , dp[i]) ;
	}
	cout << mx_len << endl ;
	
	return 0 ;

```

- SLIGHT OPTMISATION OVER THIS COULD BE TO ingnore `Consecutive Duplicates` as they don't contribute to LIS (has to be strictly increasing)
- But still O(M*M) where M -> reduced length of a (after removal of consecutive duplicates )
```cpp
#include <bits/stdc++.h>
using namespace std;
 
int main() {
	int n ;
	cin >> n ;
	vector<int> a ;
	int prev = -1 ;
	
	for (int i = 0; i < n ; i++) {
	    int e ; 
	    cin >> e ;
	    if (prev != e) {
	        prev = e ;
	        a.push_back(e);  
	    }
	}
	
	int m = a.size();
	vector<int> dp(m,1) ;
 
 
	int mx_len = 1 ;
	for (int i = 1 ; i < m ; i++) {
	    for (int j = 0; j < i ; j++) {
	        if (a[j] < a[i]) {
	            dp[i] = max(dp[j] + 1, dp[i]) ;
	        }
	    }
	    mx_len = max(mx_len , dp[i]) ;
	}
	cout << mx_len << endl ;
	
	return 0 ;
```
### BEST  OPTIMISED APPROACH :
- trace the `smallest tail` of any length LIS[i]
- Because if 2 LIS of same len is present than the likeliness of extending the one with smaller end is more as we have more options of next ele of LIS
- If the any prev tail with val >= curr_num present than curr_num can be a smaller tail of that LIS  => UPDATE THE TAIL TO MINIMISE TAIL VALUE
- Else curr_num greatest to all prev tails (END OF LIS formed so far) extend the LIS with new TAIL  -> Extend LIS

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	int n ;
	cin >> n ;
	vector<int> a ;
	int prev = -1 ;
	
	for (int i = 0; i < n ; i++) {
	    int e ; 
	    cin >> e ;
	    if (prev != e) {
	        prev = e ;
	        a.push_back(e);  
	    }
	}
	
	int m = a.size();

	vector<int> tails ;// end upto ith index
	
	for (int i = 0 ; i < m ; i++) {
	    int prev = lower_bound(tails.begin() , tails.end() , a[i]) - tails.begin() ; 
	    if (prev >= 0 && prev < tails.size()) {
	        tails[prev] = min( a[i] , tails[prev] ) ;
	    }else { // extend to make longert  lis 
	        tails.push_back(a[i]) ;
	    }
	}

	cout << tails.size() << endl ;

	
	return 0 ;
}
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N*LOGN) |  For every ith index , Binary seacrch over prev_tail values |
| 🧠 SPACE |    O(N)        |  LIS (TAIL) Array          |
