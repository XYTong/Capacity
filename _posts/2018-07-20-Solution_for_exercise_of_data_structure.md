---
layout: post
title: me,data structure, exercise, solution
---
## {{ Part.1 }}
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
following是*c++*语言实现: 

```cpp
#include <iostream>
using namespace std;
int main() {
    float in_cm;
    float in_inches;
    const float EPSINON = 0.00001;
    cin >> in_cm >> in_inches;
    in_inches = in_inches * 2.54;
    if (- EPSINON<=in_cm-in_inches && in_cm-in_inches <= EPSINON) {
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
[EmojiCodeInstall](https://github.com/emojicode/emojicode) 

+ **Given *n* integers, each of them appears twice except for one, which appears exactly once. Find that single one.** 

We can use sorting to finish it with a time complexity O(nlogn). **But** there is a more NB way which use **bitwise** operators 
for a solution that is O(n) time and O(1) space. As a common is the feature `x^y^x=y^x^x=y`. So in this case we do `^` for all 
the elements of the set, finally got the answer which only appears once. 
the following is the realisierung of *c++* : 

```cpp
#include <stdio.h>
#include <iostream>
using namespace std;
int n, i;
int a[100];
int findsigular (int a[], int len) {
    int res = 0;
    int j = 0;
    for (j=0;j<len;j++) {
        res = res ^ a[j];
    }
    return res;
}
int main() {
    cin >> n;
    for (i=0;i<n;i++) {
            cin >> a[i];
    }
    cout << findsigular(a,n);
}
``` 

   + advanced: **Given *n* integers, each of them appears three times except for one, which appears exactly once. Find that single one.** 
   > ‘ones’ and ‘twos’ are initialized as 0. For every new element in array, find out the common set bits in the new element and previous value of ‘ones’. These common set bits are actually the bits that should be added to ‘twos’. So do bitwise OR of the common set bits with ‘twos’. ‘twos’ also gets some extra bits that appear third time. These extra bits are removed later.
   Update ‘ones’ by doing XOR of new element with previous value of ‘ones’. There may be some bits which appear 3rd time. These extra bits are also removed later. 
   Both ‘ones’ and ‘twos’ contain those extra bits which appear 3rd time. Remove these extra bits by finding out common set bits in ‘ones’ and ‘twos’. 
   the [following](https://www.geeksforgeeks.org/find-the-element-that-appears-once/) is the realisierung of *c++* : 

   ```cpp 
    int getSingle(int arr[], int n)
    {
        int ones = 0, twos = 0 ;
    
        int common_bit_mask;
    
        // Let us take the example of {3, 3, 2, 3} to understand this
        for( int i=0; i< n; i++ )
        {
            /* The expression "one & arr[i]" gives the bits that are
            there in both 'ones' and new element from arr[].  We
            add these bits to 'twos' using bitwise OR
    
            Value of 'twos' will be set as 0, 3, 3 and 1 after 1st,
            2nd, 3rd and 4th iterations respectively */
            twos  = twos | (ones & arr[i]);
    
    
            /* XOR the new bits with previous 'ones' to get all bits
            appearing odd number of times
    
            Value of 'ones' will be set as 3, 0, 2 and 3 after 1st,
            2nd, 3rd and 4th iterations respectively */
            ones  = ones ^ arr[i];
    
    
            /* The common bits are those bits which appear third time
            So these bits should not be there in both 'ones' and 'twos'.
            common_bit_mask contains all these bits as 0, so that the bits can 
            be removed from 'ones' and 'twos'   
    
            Value of 'common_bit_mask' will be set as 00, 00, 01 and 10
            after 1st, 2nd, 3rd and 4th iterations respectively */
            common_bit_mask = ~(ones & twos);
    
    
            /* Remove common bits (the bits that appear third time) from 'ones'
                
            Value of 'ones' will be set as 3, 0, 0 and 2 after 1st,
            2nd, 3rd and 4th iterations respectively */
            ones &= common_bit_mask;
    
    
            /* Remove common bits (the bits that appear third time) from 'twos'
    
            Value of 'twos' will be set as 0, 3, 1 and 0 after 1st,
            2nd, 3rd and 4th itearations respectively */
            twos &= common_bit_mask;
    
            // uncomment this code to see intermediate values
            //printf (" %d %d n", ones, twos);
        }
    
        return ones;
    }
   ``` 
+ **Given a string of a heximal number(might not be an integer), print it in decimal form.** 

according to [ASCII](https://zh.wikipedia.org/wiki/ASCII) : 
**Printable characters** 

Binary|Oct|Dec|Hex|Glyph
---|:--:|:--:|:--:|---:
011 0000|060|48|30|0
011 0001|061|49|31|1
011 0010|062|50|32|2
011 0011|063|51|33|3
011 0100|064|52|34|4
011 0101|065|53|35|5
011 0110|066|54|36|6
011 0111|067|55|37|7
011 1000|070|56|38|8
011 1001|071|57|39|9
100 0001|101|65|41|A
100 0010|102|66|42|B
100 0011|103|67|43|C
100 0100|104|68|44|D
100 0101|105|69|45|E
100 0110|106|70|46|F
100 0111|107|71|47|G
...|...|...|...|...

so here is the code in *c++* : 

```cpp
#include <iostream>
#include <string>
#include <math.h>
using namespace std;
int i, sum;
int main() {
    string hexd;
    cin >> hexd;
    int n = hexd.length();
    sum = 0;
    for (i=n-1;i>=0;i--) {
        if (hexd[i]>='0' && hexd[i] <= '9') {
            sum+=(hexd[i]-48)*pow(16,n-i-1);
        }
        else if (hexd[i]>='A' && hexd[i]<='F') {
            sum+=(hexd[i]-55)*pow(16,n-i-1);
        }
    }
    cout << sum;
}
``` 
specially, if it might not be an integer, we just need do a tiny change. 
find the index `.` and... 

+ **Write a programm of encryption and decryption of Caesar ciphering.** 

```cpp
#include <iostream>
#include <cmath>
#include <string.h>
using namespace std;
int main() {
    char a[105],ch;
    int k, i, j;
    cout << "please enter Key(k):";
    cin >> k;
    cout << "please select encryption(0) or decryption(1): ";
    cin >> ch;
    if (ch=='0') {
        cout << "please enter Plaintext string:";
        cin >> a;
        for (i=0; i<strlen(a); i++) {
            if (a[i]>='a' && a[i]<='z') {
                cout << (char)((a[i]-'a'+k)%26 + 'a');
            }
            else if (a[i]>='A' && a[i]<='Z') {
                cout << (char)((a[i]-'A'+k)%26 + 'A');
            }
        }
    }
    else if (ch=='1') {
        cout << "please enter cyphertext string: ";
        cin >> a;
        for (j=0;j<strlen(a);j++) {
            if (a[j]>='a' && a[j]<='z') {
                cout << (char)((a[j]-'a'+26-k)%26 + 'a');
            }
            else if (a[j]>='A' && a[j]<='Z') {
                cout << (char)((a[j]-'A'+26-k)%26+'A');
            }
        }
    }
}
``` 

+ Name algorithms of string searching and compare their advantages and disadvantages. 

Algorithm|Preprocessing time|Matching time|space
---|:--:|:--:|---:
Naïve string-search algorithm|none|Θ(nm)|none
Rabin–Karp algorithm|Θ(m)|average Θ(n + m)|O(1)
Knuth–Morris–Pratt algorithm|Θ(m)|Θ(n)|Θ(m)
Boyer–Moore string-search algorithm|Θ(m + k)|best Ω(n/m)|Θ(k)
Bitap algorithm|Θ(m + k)|O(mn)| 
Two-way string-matching algorithm|Θ(m)|O(n+m)|O(1)

{{ page.date | date_to_string }}
