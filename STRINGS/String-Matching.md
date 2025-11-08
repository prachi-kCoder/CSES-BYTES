# String-Matching

- KMP Algorithm : To compute the longest prefix suiffix of any string , eliminating the need to match the complete pattern starting from every ith index as in Brute force we do
- ### KNUTH MORRIS PRAT :
- Compute LPS of the pattern to use to while match to the given s string
- `The core idea is that when a mismatch occurs, we don't need to backtrack the text pointer. Instead, we use the precomputed lps array to figure out how many characters to shift the pattern to the right, so we can continue the comparison from where we left off in the text string. This is possible because the lps array tells us the length of the longest proper prefix of a substring that is also a suffix of the same substring.`


```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> get_lps(const string& pat) {
    int m = pat.length();
    vector<int> lps(m, 0) ;
    int i = 1 ;
    int len = 0 ;
    while (i < m) {
        if (pat[i] == pat[len]) {
            len++ ;// increased len 
            lps[i] = len ;// mark increased len 
            i++ ; // update pointer
        }else if (len != 0) { // some lps exist so continue from there on 
            len = lps[len-1] ;
        } else { 
            len = 0 ;
            lps[i] = 0 ;// NOT LPS 
            i++ ;
        }
    }
    return lps ;
}

int main() {
	string s , pat ;
	cin >> s ;
	cin >> pat ;
	int n = s.length() ; int m = pat.length(); 
	if (n < m){
	    cout << 0 << endl ;
	    return 0 ;
	}else if (n == m) {
	    cout << (s == pat) << endl ;
	    return  0 ;
	}
	vector<int> lps = get_lps(pat) ;
	
	int i = 0 ,j = 0 , count = 0 ;// iterate over pattern
	
    while (i < n) {
        if (s[i] == pat[j]) {
            i++ ; j++ ;
            if (j == m) { // pattern found
                count++ ;
                j = lps[m-1] ;
                // Start matching with the lps len now for the next occ {As it is in prefix & suffix too !!}
                
            }
        } else if (j == 0 ){// notmatched
            i++ ;
        } else {
            j = lps[j-1] ; // len in pattern
        }
    }
	cout << count << endl ;
	
	return 0;
}

```


# 🔍COMPLEXICITY ANALYSIS

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N+M)       |  Compute lps , then traverse the string s to match pattern & used the preComputed lps of pattern {efficiently eliminating the need to reset i to match the whole pattern from start }          |
| 🧠 SPACE |    O(M)      |  LPS Array for pattern          |
