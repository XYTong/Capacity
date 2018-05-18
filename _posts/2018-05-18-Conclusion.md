---
layout: post
title: 我，比赛, 总结, Div484
---
## {{ page.title }}
Problem A
this is a very simple and typical problem about how to deal with string,  
but i haven't considered about the initial and end problem.  
so yeal, in initial or end point if '00' exists， it should output also  
'No', so i can just add '0' both in end and initial of the string and at  
the same time has no influence on others of the string.  
Also, we avoid the situation that len(a) == 1 

```py
def F(a):
    a = '0' + a + '0'
    if len(a) == 1:                   #this is no need
        print('Yes')
        return

    else:    
        if a.find('11') == -1:
                
            if a.find('000') == -1:
                print('Yes')
                return
            
        print('No')
        return
n = input()
a = str(input())
F(a)                                  #   
```

{{ page.date | date_to_string }}