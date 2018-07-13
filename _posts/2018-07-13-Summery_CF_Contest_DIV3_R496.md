---
layout: post
title: 我,Codeforce, DIV3_R496, summary
---
## {{ page.title }}
+ **这次比赛，本来能做四道，结果D题DP问题太不熟练，前面三题耽误了大量时间，反省** 

以下是这次比赛的总结: 

+ [A.Tanya and Stairways](http://codeforces.com/contest/1005/problem/A) 

作为DIV3的开题来说，实则是非常可口的一道开胃菜了 o(*￣▽￣*)ブ 直接for循环嵌套一个if判断语句 
实现。本题没有很高深的算法思想，just do it！

```py
n = int(input())
a = [int(x) for x in input().split()]
a.append(-1)
b = []
c = 0
for i in range(0,n):
    if a[i+1] <= a[i]:
        c = c + 1
        b.append(a[i])
print(c)
for e in b:
    print(e,end=' ')
```

+ [B. Delete from the Left](http://codeforces.com/contest/1005/problem/B) 

此题大概意思，即给两个string，可操作空间为remove掉最左边的字母，可以无限次，问最少几步操作能达 
到两个string相等。 因只能从左边删除，最后保留的字符必须相等，所以应该从右往左循环最好，即逆输出 
两个字符串 `a = a[::-1]` `b = b[::-1]`，然后以最小长度的字符串 `l = min(na,nb)` 为range建立 
for循环(多出来的 `d = abs(na-nb)` 为必定要remove的长度，最后循环完毕再加上即可) 
以下是*python*语言实现: 

```py
a = str(input())
b = str(input())
a = a[::-1]
b = b[::-1]
na = len(a)
nb = len(b)
d = abs(na-nb)
l = min(na,nb)
k = 0
for i in range(0,l):
    if a[i] != b[i]:
        k =  (l - i)*2
        break
print(d+k)
``` 

+ [C. Summarize to the Power of Two](http://codeforces.com/contest/1005/problem/C) 

题目大意:一个数组里对于任意一个元素，总能找到至少另外一个组里元素相加为2的幂，则此Sequence称之 
为*go♂d* 。给出一个数组，求需要最少操作量的remove能使其变为*go♂d* 。
思路: 鉴于 *n <= 120000, a[i] <= 10^9* ，所以不能高于 **Onlogn** 的复杂度，鄙人认为最好的解 
法应该先排序 `a = sorted(a)` (排序不影响*go♂d*)，在*n*循环下实施 **binary search** ，对于任意 
a里面的元素，其需要的互补元素(使之相加能达到2^k),即建立一个 **2^k** 数组: 
```py
for i in range(1,31):
    p2.append(2**i)
```
然后求出每一个互补元素 `d = 2**k -a[i]` 再通过 `f = bisect.bisect(a,d)` 判断 `a[f-1] == d`  
的存在， 如果为真，则 `c = c + 1` 并 `break` 跳出k循环。特别地，如果 *bisect* 得出的值是其本身 `if i == f-1` 
则执行 `if a[f-2] == d` ，结果为真，则计数 `c = c + 1`。完整版代码如下: 
```py
import bisect
n = int(input())
a = [int(x) for x in input().split()]
a = sorted(a)
p2 = []
for i in range(1,31):
    p2.append(2**i)
c = 0
if n == 1:
    print(1)
else:
    for i in range(0,n):
        flag = 0
        for j in p2:
            if j > a[i]:
                d = j -a[i]
                f = bisect.bisect(a,d)
                if d != a[i]:
                    if a[f-1] == d:
                        flag = 100
                        break
                else:
                    if i != f-1:
                        if a[f-1] == d:
                            flag = 100
                            break
                    else:
                        if a[f-2] == d:
                            flag = 100
                            break

        if flag == 0:
            c = c + 1
    print(c)
``` 
 
+ [D. Polycarp and Div 3](http://codeforces.com/contest/1005/problem/D) 
> *Print the maximum number of numbers divisible by 3 that Polycarp can get by making vertical cuts in the given number s.* 
思路:**最最最最**简单的dp问题，不要怂，直接写就是了！ 
```py 
a = str(input())
a = 'x' + a
n = len(a)
f = [0 for i in range(0,10**6)]
k = 0
for i in range(1,n):
    if int(a[i])%3 == 0:
        f[i] = f[i-1] + 1
        #if i == 4:
            #print(a[i],f[i])
        k = i
    else:
        for j in range(i-1,k,-1):
            if int(a[j:i+1])%3 == 0:
                f[i] = f[k] + 1
                k = i
        else:
            f[i] = f[k]
maxf = 0
for i in range(0,n):
    maxf = max(maxf,f[i])
print(maxf)
```



{{ page.date | date_to_string }}
