### Here unordered_set is less favourable (it gives run time error) : Due to hashing overhead 
## THEORETICAL STANDPOINT :
- unordered_set offers amortized O(1) insertion and lookup (thanks to hashing)
- set offers O(log n) insertion and lookup (because it uses a balanced BST)

## 🔍 So... Why Did set Perform Better in our case ?
- When inputs are large and adversarial (like many random-looking values up to 1e9), unordered_set can suffer from hash collisions, degrading performance toward O(n)
- unordered_set involves pointer chasing and hashing overhead, which can wreak havoc with CPU caching and branch prediction—especially with massive datasets.
 
- set has predictable access patterns due to its tree structure. 


```cpp
#include <iostream>
#include <set>
using namespace std;

int main() {
    int n;
    cin >> n;
    set<int> s; // ordered but efficient for this problem
    for (int i = 0; i < n; ++i) {
        int e;
        cin >> e;
        s.insert(e);
    }
    cout << s.size() << endl;
    return 0;
}
```
