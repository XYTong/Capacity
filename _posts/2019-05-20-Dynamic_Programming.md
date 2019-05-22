---
layout: post
key: 1dp
title: Study Notes, Introduction to Algorithms, Dynamic Programming
---  

**Dynamic Programming** is similar to **Divide and Conqure**, which is, through making combination of  
solutions of **subproblems** to solve the Original Problem.  
By **Divide and Conqure** we divide problem into disjoint sub-problem, solve these problems recursively  
and combine them to solve then Original Problem.  
In opposite of DP, it applies in the case of overlapped sub-problem, which means different sub-problem  
has common sub-subproblem. In this case, **Divide and Conqure** will do many non-necessary works, solve  
the common sub-subproblem repeatedly. However DP-Algorithm solve each subproblem for only once.  

**steps of DP**:  

1. characterize a structure feature of an optimal solution.  
2. define the value of optimal solution recursively.  
3. caculate the value of optimal solution, normally from the bottom to the top.  
4. with all caculated information to structure a optimal solution.  

**Principle of DP**:  

1. optimal sub-struct.  
if the optimal solution of a problem include contains the solutions of its sub-problems, then we called, it  
has the feature of optimal sub-struct. So if a problem is fit to use DP, it's a good clue that if it obtain  
optimal sub-struct. (of course sptimal sub-struct means also suitble for **Greedy**)  
2. a solution of a subproblem has no influence on the onther subproblem form the same Source Problem. which  
means they are **independent**.  
example: the shortest unweighted path and the longest unweighted path.  
3. Overlapping subproblems. means the revursing caculate the same subproblem repeatedly instead of creating  
new subproblems.  


**Problems:**  

1. [123](https://xytong.github.io/Capacity/2018/05/17/D_XORpyramid.html)  
2. [codeforces_DIV2.214_C](https://xytong.github.io/Capacity/2018/05/26/DP_Problem_Practice.html)  
3. [Polycarp_and_Div3](https://xytong.github.io/Capacity/2018/07/13/Summery_CF_Contest_DIV3_R496.html)  
4. [XOR-pyramid](http://codeforces.com/contest/984/problem/D)  

```py  
n = int(input())
a = [int(x) for x in input().split()]
c = int(input())
b = [[int(x) for x in input().split()] for i in range(0,c)]
f = [[0 for j in range(0,n-i)]for i in range(0,n)]
for i in range(0,n):
    f[0][i] = a[i]

for i in range(1,n):
    for j in range(0,n-i):
        f[i][j] = f[i-1][j] ^ f[i-1][j+1]

for i in range(1,n):
    for j in range(0,n-i):
        f[i][j] = max(max(f[i][j],f[i-1][j]),f[i-1][j+1])
for i in range(0,c):
    print (f[b[i][1]-b[i][0]][b[i][0]-1])
```  

5. [Dima_and_Salad](http://codeforces.com/contest/366/problem/C)  

```py  
[n,k] = [int(x) for x in input().split()]
a = [int(x) for x in input().split()]
b = [int(x) for x in input().split()]
b.insert(0,0)
a.insert(0,0)
s = sum(b) * k
f = [[0 for i in range(0,4*s+1)] for j in range(0,n+1)]
for i in range(0,n+1):
    a[i] = a[i] - (k * b[i])
for i in range(1,n+1):
    for j in range(s,3*s+1):
        f[i][j] = f[i-1][j]
        if j-a[i] == 2*s or f[i-1][j-a[i]] > 0:
            f[i][j] = max(f[i][j],f[i-1][j-a[i]]+b[i])
if f[n][2*s]:
    print(f[n][2*s] * k)
else:
    print(-1)
```  
5. [Three_displays](http://codeforces.com/contest/987/problem/C)  
```py  
n = int(input())
s = [int(x) for x in input().split()]
c = [int(x) for x in input().split()]
f1 = [0 for x in range(0,3005)]
f = [[99999999999 for x in range(0,3005)] for i in range(1,4)]
f.insert(0,f1)
for i in range(0,n):
    f[1][i] = c[i]
for x in range(2,4):
    for i in range(x-1,n):
        for j in range(0,i):
            if s[j] < s[i] and f[x-1][j] != 99999999999:
                f[x][i] = min(f[x-1][j]+c[i], f[x][i])
for i in range(1,n):
    f[3][i] = min(f[3][i-1],f[3][i])
if f[x][i] != 99999999999:
    print(f[x][i])
else:
    print(-1)
```  


