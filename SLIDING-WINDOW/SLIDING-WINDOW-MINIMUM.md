# SLIDING WINDOW MINIMUM 
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
#define ll long long 
const int N = 1e7 + 1 ;
int arr[N] ;
int main() {
    FASTIO ;
    int n , k ;
    cin >> n >> k ;
    int x , a, b, c ;
    cin >> x >> a >> b >> c ;
    arr[0] = x ;
    
    for (int i = 1 ; i < n ; i++) {
        arr[i] = (1LL*arr[i-1]*a + b)%c ;
    }
    if (n == 1) {
        cout << 1 << endl;
        return 0;
    }
    ll XOR = 0LL ;
    
    if (k == 1) XOR = arr[0] ;
    int mnIdx = 0 , mnVal = arr[0] ;
    priority_queue<pair<int,int>, vector<pair<int,int>> , greater<pair<int,int>>> minHeap ;
    minHeap.push({arr[0] , 0});
    for (int i = 1 ; i < n ; i++) {
        minHeap.push({arr[i] , i}) ;
        if ( i >= k-1 ) {
            int l = i - k + 1;
            while (!minHeap.empty() && minHeap.top().second < l) minHeap.pop();
            int mnVal = minHeap.top().first ;
            XOR ^= mnVal ;
        }
    }
    
    cout << XOR << endl;
	return 0 ;
}
```
## COMPLEXICITY ANALYSIS 
| METRIC  |   COMPLEXICITY   |  HOW ?  | 
|---------|-------------------|----------|
| TIME    |  O(n + n*logn)       | Array creation + Heap Insertion (logn) for n elements (in worst case) |
| SPACE   |  O(n + n)            | PriorityQueue + Array used |


# OPTMISED APPROACH : (Using DEQUE (Double Ended Queue))
### Deque : Here is to keep the minVal Index , 
- we take the minValue Idx from front
- Check if the minValue Idx is out of window front left side then pop from front
- Keep track of minVal encountered will sliding the window towards right and keep push the new minVal from the back 
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
#define ll long long 
const int N = 1e7 + 1 ;
int arr[N] ;
int main() {
    FASTIO ;
    int n , k ;
    cin >> n >> k ;
    int x , a, b, c ;
    cin >> x >> a >> b >> c ;
    arr[0] = x ;
    
    for (int i = 1 ; i < n ; i++) {
        arr[i] = (1LL*arr[i-1]*a + b)%c ;
    }
    if (n == 1) {
        cout << 1 << '\n';
        return 0;
    }
    ll XOR = 0LL ;
    deque<int> dq ;// keep the index in the minVal of nums 
    
    for (int i = 0 ; i < n ; i++) {
        while (!dq.empty() && arr[i] <= arr[dq.back()]) dq.pop_back();
        dq.push_back(i) ;
        
        if (!dq.empty() && dq.front() <= i-k) dq.pop_front();
        
        if ( i >= k-1 ) {
            XOR ^= arr[dq.front()] ;
        }
    }
    cout << XOR << '\n';
	return 0 ;
}
```
## COMPLEXICITY ANALYSIS 
| METRIC  |   COMPLEXICITY  |  HOW ?  | 
|---------|-----------------|----------|
| TIME    |  O(n + n)       | Array creation + Deque for n elements |
| SPACE   |  O(n + n)       | PriorityQueue + Array used |
