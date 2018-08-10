---
layout: post
title: me,data structure, exercise, solution
---
# Part I 
 

**thanks for the help by [simonmysun](https://github.com/simonmysun) for the Collectionin in learning and practicing of data structure** 
 
--- 
the following comes the solutions and summary of [data structure](https://xytong.github.io/Capacity/2018/07/20/Learning_data_structure.html): 

## Data types 

### Primitive types 

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
--- 

### Composite types or non-primitive type 

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

+ **Implement a expression evaluator supporting decimal numbers(with or without seperator), + and −.** 

acctually if we wanna figure out like 编译原理 stuff, first step is **lexical analysis**, then **Syntacticanalysis** 
here is the steps:
1. we spilt each of the data, like `3*2.3+2`, to `3`, `*`, `2.3`, `+`, `2` 
2. from **Infix notation** to **RPN**, `3`, `2.3`, `*`, `2`, `+` 
3. use the feature of stack to caculate the result 
and there are some tiny tipps for that: 
1. 符号栈top()优先级大于当前遍历的符号的话，出栈，再入当前当前遍历的符号入栈。 
2. 遇’(‘左括号，符号栈保持不变，并添加’(‘入栈。 
3. 遇’)’右括号，符号栈一直出栈，直到遇到’(‘左括号。

[code](https://blog.csdn.net/what951006/article/details/77892670)(*c++*) : 
```cpp 
#include <iostream>
#include <stack>
#include <algorithm>
#include <vector>
using namespace std;
enum AnalysisType:unsigned char{FLOAT=0x01,OPERATOR=0x02};
struct ItemValue
{
    union ValueUnion
    {
        float fdigit;
        char symbol;
    };
    AnalysisType type;
    ValueUnion value;
};
//简单的int加减乘除
int GetPriority(char symbol)
{
    switch (symbol)
    {
    case '+':
    case '-':
        return 0;
    case '*':
    case '/':
        return 1;
    case '(':
    case ')':
        return 2;
    }
    return -1;
}

bool IsOperator(char symbol)
{
    switch (symbol)
    {
        case '+':
        case '-':
        case '*':
        case '/':
        case '(':
        case ')':
        return true;
    }
    return false;
}
//转成vector存
void wordsAnalysis(char*pIn, vector<ItemValue>&vec)
{
    int nCount = strlen(pIn);
    int nIndex = 0;
    while (nIndex<nCount)
    {
        ItemValue item = { FLOAT,0};
//处理操作符
        if (IsOperator(pIn[nIndex]))//如果是操作符
        {
            item.type = OPERATOR;
            item.value.symbol = pIn[nIndex];
            vec.push_back(item);
        }
//处理数字
        int nTemp = nIndex;
        char nBuffer[20] = {0};//20位
        while (isdigit(pIn[nTemp]) || '.'==pIn[nTemp])
        {   
            nBuffer[nTemp - nIndex]=pIn[nTemp];
            ++nTemp;
        }
        if (nTemp != nIndex)
        {
            item.value.fdigit = atof(nBuffer);
            vec.push_back(item);
        }
//////////
        if (nTemp != nIndex)
            nIndex += strlen(nBuffer);
        else
            ++nIndex;
    }
}
//中缀转后缀
void midToLast(vector<ItemValue> & vecIn, vector<ItemValue> & vecOut)
{
    ItemValue item{ OPERATOR ,0.0f };
    stack<char> stack_symbol;
    for_each(std::begin(vecIn), std::end(vecIn), [&](ItemValue &it) {
        if (FLOAT == it.type )
        {
            vecOut.push_back(it);
        }
        else if (OPERATOR == it.type)
        {
            if (')' == it.value.symbol)
            {
                while (!stack_symbol.empty())
                {
                    if (stack_symbol.top() == '(')
                    {
                        stack_symbol.pop();
                        return;
                    }
                    item.value.symbol = stack_symbol.top();
                    stack_symbol.pop();
                    vecOut.push_back(item);
                }
            }
            if (!stack_symbol.empty())
            {
                if (GetPriority(stack_symbol.top()) - GetPriority(it.value.symbol) >= 0 && stack_symbol.top()!='(')
                {
                    item.value.symbol = stack_symbol.top();
                    stack_symbol.pop();
                    vecOut.push_back(item);
                }
            }
            if(')' != it.value.symbol)
                stack_symbol.push(it.value.symbol);
        }
    });
    //把栈里的操作符提出来
    while (!stack_symbol.empty())
    {
        item.value.symbol = stack_symbol.top();
        stack_symbol.pop();
        vecOut.push_back(item);
    }
}
//计算
float Calculate(vector<ItemValue>& vec)
{
    float fResult=0.0f;
    stack<ItemValue> stack_value;
    for_each(std::begin(vec), std::end(vec), [&](ItemValue &it) {
        if (FLOAT == it.type)
        {
            stack_value.push(it);
        }
        else if(OPERATOR == it.type)
        {
            ItemValue Value1, Value2 ;
            Value2=stack_value.top();
            stack_value.pop();

            Value1=stack_value.top();
            stack_value.pop();

            switch (it.value.symbol)
            {
            case '+':
                Value1.value.fdigit += Value2.value.fdigit;
                break;
            case '-':
                Value1.value.fdigit -= Value2.value.fdigit;
                break;
            case '*':
                Value1.value.fdigit *= Value2.value.fdigit;
                break;
            case '/':
                Value1.value.fdigit /= Value2.value.fdigit;
                break;
            }
            Value1.type = FLOAT;
            stack_value.push(Value1);
        }
    });
    fResult = stack_value.top().value.fdigit;
    return fResult;
}

int main()
{
    char buffer[64] = {0};
    vector<ItemValue> vecIn,vecOut;
    cout << "请输入表达式：";
    cin >> buffer;
    wordsAnalysis(buffer, vecIn);//拆分数据
    midToLast(vecIn,vecOut);//转到后缀表达式，vecOut内
    cout << "中缀到后缀：";
    for_each(std::begin(vecOut), std::end(vecOut), [&](ItemValue &it) {
        FLOAT == it.type?       
        cout << it.value.fdigit << "  ":
        cout << (char)it.value.symbol << "  ";
    });
    cout <<endl<<"计算结果：" << Calculate(vecOut)<<endl ;
    return 0;
}
``` 

for the case which only contains Operator `+` and `-` we can write more simple and explicitly instead of using **Stack** 
here is the code: 

```cpp 
#include <string>
#include <iostream>
using namespace std;
float calculate(float Operand1, float Operand2, char Operator) {
    float res = 0 ;
    if (Operator == '+') {
        res = Operand1 + Operand2;
    }
    else if (Operator == '-') {
        res = Operand1 - Operand2;
    }
    return res;
}

float EE(const string& str) {
    float Operand1 = 0;
    float Operand2 = 0;
    char Operator = 0;
    for (size_t i=0, size=str.size(); i<size; ++i) {
        const char& ch = str[i];
        if ('0'<=ch && ch<='9') {
            if (Operator == 0) {
                Operand1 = Operand1*10 + ch - '0';
            }
            else {
                Operand2 = Operand2*10 + ch - '0';
            }
        }
        else if (ch=='+' || ch=='-') {
            if (Operator == 0) {
                Operator = ch;
            }
            else {
                Operand1 = calculate(Operand1, Operand2, Operator);
                Operand2 = 0;
                Operator = ch;
            }
        }
    }
    Operand1 = calculate(Operand1, Operand2, Operator);
    return Operand1;
}
int main() {
    string str;
    cin >> str;
    float Res = EE(str);
    cout << str << "=" << Res << endl;
}
``` 


## Basic data structures 

### Linked list 

+ Use arrays to implement linked lists. 

there are various ways to implement a linked list with using arrays. here i wrote tow different ways: 

1. using **Node structure** and **pointer**(Singly Linked List). 
each **Node** contains a data type and a **pointer** to the next Node: 

```cpp 
struct node {
    int data;
    struct node *next;
};
``` 

besides we wil use a function to conected each 2 "adjacent" Nodes. It has tow Parameters: 
array pointer and size of array: 

```cpp
#include <iostream>
#include <string>
#include <stdlib.h>
using namespace std;

struct node {
    int data;
    struct node *next;
};

node * createnode(int val) {
    node * newnode = (node*)malloc(sizeof(node));
    if (newnode == NULL) {
        return NULL;
    } else {
        newnode->data = val;
        newnode->next = NULL;
        return newnode;
    }
}

int main() {
    int arr[100];
    int n;
    cin >> n;
    for (int k = 0; k < n; k++) {
        cin >> arr[k];
    }
    node * head;
    node * tail = NULL;
    for (int i = 0; i < n; i++) {
        if (i == 0) {
            head = createnode(arr[i]);
            head->next = createnode(arr[i]);
            tail = head->next;
        } else {
            node * newnode = createnode(arr[i]);
            tail->next = newnode;
            tail = tail->next;
        }
    }
    node * element = head->next;
    while (element != NULL) {
        cout << element->data << " ";
        element = element->next;
    }
    cout << endl;
}
```
pointer function `node * createnode(int val)` return a new node with a empty pointer to NULL 
in the main func we use loop to create new node meanwhile we keep the head value and tail value to the next
for operation of the linked list we just need head as input. 
for remove: 

```cpp
void DeleteByVal(node *head, int val)
{
    if (head->next == NULL)
    {
        return;
    }

    //find target node and its precursor
    node *cur = head->next, *pre = head;
    while(cur)
    {
        if (cur->data == val)
            break;
        else {
            cur = cur->next;
            pre = pre->next;
        }
    }

    //delete target node
    pre->next = cur->next;
    free(cur);
    head->data--;
}
``` 

for empty the list: 

```cpp 
void Free(node *head)
{
    for (node *temp = head; temp != NULL; temp = head->next) 
    {
        head = head->next;
        free(temp);
    }
}
```

2. using array 


```cpp
#include <iostream>
using namespace std;
struct node {
    int data;
    int next;
};
node A[10];
int main() {
    int arr[10];
    for (int i = 0; i < 10; i++) {
        cin >> arr[i];
        A[i].data = arr[i];
        if (i != 9) {
            A[i].next = A[i+1].data;
        } else {
            A[i].next = A[0].data;
        }
    }
    for (int j = 0; j < 10; j++) {
        cout << A[j].data << " ";
    }
}

``` 

+ **Implement undo/redo functionality(or back/forward navigation in explorer).** 

For some softwares, they generally offer the **Redo** and **Undo** Operations, like Action panel in Paint.NET, or UNDO/REDO in 
*Word* , normally we just press CTRL-Z to implement it. 
to implement the funtionality , directly thinking is, that we put the Command as a class into a Stack, which we can imagine it as 
a class.
abstract the Command or Operation as a class, which can use different Request parameter to initialize the class, in other word **Queue processing for Commands, recording the requests, execute Undo/Redo Operations.**, that's called **Command Pattern**. the 
most advantages its is that, **Separating the call and implement**. 
> The standard is to keep the Command objects in a stack to support multi level undo. In order to support redo, a second stack keeps all the commands you've Undone. So when you pop the undo stack to undo a command, you push the same command you popped into the redo stack. You do the same thing in reverse when you redo a command. You pop the redo stack and push the popped command back into the undo stack. 
here is a **small**  example for implementing of undo/redo functionality: 

first we build a command class `ICoomand` and its two subclass as Operator 1 and 2, here we used virtual function ([see more](https://github.com/simonmysun) about **virtual function**). Then we built a class `AssWeCan` for implementing of stack, whitch 
contains **undo-stack** and **redo-stack** and a function `void RBQ(command)` to store the commands. `class FAQ` contains  
end two outputs which can be called by two subclass of `ICommand`. otherwise, the two pointer functions (PopUndoCommand and 
PopRedoCommand) were used to implement **undo/redo**, return the one which was poped from the top of **stack** and into anonther 
stack. 
for `int main()` function, we use while loop to implement multi commands and multi undo/redo. 
[see more](https://github.com/simonmysun) deep dark fantasy. 

here is the code by 'c++' :

```cpp 
#include <iostream>
#include <stack>
#include <stdio.h>
using namespace std;

class ICommand {
public:
    virtual void Execute() = 0;
};

class AssWeCan {
public:
    stack<ICommand *>undolist;
    stack<ICommand *>redolist;
    void RBQ(ICommand *command) {
        if (command) {
            undolist.push(command);
            command->Execute();
        }
    }
};

class FAQ {
public:
    void deedar() {
        cout << "deep \u2642 dark \u2642 fantasy \u2642." << endl;
    }
    void perform_artist() {
        cout << "do u like \u2642 what \u2642 u \u2642 see." << endl;
    }
};

class DeedarCommand : public ICommand {
private:
    FAQ *_fuck_u;
public:
    DeedarCommand(FAQ *fuck_u) {
        _fuck_u = fuck_u;
    }
    void Execute() {
        _fuck_u->deedar();
    }
};

class PerformCommand : public ICommand {
private:
    FAQ *_fuck_u;
public:
    PerformCommand(FAQ *fuck_u) {
        _fuck_u = fuck_u;
    }
    void Execute() {
        _fuck_u->perform_artist();
    }
};

ICommand * PopUndoCommand(AssWeCan* asswecan) {
    ICommand *pcommand = NULL;
    if (!asswecan->undolist.empty()) {
        pcommand = asswecan->undolist.top();
        asswecan->undolist.pop();
    }
    return pcommand;
}

ICommand * PopRedoCommand(AssWeCan* asswecan) {
    ICommand * pcommand = NULL;
    if (!asswecan->redolist.empty()) {
        pcommand = asswecan->redolist.top();
        asswecan->redolist.pop();
    }
    return pcommand;
}

int main() {
    stack<ICommand *>undolist;
    stack<ICommand *>redolist;
    FAQ* fuck_u = new FAQ;
    ICommand* ddf = new DeedarCommand(fuck_u); 
    ICommand* pa = new PerformCommand(fuck_u);
    AssWeCan* asswecan = new AssWeCan;
    char ch;
    cout << "Enter ur favourite w\u2642rd a)deedar b)perform artist: " << endl;
    cin >> ch;
    while (ch != 'q') {
        if (ch == 'a') asswecan->RBQ(ddf);
        else asswecan->RBQ(pa);
        cout << "Enter ur favourito w\u2642rd a)deedar b)perform aritist (press q to quit): " << endl;
        cin >> ch;
    }
    cout << asswecan->undolist.top() << endl;
    asswecan->undolist.top()->Execute();
    cout << "Press (u) to undo and (r) to redo( (q) for quit): " << endl;
    char ch1;
    cin >> ch1;
    while(ch1 != 'q') {
        if (ch1 == 'u' ) {
            ICommand * pcommand = PopUndoCommand(asswecan);
            cout << asswecan->undolist.top() <<endl;
            asswecan->redolist.push(pcommand);
            asswecan->undolist.top()->Execute();
        }
        else {
            ICommand * pcommand = PopRedoCommand(asswecan);
            asswecan->undolist.push(pcommand);
            asswecan->undolist.top()->Execute();
        }
        cout << "Press (u) to undo and (r) to redo( (q) for quit): " << endl;
        cin >> ch1;
    }

    delete fuck_u;
    delete ddf;
    delete pa;
    delete asswecan;
    return 0;
}
``` 

+ Reverse a given linked list(unless otherwise specified, linked lists refer to sigly linked list of number) 

we can write directly with out doubt: 

```cpp 
node* Reverse (node* head) {
    if (head == NULL || head->next == NULL) return head;
    else {
        node *cur = head->next,
             *pre = NULL,
             *next = NULL;
        while (cur != NULL) {
            next = cur->next;
            cur->next = pre;
            pre = cur;
            cur = next;
        }
        head->next = pre;
        return head;
    }
}
``` 

+ Find *n* th node from the end of a given linked list. 

`cout << tail->data << endl;` 

+ Find the middle node of a given linked list. 

```cpp 
node * element = head->next; 
for (int i = 0; i < n; i++) {
    if (n % 2 != 0) {
        if (i == (n-1)/2) {
            cout << element->data << endl;
            break;
        }
    } else {
        if (i == n/2 - 1) {
            cout << element->data << endl;
            cout << element->next->data << endl;
            break;
        }
    }
    element = element->next;
}
``` 

+ Sort a given linked list. 




