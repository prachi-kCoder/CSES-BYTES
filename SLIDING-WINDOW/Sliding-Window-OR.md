# Sliding-Window-OR
- 2 Stack Approach allows to get the or of a range of value and reverting the in-stack to out-stack allows to delete element from top of out stack (bottom most is in-stack ie ele which came earliest !)


```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long 
stack<pair<ll,ll>> in ;
stack<pair<ll,ll>> out ;

int main() {
	int n, k;
    cin >> n >> k;
    ll x, a, b, c;
    cin >> x >> a >> b >> c;
 
    vector<ll> v(n) ;
    v[0] = x;
    for (int i = 1 ; i < n; i++) {
        v[i] = (a * v[i - 1] + b) % c;
    }
    
    // 1st window 
    for (int i = 0; i <= k-1 ; i++) {
        ll prev_or = 0LL ;
        if (!in.empty()) {
            prev_or = in.top().second ;
        }
        in.push({v[i] , (prev_or|v[i])}) ;
    }
    ll ans = in.top().second ;// first_window or 
    
    for (int i = k ; i < n ; i++) {
        
        if (out.empty()) {
            while (!in.empty()) {
                auto c = in.top(); in.pop();
                ll prev_or = 0LL ;
                if (!out.empty()) {
                    prev_or = out.top().second ;
              }
                out.push({c.first , (c.first|prev_or)});
            }
        }
        // del the left ele = topMost at out 
        out.pop();
        ll prev_or = 0LL ;
        if (!in.empty()) prev_or = in.top().second ;
        in.push({v[i] , ( prev_or|v[i])});
        
        ll or_val = (out.empty()) ? in.top().second : (in.top().second|out.top().second) ;
        ans ^= or_val ;
    }
    
    cout << ans << endl ;
    return 0;
}

```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |    O(N)     | Every element at most be once contained by `in`-STACK or `out`-STACK ,so every element is processed 3 push in / transferred to out / pop() from out|
| 🧠 SPACE |    O(N)     |   O(N) - `in` / `out` stack |
