# Square-Root-Decomposition

- To get the sum of divisors of all divisor `[1,N]`  (CSES problem)

- what we need is :
- As for number 1-N all num in range have multiples (ie acting as a divisor of bigger nos in range so all i [1,N] are needed to be added repeted;y)
- Eg [1,10] : 1 {divisor of all so need to be added 10 times} , 2 {to be added 5 times} , 3 {to be added 3 times} ....
- hence for any num i = [1,N] are acting as a divisor N/i times
- But if constraints are high O(N) is also not allowed hence `O(N) -> O(sqroot(N))` by `SQUARE ROOT DECOMPOSITION`

```
   S(N)=d 1∑N  ​d⌊dN​⌋

🔹 Key observation: 
 
For small d, values of ⌊ 𝑁 / 𝑑 ⌋  are large but distinct. 
For large d, values of ⌊N/d⌋ repeat for ranges of d.

```
Eg N=10 :
| DIVI     |  times(v)     |
|----------|---------------|
|  1       |     10/1 = 10   |
|  2       |     10/2 = 5   |
|  3       |     10/3 = 3  |
|  4 or 5      |     10/4 or 10/5 = 2   |
|  6/7/8/9/10      |     10/{6 /.../10} = 1   |

👉 We can group equal quotients together. You can see that for many consecutive d’s, `floor(N/d)` is the same.

# Trick (Dirichlet Hyperbola / sqrt decomposition)
```
For a fixed v = floor(N/d):
      - the smallest d giving this v is d_low = floor(N/(v+1)) + 1
      - the largest d giving this v is d_high = floor(N/v)
    So you can compute the contribution for all d in [d_low, d_high] at once.
```

<img width="976" height="516" alt="image" src="https://github.com/user-attachments/assets/64616398-1572-4f05-beea-64477921dfa5" />
<img width="1094" height="635" alt="image" src="https://github.com/user-attachments/assets/047270ea-4151-45b8-a93e-87483e58dc03" />
<img width="986" height="550" alt="image" src="https://github.com/user-attachments/assets/0f8dd6a3-b856-4f19-b792-aba20eea5336" />


- To get the sum of ```range[L,R] = (R+L)*( R- L + 1) /2```
