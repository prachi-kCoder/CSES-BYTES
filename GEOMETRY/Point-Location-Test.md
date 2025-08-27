## Point-Location-Test

- Here rather than going with the conventional method of satisfying a point with in the equation & get us with the intuition of relation position may not always gives accurate result due to floating point correction
- USE `CROSS-PRODUCT`
- 3 pts : `A` : `{x1,y1}` , `B`:`{x2,y2}` , `C` :`{x3,y3}`
- 2 Vectors :
-   `AB : ( x2-x1 , y2-y1 )` , `AC : {x3-x1 , y3-y1}`
-  `AB x AC` => Shows signed paralleogram between the vectors
  
|   sign | What is means ?  |
|----------|------------------|
| POSITIVE  | Counter Clockwise movement from AB TO AC so (+ve )  hence C is on Left of AB |
| NEGATIVE  |  Clockwise movement from AB TO AC so (-ve )  hence C is on Right of AB |
| ZERO      |  A , B, C all collinear so C touches the line passing via A & B |


- Now `CROSS PRODUCT` is by matrix multiplication between `AB` , `AC`
  |  x2-x1   |  y2-y1|
  |---------|--------|
  | x3-x1  |  y3-y1  |
  
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t ;
    cin >> t ;
    
    while (t-- > 0) {
        int x1 , y1 , x2 ,y2 , x3 , y3 ;
        cin >> x1 >> y1 >> x2 >> y2 >> x3 >> y3 ;
        
        long long val = 1LL*(x2-x1)*(y3-y1) - 1LL*(y2-y1)*(x3-x1) ;
        
        if (val == 0LL) {
            cout << "TOUCH" << endl ;
        }else if (val > 0LL) {
            cout << "LEFT" << endl ;
        }else {
            cout << "RIGHT" << endl ;
        }
    }
    
    
    return 0;
}

```
TC = SC = O(1)
