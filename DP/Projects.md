# PROJECTS 

#### Just understand with this first the intuition 
- This will give you RUN TIME ERROR (but good for deeper understanding about the approach) :
- `take` or `skip` : 2 options for any of the project
Here dp[i] : represents max_rewards gained upto ith day , and if ith day is the end of any of the project (consider the take option)

```cpp
#include <bits/stdc++.h>
using namespace std;
struct Project{
    int s , e, g ;
};
bool compare(const Project& p1 , const Project& p2) {
    return p1.e < p2.e ;
};
int main() {
	int n;
    cin >> n;
    vector<Project> v(n);
    int mx_t = 0 ;
    for (int i = 0; i < n; i++) {
        cin >> v[i].s >> v[i].e >> v[i].g;
        mx_t = max(mx_t , v[i].e );
    }
    sort(v.begin(), v.end() , compare) ;
    vector<long long> dp(mx_t + 1,0LL );
    int j = 0 ;
    for (int i = 1 ; i <= mx_t ; i++) {
        dp[i] = dp[i-1] ;
        
        while(j < n && v[j].e == i) {
            int st = v[j].s ;
            int gain = v[j].g ;
            dp[i] = max( dp[i] , dp[st-1] + gain );
            j++ ;
        }
    }
     
    cout << dp[mx_t] << endl ; 
 
};
```


- Now rather that consider dp[i] = Max reward upto ith day
- Make a dp such that dp[i] = Max reward upto ith project !! (Because max_end_day is large in out case or it will cause runtime error)
- Optimised space complexicity
- Binary search for any of the project with start time s[i] , find the max gain with the project end before the curr_project start time!
  
```cpp
#include <bits/stdc++.h>
using namespace std;
struct Project{
    int s , e, g ;
};
bool compare(const Project& p1 , const Project& p2) {
    return p1.e < p2.e ;
};
int main() {
	int n;
    cin >> n;
    vector<Project> v(n);
    int mx_t = 0 ;
    for (int i = 0; i < n; i++) {
        cin >> v[i].s >> v[i].e >> v[i].g;
        mx_t = max(mx_t , v[i].e );
    }
    sort(v.begin(), v.end() , compare) ;
    
    vector<long long> dp(n , 0LL) ;
    vector<int> pe(n) ;
    

    for (int i = 0; i <n ; i++) {
        pe[i] = v[i].e ;
    }
    for (int i = 0; i < n ; i++) {
        long long take = v[i].g ;
        long long skip = (i > 0) ? dp[i-1] : 0 ;
        
        int pos = lower_bound(pe.begin() , pe.end() , v[i].s ) - pe.begin() ;
        if (pos > 0) {
            take += dp[pos-1] ;
        }
        dp[i] =  max(take , skip ) ;
    }
     
    cout << dp[n-1] << endl ; 
    
    return  0 ;
};
```


## 🔍 COMPLEXITY ANALYSIS

| METRIC     | COMPLEXITY   | EXPLANATION |
|------------|--------------|-------------|
| 🧭 TIME     | O(n·log n)    | For each of the n projects, perform binary search over the sorted `project end_time` array |
| 🧠 SPACE    | O(n)          | Space for `dp` array and `end_time` array (`pe[]`) |


