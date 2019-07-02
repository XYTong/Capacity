---
layout: post
title: PVL_1
---
```py
#_*_coding:utf-8_*_
import os
import sys
import numpy as np
mat0 = np.matrix([-1,1,1,1,-1,\
1,-1,-1,-1,1,\
1,-1,-1,-1,1,\
1,-1,-1,-1,1,\
1,-1,-1,-1,1,\
-1,1,1,1,-1])
mat1 = np.matrix([-1,1,1,-1,-1,\
-1,-1,1,-1,-1,\
-1,-1,1,-1,-1,\
-1,-1,1,-1,-1,\
-1,-1,1,-1,-1,\
-1,-1,1,-1,-1])
mat2 = np.matrix([1,1,1,-1,-1,\
-1,-1,-1,1,-1,\
-1,-1,-1,1,-1,\
-1,1,1,-1,-1,\
-1,1,-1,-1,-1,\
-1,1,1,1,1])
mat0t = mat0.getT()
mat0p = mat0t.dot(mat0)
mat1t = mat1.getT()
mat1p = mat1t.dot(mat1)
mat2t = mat2.getT()
mat2p = mat2t.dot(mat2)
print ("===============matrix 0====================")
print(mat0p)
print ("===============matrix 1====================")
print(mat1p)
print ("===============matrix 2====================")
print(mat2p)
matw = mat0p+mat1p+mat2p
print ("===============matrix sum====================")
print (matw)
testa0 = np.matrix([-1,1,1,1,-1,\
1,-1,-1,-1,1,\
1,-1,-1,-1,1,\
-1,-1,-1,-1,-1,\
-1,-1,-1,-1,-1,\
-1,-1,-1,-1,-1])
mata0 = matw.dot(testa0.getT())
print ("=========== raw mata0 ==============")
print (mata0)
for ii in range(mata0.size):
    if mata0[ii] > 0:
        mata0[ii] = 1
    else:
        mata0[ii] = -1
print ("============= After testa0 =================")
print(mata0)
```