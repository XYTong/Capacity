---
layout: post
title: me,data structure, exercise, solution
---
## {{ page.title }}
**thanks for the help by [simonmysun](https://github.com/simonmysun) for the Collectionin in learning and practicing of data structure** 
 
--- 
the following comes the solutions and summary of [data structure](https://xytong.github.io/Capacity/2018/07/20/Learning_data_structure.html): 

+ **Given two 32-bit signed integers *a* and *b*, print how many bits changes when turning *a* to *b*.**

in a word, we just need to caculate how many different bits between *a* and *b*. 
first of all, we can use `a^b`, so that the *1* in result represent the different two bits. 
second, use hamming weight to caculate the number of *1* which is the answer we want. 
here is the programming by *python*: 

```py
class Solution:
    def deor(self,a,b):
        a ^= b
        if a > 0:
            return self.count(a)
        else:
            c = abs(a - 1)
            return 32 - self.count(c)            #we must consider if a < 0
    
    def count(self,n):
        count = 0
        while n != 0:
            n = n & (n - 1)
            count += 1
        return count
``` 
otherwise there is a more NB way to get Hamming Weight [here](https://en.wikipedia.org/wiki/Hamming_weight): 
 
```cpp
//types and constants used in the functions below

typedef unsigned __int64 uint64;  //assume this gives 64-bits
const uint64 m1 = 0x5555555555555555; //binary: 0101...
const uint64 m2 = 0x3333333333333333; //binary: 00110011..
const uint64 m4 = 0x0f0f0f0f0f0f0f0f; //binary:  4 zeros,  4 ones ...
const uint64 m8 = 0x00ff00ff00ff00ff; //binary:  8 zeros,  8 ones ...
const uint64 m16 = 0x0000ffff0000ffff; //binary: 16 zeros, 16 ones ...
const uint64 m32 = 0x00000000ffffffff; //binary: 32 zeros, 32 ones ...
const uint64 hff = 0xffffffffffffffff; //binary: all ones
const uint64 h01 = 0x0101010101010101; //the sum of 256 to the power of 0,1,2,3...

//This is a naive implementation, shown for comparison,
//and to help in understanding the better functions.
//It uses 24 arithmetic operations (shift, add, and).
int popcount_1(uint64 x) {
    x = (x & m1 ) + ((x >>  1) & m1 ); //put count of each  2 bits into those  2 bits 
    x = (x & m2 ) + ((x >>  2) & m2 ); //put count of each  4 bits into those  4 bits 
    x = (x & m4 ) + ((x >>  4) & m4 ); //put count of each  8 bits into those  8 bits 
    x = (x & m8 ) + ((x >>  8) & m8 ); //put count of each 16 bits into those 16 bits 
    x = (x & m16) + ((x >> 16) & m16); //put count of each 32 bits into those 32 bits 
    x = (x & m32) + ((x >> 32) & m32); //put count of each 64 bits into those 64 bits 
    return x;
}

//This uses fewer arithmetic operations than any other known  
//implementation on machines with slow multiplication.
//It uses 17 arithmetic operations.
int popcount_2(uint64 x) {
    x -= (x >> 1) & m1;             //put count of each 2 bits into those 2 bits
    x = (x & m2) + ((x >> 2) & m2); //put count of each 4 bits into those 4 bits 
    x = (x + (x >> 4)) & m4;        //put count of each 8 bits into those 8 bits 
    x += x >>  8;  //put count of each 16 bits into their lowest 8 bits
    x += x >> 16;  //put count of each 32 bits into their lowest 8 bits
    x += x >> 32;  //put count of each 64 bits into their lowest 8 bits
    return x &0xff;
}

//This uses fewer arithmetic operations than any other known  
//implementation on machines with fast multiplication.
//It uses 12 arithmetic operations, one of which is a multiply.
int popcount_3(uint64 x) {
    x -= (x >> 1) & m1;             //put count of each 2 bits into those 2 bits
    x = (x & m2) + ((x >> 2) & m2); //put count of each 4 bits into those 4 bits 
    x = (x + (x >> 4)) & m4;        //put count of each 8 bits into those 8 bits 
    return (x * h01)>>56;  //returns left 8 bits of x + (x<<8) + (x<<16) + (x<<24) + ... 
}
```

+ **Given a number of height in inches and a number of height in centimeters, tell whether they equal each other.**

it's so **braindead** so that i don't need to explain. 
以下是*c++*语言实现: 

```cpp
#include <iostream>
using namespace std;
int main() {
    float in_cm;
    float in_inches;
    cin >> in_cm >> in_inches;
    in_inches = in_inches * 2.54;
    if (in_cm == in_inches) {
        cout << "YES";
    }
    else {
        cout << "NO";
    }
}
``` 

+ **Explain ASCII code *0,9,10,13* and declare variables of them in charactor literals.** 

Orc|Arvt|Name
---|:--:|---:
0|NUL|Null
9|HT|Horizontal Tab
10|LF|Line Feed
13|CR|Carriage Return

 
+ **How to print an emoji?** 
So the clang document says (emphasis mine): 

> *This feature allows identifiers to contain certain Unicode characters, as specified by the active language standard;* 
[Emoji List](https://en.wikipedia.org/wiki/Hamming_weight)


{{ page.date | date_to_string }}
