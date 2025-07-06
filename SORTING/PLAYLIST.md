# LONGEST SEQUENCE OF UNIQUE SONGS from PLAYLIST 

### INTUITION : 2 POINTER {whenever you encounter second occurence of any element in the seq , slide the leftPointer to the right of previous occurence of the same element encounter currently .

```cpp
#include <bits/stdc++.h>
#include <bitset>
using namespace std;
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) 

int main() {
    FASTIO ;
    int n ;
    cin >> n ;
    
    int start = 1 , mx = 1 ;
    map<int,int> lastPos ;
    for (int i = 1 ;i <= n ; i++) {
        int ele ;
        cin >> ele ;
        if (lastPos[ele] >= start) {
            start = lastPos[ele] + 1 ;
        }
        lastPos[ele] = i ;
        mx = max(mx , i - start + 1) ;
    }
    cout << mx << endl ;
    
    return  0;
}
```

📊 Complexity Analysis
| Metric	              |Complexity |	Description   |
|-----------------------|-----------|--------------------|
| Time Complexity       | O(n)      | {Sliding window with hashmap} |
| Space COMPLEXICITY    | O(n)      | HashMap (to keep last occurence of elements) |
