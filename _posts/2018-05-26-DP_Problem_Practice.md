---
layout: post
title: 我，DP问题, 学习一个, Div2.214_C
---
## {{ page.title }}
学习一个，im angry！
借鉴了@simonmysun的代码，居然他自己都看不懂了
```py
[n,k] = [int(x) for x in input().split()]
a = [int(x) for x in input().split()]
b = [int(x) for x in input().split()]
b.insert(0,0)                                                #加0，让数组和参数i同步
a.insert(0,0)
s = sum(b) * k                                               #求s，差距j最大的情况
f = [[0 for i in range(0,4*s+1)] for j in range(0,n+1)]      #考虑s正负+2倍缓冲
for i in range(0,n+1):
    a[i] = a[i] - (k * b[i])                                 #计算出单个的i的离需要达到指定ratio的差距
for i in range(1,n+1):                                       #用差距来做状态转移，从前i个里找出加起来差距是j的若干个b元素
    for j in range(s,3*s+1):                                 #第i个放不放，取决于能不能使得 sum（bi）最大
        f[i][j] = f[i-1][j]                                  #即使通过放或不放（0,1），选定了一种状态，剩下一种状态也可能在另外一个状态方程里出现
        if j-a[i] == 2*s or f[i-1][j-a[i]] > 0:              #只要其满足条件，这样相交交互的类似于DNA双螺旋结构（雾）的关系保证了涵盖掉所有的可能，却又资源最大化
            f[i][j] = max(f[i][j],f[i-1][j-a[i]]+b[i])       #不过还是需要鄙人找个时间来好好推一推关系式
if f[n][2*s]:
    print(f[n][2*s] * k)                                     #间接sum（a）最大
else:
    print(-1)                                                #潇洒收尾
```

{{ page.date | date_to_string }}