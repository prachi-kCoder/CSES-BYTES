# Finding-Periods.md
- as the same Prefix is to be repeated so that to make the whole string , like the string which is PREFIX + SUFFIX so obvoiusely we need LPS
- So for the full string `s[0..n-1]`, `lps[n-1]` gives the length of the longest prefix that is also a suffix of the entire string.
- But here’s the magic: that prefix might itself have a period, and so on recursively.
- k = lps[n-1] LONGEST  prefix-suffix of full string
- lps[k-1] given longest prefix-suffix of that prefix
- lps[lps[k-1]] further givens next longest prefix-suffix !
  
```cpp

  #include <bits/stdc++.h>
  using namespace std;
   
  void print(const vector<int>& a) {
      for (int e : a) {
          cout << e << " ";
      }
      cout << endl;
  }
   
  vector<int> get_lps(const string& s) {
      int n = s.length();
      vector<int> lps(n, 0);
      int i = 1, len = 0;
      while (i < n) {
          if (s[i] == s[len]) {
              len++;
              lps[i] = len;
              i++;
          } else {
              if (len != 0) {
                  len = lps[len - 1];
              } else {
                  lps[i] = 0;
                  i++;
              }
          }
      }
      return lps;
  }
  int main() {
  	string s ;
  	cin >> s ;
  	int n = s.length();
  	
  	vector<int> lps = get_lps(s) ;
  	vector<int> ans ;
  	ans.push_back(n) ;
  	int k = lps.back() ;
  	
  	while (k > 0) {
  	    ans.push_back(n-k); // prefix len ie not at suffix 
  	    k = lps[k-1] ;
  	}
  	
  	sort(ans.begin() , ans.end()) ;
  	print(ans) ;
  }
```

# 🔍COMPLEXICITY ANALYSIS

| 📊 METRIC  | 📈 COMPLEXITY	  |  🧩 EXPLAINATION |
|-----------|-------------|------------|
| 🧭 TIME  |   O(N)       | LPS Array calculation + Reverse traversal of the lps[curr lps length-1] |
| 🧠 SPACE |   O(N)     |  LPS Array          |

