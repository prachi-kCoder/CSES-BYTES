# Distinct-Values-Subarray

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n ;
    cin >> n ;
    vector<int> nums(n) ;
    for (int i = 0; i <n ; i++) {
        cin >> nums[i] ;
    }
    // windows 
    map<int,int> mp ;
    long long ans = 0LL ;
    int l = 0 ;
    for (int r = 0 ; r < n ; r++) {
        if (mp.find(nums[r]) != mp.end() && mp[nums[r]] >= l) {// reocc
            int len = r - l  ;
            ans += (1LL*len*(len+1))/2 ;
            int prev_idx = mp[nums[r]] ;
            // repeated 
            int r_len = r - prev_idx - 1 ;
            long long r_sub_cnt = (1LL*r_len*(r_len + 1))/2 ; 
            ans -= r_sub_cnt ;
            
            l = max(l ,prev_idx+1 ) ;
        }
        
        mp[nums[r]] = r ; // update 
    }
    int len = (n-1) - l + 1 ;
    ans += (1LL*len*(len+1))/2 ;
    cout << ans << endl ;
	return  0 ;
}
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC | 📈 COMPLEXITY | 🧩 EXPLAINATION |
|-----------|--------------|----------|
| 🧭 TIME  |    O(N)      |  O(N)  |
| 🧠 SPACE |    O(1)      |  O(1)  |



