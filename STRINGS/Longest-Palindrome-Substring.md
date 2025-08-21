# Longest-Palindrome-Substring

```cpp
#include <bits/stdc++.h>
using namespace std;
int expand(int l, int r , const string& s) {
    int n = s.length();
    int len = 0 ;
    bool mismatch = false ;
    while(l >= 0 && r < n) {
        if (s[l] != s[r]) {
            len = max(len , r - l - 1);
            mismatch = true ;
            break ;
        }
        l-- ; r++ ;
    }
    if (!mismatch) {
        len = max(len , r - l - 1);
    }
    
    return len ;
}
int main() {
	string s ;
	cin >> s ;
	int n = s.length();
	int max_len = 1 ;
	string res = "" ;
	res += s[0] ;
	
	for (int i = 0 ; i < n-1 ; i++) {
	    int odd = expand(i , i , s);
	    int even = expand(i , i+1 , s);
	   // cout << odd << " & " << even << endl ;
	    if (max_len < max(odd,even)) {
	        int r = odd > even ? 0 : 1 ;
	        max_len = max(odd,even);
	        
	        if (odd > even) {
	            res = s.substr(i - max_len/2 , max_len) ;
	        }else {
	            res = s.substr(i - max_len/2+1 , max_len) ; 
	        }
	    }
	}
	
// 	cout << max_len << endl ;
	cout << res << endl ;
	
	return 0 ;
}
```
- But this will undergo TLE because of O(N*N) complexicity !

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |     O(N*N)  |  for e          |
| 🧠 SPACE |            |            |
