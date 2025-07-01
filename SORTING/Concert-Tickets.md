## Simple Problem to assign ticket to customers 
### All customers have mxPrice that they can at max pay 

### Tricky thing here people get confused with is change in the meaning of lower_bound() , upper_bound()  these work based on the sequence you're applying over
### We take multiset to keep tickets sorted and in Descending Order ?

### WHY DESCENDING ?
- - Because while assigning tickets to any person , we need to ensure the maxPriced ticket are given out if asked by any custormer having high max price
  - Assigning tickets to customers in way so that the price of ticket given away <= mxPrice{affordable to customer}
  - When multiset is in ascending order :- mn.lower_bound(ele)  gives it pointing to a pt >= ele  
  - Eg ms : {2,3,5,7,8,9}  *mn.lower_bound(6) = 7
  - When multiset is in descending order :- mn.lower_bound(ele)  gives it pointing to a pt <= ele
  - Eg dms : {9,8,7,5,3,2}  *mn.lower_bound(6) = 5
 
  ### Order of sequence matter here !!
  
```cpp
#include <bits/stdc++.h>
#define ll long long 
using namespace std;
int main() {
    int n , m ;
    cin >> n >> m ;
    ll temp ;
    multiset<ll,greater<ll>> t ;// tickets in desc 
    for (int i = 0; i < n ; i++) {
        cin >> temp ;
        t.insert(temp) ;
    }
    vector<ll> custMx(m) ;
    for (int i = 0; i < m ; i++) {
        cin >> custMx[i] ;
    }
    
    for (int j = 0; j < m ; j++) {
        auto it = t.lower_bound(custMx[j]);
        if (it == t.end()) {
            cout << -1 << endl ;
        }else {
            cout << *it << endl ;
            t.erase(it);
        }
    }
}
  
```

# COMPLEXICITY ANALYSIS :
## 🧮 Time Complexity (TC) 
### Insertion in multiset : logn (for n tickets) , for m customers {lower_bound-> logn}
- O(n log n + m log n) = O((n + m) log n)
## 🧠 Space Complexity 
- (SC) = O(m + n) 
 
