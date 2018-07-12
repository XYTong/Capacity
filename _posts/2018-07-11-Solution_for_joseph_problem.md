---
layout: post
title: 3 typical Solutions for Joseph-Problem 
---
## {{ page.title }}
**这是非常出名且典型的一个问题:**
 
一共n个人（0...n-1)围成一圈，从0开始计数，每轮到第m个人，这个人就会屎，之后循环继续，直到所有人都屎完（剩最后一个人自动屎）。 
 
下面给出三种解♂法:

+ **时间复杂度O(n),空间复杂度O(1)** 

首先射*f(n)*为有*n*个人时最后一个屎的人的编号，则有如下关♂系式: 
`f(n) = (f(n-1) + m) % 5` 
稍有算法常识的人就能看出，第一轮屎亡后，第m-1个人屎掉，则开始n-1人的约瑟夫游♂戏，只不 
过整体人的loop圈往时间流逝方向旋转了m个位移，即与初始n-1约瑟夫 
状态函数f+m相等，实现转圈loop则用膜除m来实现。 

下面是*python*语言实现: 

```py
def joseph(n,m):
    f = 0
    for i in range(2,n+1):
        f = (f + m) % i
    return (f)
```

+ **时间复杂度Olog(n),空间复杂度Olog(n)** 

>*To iterate is human,to recurse divine.*  
  
考虑一下，把每次循环体变成在一圈约瑟夫游♂戏中最后一个屎亡的状态。此时，已经有 *m(n//m)* 
个人都已经报完数，并且屎了 (*n//m*) 个人。即问题从*n*降低到 *n-n//m* ，根据 *n-n//m* 
时候的答案*s*算出*n*时候的答案*sn*。这个有 **两种** 情况, 如果*s*在最后一个屎亡的人后 
面，即 *s < n%m* , 那么 `s2 = s-n%m+n` ， 否则 `s2 = s-n%m+(s-n%m)//(m-1)` 。 
**特别地**，如果*n < m* , 即报数完一轮还没有一个人屎, 则问题的规模无法降低到 *n-n//m* 
所以此方法不适用, 需要再借助前文第一种方法。 下面是 *python* 语言的实现: 

```py

def joseph(n,m):
    if n == 1:
        return (0)
    if n < m:
        return ((joseph(n-1, m) + m) % n)
    x = joseph(n-n//m, m) - n%m
    if x < 0:
        return (x+n)
    return (x+x//(m-1))                 
                                
``` 

+ **时间复杂度Olog(n),空间复杂度O(1)** 

>*Explicit is better than implicit.*  
  
我们换种思路，不妨把整个报数循环展开, 用第几次报数来表示。第*k*个屎的人即使第 *km+m-1* 
次报数滴人(亦是从0开始计数), 设第p个报数的人x, 则有 `p = m*a+b (0 <= b < m)`。且经过 
前p次报数，一共屎了 *p//m = a* ，总共loop还剩下 *n-a* 人。如果x本次没有屎，那下次报数 
是经过圈子其他人报数之后，即 `q = p+n-a = n+(m-1)*a+b` 。已知 *b < m-1* ，易得结果 
`p = q-(n-a) = q-n+floor((q-n)/(m-1))` 
所以我们要求第 *k* 个屎的人， 是第 *km-1* 次报数后shi的，由此往前逆推，不断重复这一过 
程，直到他是第 *k* 次报数的人，则 *k* 即是其编号。以下是 *python* 语言实现: 

```py

def joseph(n,m,k):
    k = k*m+m-1
    while k >= n:
        k = k-n+(k-n)//(m-1)
    return (k)                
                                
```
参考: 
+ [maskray](http://maskray.me/blog/2013-08-27-josephus-problem-two-log-n-solutions) 
+ [Josephus for large n](http://stackoverflow.com/questions/4845260/josephus-for-large-n-facebook-hacker-cup)

{{ page.date | date_to_string }}