# PROJECTS 

#### Just understand with this first the intuition 
- This will give you RUN TIME ERROR (but good for deeper understanding about the approach) :
```cpp

```


- Now rather that consider dp[i] = Max reward upto ith day
- Make a dp such that dp[i] = Max reward upto ith project !!
  
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

