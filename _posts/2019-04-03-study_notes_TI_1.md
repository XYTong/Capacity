---
layout: post
title: ich,Theoritische Informatik, NOTES
---
# Part I 
 
## Größenordnungen 

**Definition 2.2** 

$ Durchschnittliche Laufzeit = \frac{\sum_{x Eingabe}Laufzeit(x)}{#Eingaben}$ 

**Definition 3.1**  

$ O(g) = \lbrace f:\textbf{IN} \rightarrow  \mathbb{R}_{0}^{+} \rvert \exists c>0,\exists n_0,\forall n \geq n_0 : f(n) \leq c \cdot g(n) \rbrace $ 
$Seien f, g: \textbf{IN} \rightarrow \mathbb{R}_{0}^{+} Funktionen. Dann bedeutet:$ 
 
$1.f = O(g), wenn \exists c>0, \exists n_0, \forall n \geq n_0: f(n) \leq c \cdot g(n); \\
"f wächst nicht schneller als g"$ 
$2.f = \Omega (g), wenn g = O(f) gilt; \\
"f wächst mindestens so schnell wie g"$ 
$3.f = \Theta (g), wenn f = O(g) und g =O(f) gilt; \\
"f und g sind von gleicher Größenordnung"$ 
$4.f = o(g), wenn f(n)/g(n) Nullfolge ist; \\
f wächst langsamer als g$ 
$5.f = /omega(g),wenn g = o(f) gilt; \\
"f wächst schneller als g"$ 

**Definition 3.4** $Eine Funktion f:\textbf{IN} \rightarrow \mathbb{R}_{0}^{+}$ 
+ *heißt polynomiell beschränkt, falls es ein Polynom p gibt mit f = O(p).* 
+ $wächst exponentiell, wenn es ein \varepsilon > 0 gibt mit f = \Omega (2^{n^{\varepsilon}}). \lbrak f wächst mindestens so schnell wie c /cdot 2^{n^{\varepsilon}} für eine Konstante c>0$ 