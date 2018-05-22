---
layout: post
title: 我，python, 优化2, EDU44_C
---
## {{ page.title }}
学习一个，im angry!  
这次的edu比赛，本以为是送分题，结果又只做了一道。。。果然还是做div3才能提高自信  
不过呢，也能借此学到很多东西，新的语法，多多练习，熟练，也当是一种提高吧  
以后每次做题前，都应该花10分钟构思一下整个program的结构，提前想好，也不至于操作  
的时候一阵慌乱。开局先把input，变量都声明，不要写太多废语句，多打print来检查程序  
运行状态

```py
# 老版，错的
[n,k,l] = [int(x) for x in input().split()]
a = [int(x) for x in input().split()]          #input写的很霸气
import bisect
s = 0                                          #最终要求的，先写出来
a = sorted(a)                                  #排序，很多题都要用到
b = bisect.bisect_right(a,a[0]+l)              #这个检索语句还是得好好掌握，用熟了很好用
c = len(a) - 1                                 #干嘛呢？没必要
if b > n:                                      #完全可以把 > 和 = 写成一种情况
    a1 = a[:b]                                 #排序了之后，从这个里面扣的依次就是最小满足的情况（暂时
    for i in range(b-1,b-n-1,-1):              #这个循环是没有错滴
        k = a1.pop()                           #扣
        if c >= b:                             #判断b后面的组有没有扣完，这里写错了，应该先整个av出来，算出b后面可用（扣）的个数
            p = a.pop()                        #扣
            c = c - 1                          #扣了-1，这里写的还行，思维是有了
        else:
            p = a1.pop()   
        s = s + min(k,p)                       #其实最后根本不用比大小，扣完事了，扣得正确，扣下来的全是最后要找的
    print(s)
elif b == n:
    for i in range(0,n):
        s = s + a[i]
    print(s)
else:
    print(0)                                   #最好写的部分，但是也是要判断滴  
```

{{ page.date | date_to_string }}

## {{ page.title }}
学习一个，im angry！

```py
#优化过的完美程序
[n,k,l] = [int(x) for x in input().split()]
a = [int(x) for x in input().split()]
import bisect
s = 0
a = sorted(a)
b = bisect.bisect_right(a,a[0]+l)
a1 = a[:b]
tot = n * k
av = tot - b
if b >= n:
    for i in range(b-1,b-n-1,-1):
        m = a1.pop()
        for j in range(0,k-1):
            if av > 0:
                av = av - 1
            else:
                m = a1.pop()
        s = s + m
    print(s)
else:
    print(0)                                 #   
```

{{ page.date | date_to_string }}