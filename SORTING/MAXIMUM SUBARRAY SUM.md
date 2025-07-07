# APPLY KADANE'S ALGORITHM 
### mxSum stores the global maximum subarray sum found so far.
### currSum is the current running sum of the subarray under consideration. 
- currSum allows us to whether the overall contribution of subArray is positive or negative , include any subArray only if a positive contiribution . Otherwise start new subarray ie why currSum = 0
 

```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0)
#define ll long long 
using namespace std;
const int N = 2e5 + 1 ;
 
int main() {
	FASTIO ;
	int n ;
	cin >> n ;
	ll mxSum = LLONG_MIN; ll currSum = 0 ;
	for (int i = 0; i < n ; i++) {
	    int ele ;
	    cin >> ele ;
	    currSum = (currSum + ele) ;
	    mxSum = max(mxSum , currSum) ;
	    if (currSum < 0) {
	        currSum = 0 ;
	    }
	}
	cout << mxSum << endl ;
	return 0;
 
}
```
## ⏱️ Complexity Analysis
|   Metric	  |   Value   | 
|-------------|-----------|
|🕒 Time Complexity| O(n) – Single pass through the array. |
|🧠 Space Complexity	O(1) | Only constant extra space used (mxSum, currSum). |
