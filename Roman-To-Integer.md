# ROMAN TO INTEGER
```cpp
int romanToInt(string s) {
        int val[26] = {} ;
        val['I'-'A'] = 1 ; val['V'-'A'] = 5 ;
        val['X'-'A'] = 10 ; val['L'-'A'] = 50 ;
        val['C'-'A'] = 100 ; val['D'-'A'] = 500 ;
        val['M'-'A'] = 1000 ;

        int n = s.length();
        int num = 0 ;
        char prev = '*' ;
        for (int i = 0; i < n ; i++ ) {
            if (prev != '*' && val[prev-'A'] < val[s[i]-'A']) {
                num -= 2*val[prev-'A'] ;
            }
            num += val[s[i]-'A'] ;
            prev = s[i] ;
        }

        return num ;
    }
```
Complexicity  : 
TIME : o(N) , SPACE : O(26) approx O(1) constant space !
