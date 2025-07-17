# REMOVAL GAME

## INTUTION : Rather than looking just for maximising score for the players , look for difference between scores (Player1 - Player2) 
- Why difference  ?
- Because each player is playing optimally then they won't be just considering to maximise their score but to ensure the next player score to be minimised ?
- - UNDERSTAND :
  -At any turn:
    - If it's Player 1's turn:
    - He picks either a[l] or a[r].
    - If he picks a[l], then the remaining subproblem is dp(l+1, r), and now it's Player 2's turn.
    - -So Player 1 gets: a[l] - dp(l+1, r)
#### (Why minus? 
- Because dp(l+1, r) is Player2's advantage in the remaining subarray — Player1 wants to reduce that.)
- Same for picking a[r]:
- Player 1 gets: a[r] - dp(l, r-1) , here dp(l,r-1) is the player2 advantage

- ## The difference of a[l] - dp[l+1, r]  & a[r] - dp[l , r-1]  this shows the Player1's advantage over the other Player2 hence take the maximum of the 2 advantage
 ```cpp
  dp(l, r) = max(
    a[l] - dp(l+1, r),
    a[r] - dp(l, r-1)
  )
  ```
### HOW TO GET THE MAX PLAYER'S SCORE 
- Dp show's the max difference alternating b/w the player (no matter which player's turn it is , showing optmal play)
- total = sum of all elements  &  diff = dp(0, n-1) (i.e., final difference Player 1 can enforce) , because Player1 starts the game 
- Let P1 = Player 1's final score & Let P2 = Player 2's final score
  ```cpp
  P1 + P2 = total   (because all elements are taken)
  P1 - P2 = diff    (because that’s what Player 1 enforced)
  
  => 2 * P1 = total + diff
  => P1 = (total + diff) / 2
  ```

## CODE SOLUTION 
```cpp
#include <bits/stdc++.h>
#define FASTIO ios_base::sync_with_stdio(0) , cin.tie(0) , cout.tie(0)
using namespace std;
#define ll long long 
ll solve(int l , int r , vector<int>& a, vector<vector<ll>>& dp){
    if (l > r) return  0 ;
    if (dp[l][r] != LLONG_MIN) return dp[l][r];
    
    ll left = a[l] - solve(l+1 , r , a , dp); 
    ll right = a[r] - solve(l , r-1 , a , dp); 
    return dp[l][r] = max(left, right) ;
}
int main() {
	 int n;
    cin >> n;
    vector<int> a(n); 
    for (int& x : a) cin >> x;

    vector<vector<ll>> dp(n, vector<ll>(n, LLONG_MIN));
    
	ll diff = solve(0, n-1 , a , dp);
	ll total = accumulate(a.begin(), a.end(), 0LL);
	cout << (total + diff)/2 << endl ;
	
	
	return  0 ;
}

```
