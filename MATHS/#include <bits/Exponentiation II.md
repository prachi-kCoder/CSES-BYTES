# Exponentiation II


Concept : 
- Fermat's Little Theorem gives us the key. If $m$ is a prime number:
  - a^{m-1} =  1 % m
`m`-> Prime NO
```
- This is the magic trick. It means that a's powers repeat every (m-1) times.  -
- a^1 mod m = a^1
- a^2 mod m = a^2
- ...
- a^m-1 mod m = 1 mod m = 1 
- a^m mod m = a . a^m-1 mod m = a . 1 % m = a ^ 1 {Here repetition starts }
- a^(m+1) mod m = a^2 . a^m-1 mod m = a^2 . 1 % m = a ^ 2

- Our problem is a^E mod{m}, where the exponent E = b^c.
- So we cal E with m-1 expo
- And then a mod E with m expo
```
  
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
ll mod_expo(ll base , ll expo, ll mod) {
    ll res = 1LL ;
    expo %= mod ;
    while (expo > 0) {
        if (expo&1)  res = (res*base)%mod ;
        base = (base*base)%mod ;
        expo >>= 1 ;
    }
    return res ;
}
int main() {
	ll n ;
	cin >> n ;
	while (n -- > 0) {
	    ll a , b , c ;
	    cin >> a >> b >> c  ;
	    ll mod = (ll)1e9 + 7 ;
	    ll e = mod_expo(b , c, mod-1)  ;
	    cout << mod_expo(a, e, mod) << endl ;
	}

}

```
