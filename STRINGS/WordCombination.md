# WORD COMBINATIONS

- FIRST Approach would be to get set of all dictionary words in set and check for the substring in s , whether do they come in dictionary and mark ending index to use it as a starting point of other substring of s in dictionary to get all possible ways of forming s .
##### BUT TLE (As check every substr in the set taken O(n*n) time in worst case) 

```cpp
#include <bits/stdc++.h>
#define MOD 1000000007  
#define ll long long 
using namespace std;
 
int main() {
	string s ;
	cin >> s ;
	int k ;
	cin >> k ;
	set<string> set ;
	for (int i = 0; i < k ; i++) {
	    string word ;
	    cin >> word ;
	    set.insert(word) ;
	}
	int n = s.length();
	
	vector<ll> dp(n+1 , 0LL) ;
	dp[0] = 1LL ;
	for (int i = 1; i <= n ; i++) {
	    for (int j = 0; j < i ; j++) {
	        if (dp[j] > 0 && set.find(s.substr(j , i-j)) != set.end()) {
	            dp[i] = (dp[i] + dp[j]) % MOD;
	        }
	    }
	}
	
	cout << dp[n] << endl;
	return 0 ;
}`


```

## OPTIMISED VERSION (Use trie to mark the end of any of the string in word and then get the ways if the prevEnding Idx + 1 will become the start of any other word in dictionary !)
```cpp
#include <bits/stdc++.h>
#define ll long long
#define MOD 1000000007 ;
using namespace std;
struct TrieNode{
   bool EOW = false;
   vector<TrieNode*> children ;
   TrieNode() : children(26, NULL) {}
};
void add(TrieNode* root , const string& s) {
    TrieNode* curr = root ;
    for (char c : s) {
        if (!curr->children[c-'a']) {
            curr->children[c-'a'] = new TrieNode();
        }
        curr = curr->children[c-'a'] ;
    }
    
    curr->EOW = true ;
}
int main() {
	string s ;
	cin >> s ;
	int k ;
	cin >> k ;
	
	TrieNode* root = new TrieNode();
	for (int i = 0 ; i < k ; i++) {
	    string word ;
	    cin >> word ;
	    add(root,word) ;
	}
	
	int n = s.length() ;
	TrieNode* curr = root ;
	vector<ll> dp(n+1 , 0LL ) ;
	dp[0] = 1LL ;
	
	for (int i = 0 ; i < n ; i++ ) { // previous computations
	    if (dp[i] == 0) continue ;// no word starting at i 
	    TrieNode* curr = root ;
	    for (int j = i ; j < n ; j++) {
	        if ( !curr->children[s[j]-'a'] ) break ;
	        curr = curr->children[s[j]-'a'] ;
	        if (curr->EOW){
	            dp[j+1] = (dp[j+1] + dp[i])%MOD ;
	        }
	    }
	}
	
	cout << dp[n] << endl ;
	
     return 0;
}

```


# 🔍 Complexity Analysis

| METRIC   | COMPLEXICITY  |    HOW ? |
|-----------|-------------|------------|
| 🧭 TIME  |  O(n*L + k*L)          | O(k*len(word)) to Make trie + O(n) : to traverse through string s of length n |
| 🧠 SPACE | O(n + totalNodes)        |   Trie for the string + Dictionary words {Optmally saved as common prefix are shared by all words} |
