 # Elevator-Rides

 ### backtracking: bin-packing is the brute force approach with all lifts with remaining tiem recorded but undergoes TLE

 ### DP- BITMASKING ;
 - Explore all possibile initial assinment of persons to lifts and using these initial assigment of person , we can assign the rides to the remaining ones keeping the rides minimum,
- Dp[state]  state {How many persons are assigned } - mask
- Dp[mask] = {ride_cnt , occupied_wt}  This lets us to determine whether any unassigned be place in the same ride / increasing the ride_cnt in case the occupied_wt > x
  Keep the min cnt , if dp[mask] = {0,0} ie the unexplored state !
  
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n ,x ;
    cin >> n >> x ;

    
    vector<int> wt(n) ;
    for (int i = 0 ; i < n ; i++) {
        cin >> wt[i] ;
    }
    
        // all different assignments
    vector<pair<int,int>> dp((1<<n)) ;// state when all person are lifted
    //rides , weight_occupied 
    
    dp[0] = {1,0} ;// ie 1 ride with 0 wt occupied 
    
    for (int mask = 0; mask < (1<<n) ; mask++){
        for (int i = 0 ; i < n ; i++ ) {
            if (!(mask&(1<<i))) {// if person is not assigned !
                // assigning in the same lift 
                pair<int,int> new_state = {dp[mask].first, dp[mask].second + wt[i]} ;
                if (new_state.second > x) {
                    new_state.first++;
                    new_state.second = wt[i] ;
                }
                int nxt = (mask|1<<i) ;
                if (dp[nxt].first == 0 && dp[nxt].second == 0) {
                    dp[nxt] = new_state ;
                } ;
                dp[nxt] = min(dp[nxt], new_state) ;
            }
        }
    }
    cout << dp[(1<<n)-1].first << endl ;
    
    return  0 ;
}
                
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC   | 📈 COMPLEXITY     | 🧩 EXPLANATION |
|------------|------------------|----------------|
| 🧭 TIME     | O(2^N * N)       | For each of the 2^N subsets (bitmask), we try assigning the last person to a ride. For each subset, we may iterate over N people to check feasibility. |
| 🧠 SPACE    | O(2^N)           | DP table indexed by bitmask (subset of people), storing `{ride_count, occupied_weight}` for optimal ride configuration. |
