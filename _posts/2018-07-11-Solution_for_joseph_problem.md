---
layout: post
title: 4 typical Solutions for Joseph-Problem 
---
## {{ page.title }}
**这是非常出名且典型的一个问题:**

+ **Background** 
In computer science and mathematics, the **Josephus problem** (or **Josephus permutation**) is 
a theoretical problem related to a certain counting-out game. 
People are standing in a circle waiting to be executed. Counting begins at a specified point in 
the circle and proceeds around the circle in a specified direction. After a specified number of 
people are skipped, the next person is executed. The procedure is repeated with the remaining 
people, starting with the next person, going in the same direction and skipping the same number 
of people, until only one person remains, and is freed. 
The problem, given the number of people, starting point, direction, and number to be skipped, is 
to choose the position in the initial circle to avoid execution. 

> *The problem is named after Flavius Josephus, a Jewish historian living in the 1st century. According*
*to Josephus' account of the siege of Yodfat, he and his 40 soldiers were trapped in a cave by Roman*
*soldiers. They chose suicide over capture, and settled on a serial method of committing suicide by*
*drawing lots. Josephus states that by luck or possibly by the hand of God, he and another man remained* 
*until the end and surrendered to the Romans rather than killing themselves.*
 
下面给出四种解♂法:
 
+ **时间复杂度O(n*m),空间复杂度O(1)** 

比较简单的做法是用循环单链表模拟整个过程，时间复杂度是O(n*m)。
如果只是想求得最后剩下的人，则可以用数学推导的方式得出公式。且 
先看看模拟过程的解法。 

下面是*python*语言实现: 

```py
class Node(object):
	def __init__(self, value):
		self.value = value 
		self.next = None

def create_linkList(n):
	head = Node(1)
	pre = head
	for i in range(2, n+1):
		newNode = Node(i)
		pre.next= newNode
		pre = newNode
	pre.next = head
	return head

n = 5 #总的个数
m = 2 #数的数目
if m == 1: #如果是1的话，特殊处理，直接输出
	print (n)  
else:
	head = create_linkList(n)
	pre = None
	cur = head
	while cur.next != cur: #终止条件是节点的下一个节点指向本身
		for i in range(m-1):
			pre =  cur
			cur = cur.next
		print (cur.value)
		pre.next = cur.next
		cur.next = None
		cur = pre.next
	print (cur.value)
``` 


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
+ [WiKi](https://zh.wikipedia.org/wiki/%E7%BA%A6%E7%91%9F%E5%A4%AB%E6%96%AF%E9%97%AE%E9%A2%98)

{{ page.date | date_to_string }}