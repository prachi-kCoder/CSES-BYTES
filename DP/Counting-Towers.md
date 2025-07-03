# COUNTING TOWERS
### Width : 2  , Height : n {1 <= i <= n} ie i will vary and based on it we get all possibilities of arranagements
### One this that is don't get confused with mirror image, rotations ie just to confuse you how can we count the rotations .. to complicate the thinking part
### We will go with all possible arrangements of block to fill up the grid {because if we do 90 deg rotation so if n != 2 then the grid is not valid and 180 deg rotation of any arrangement gives us another arrangement of blocks used to fill up the grid !}

- WIDTH = 2 {j values {0,1}} ie Either a horizontal block {j = 0} of width 2 or a 2 vertical block of width 1 {j=1}
- Height = i {1 <= i <= n} this is what determinse all arrangements

  - dp[i][0]  : No. of ways upto ith height that the preceding blocks are horizontals {upto ith height} to fill the grid
  ### dp[i][0] = 2*dp[i+1][0]  + dp[i+1][1]
  
  -dp[i][1]  : No. of ways upto ith height that the preceding blocks are vertical {upto ith height} to fill the grid
  ### dp[i][1] = 4*dp[i+1][1]  + dp[i+1][0]

  ```cpp
  #include <bits/stdc++.h>
  #define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
  #define ll long long 
  #define M 1000000007 
  using namespace std;
  
  ll dp[(int)1e6+5][2] ;
  int main() {
      FASTIO ;
      int t ;
      cin >> t ;
      while (t-- > 0) {
          int n ;
          cin >> n ;
          // 1 -> Vertical Columns , 0 -> Horizontal Blocks
          dp[n][0] = 1LL , dp[n][1] = 1LL ;
          for (int i = n-1 ; i> 0 ; i--) {
              // Horizontal filler {3 Cases}
              dp[i][0] = (2LL*dp[i+1][0] + dp[i+1][1])%M ;
              // Vertical filler {5 Cases}
              dp[i][1] = (4LL*dp[i+1][1] + dp[i+1][0])%M;
          }
          // Last Row gives the sum of all possibilities of arranging these blocks {Horizontal + Vertical}
          cout << (dp[1][0] + dp[1][1])%M << endl ;
      }
  }
``` 

``` cpp
	#include <bits/stdc++.h>
	#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
	#define ll long long 
	#define M 1000000007 
	using namespace std;
	
	ll dp[(int)1e6+5][2] ;
	int main() {
	    FASTIO ;
	    int t ;
	    cin >> t ;
	    
	    // while (t-- > 0){
	    //     int n ; 
	    //     cin >> n ;
	    //     ll vertical = 1LL , hori = 1LL ;
	    //     for (int i = n-1 ; i > 0 ;i--) {
	    //         ll newHori = (2LL*hori + vertical) %M;
	    //         ll newVertical = (4LL*vertical + hori) %M;
	    //         vertical = newVertical ;
	    //         hori = newHori ;
	    //     }
	    //     cout << ( vertical + hori)%M << endl ;
	    // }
		
	}
```

### COMPLEXICITY ANALYSIS : 
## TIME COMPLEXICITY  : O(2*n*t)  t-> No. of test cases
## SPACE COMPLEXICITY  : Approach 1 : O(2*n)  ,  Approach 2 : O(1)  

