# LONGEST COMMON SUBSEQUENCE 
## B/w 2 given arrays a1 , a2  of size n , m respectively 
### Do print one of the longest common subsequence 
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std ;
const int N = 1001 ;
int a1[N] , a2[N]  , dp[N][N] ;
int main() {
	FASTIO ;
	int n , m ;
	cin >> n >> m ;
	for (int i = 0; i < n ; i++) cin >> a1[i] ;
	for (int j = 0; j < m ; j++) cin >> a2[j] ;
	for (int i = 1 ; i<= n ; i++) {
	    for (int j = 1; j <= m ; j++) {
	        if (a1[i-1] == a2[j-1]) {
	            dp[i][j] = 1 + dp[i-1][j-1] ;
	        }else {
	            dp[i][j] = max(dp[i-1][j] , dp[i][j-1]);
	        }
	    }
	}
	cout << dp[n][m] << '\n';
	function<void(int,int)> printLCS = [&](int i, int j) {
	    if (i == 0 || j == 0) return ;
	    if (a1[i-1] == a2[j-1]) {
	        printLCS(i-1 , j-1) ;
	        cout << a1[i-1] << " ";
	    }else if (dp[i-1][j] >= dp[i][j-1]) {
	        printLCS(i-1 , j);
	    }else {
	        printLCS(i , j-1);
	    }
	};
	
	printLCS(n , m) ;

	cout << '\n' ;
}
```

📊 COMPLEXICITY ANALYSIS :

| Complexicty             | Calculation | How |
|-------------------------|------------------|------------------------------------| 
| Time Complexicity 	  | O(n*m) + O(n+m) |Creation of table , Forming subsequence|
|Space Complexicity 	  |O(n*m) + O(min(n,m))| Creation of table , Forming subseq |
