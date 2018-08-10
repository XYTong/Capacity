---
layout: post
title: me,data structure, exercise, solution_1
---
# Part I 
 
## Basic data structures 

**thanks for the help by [simonmysun](https://github.com/simonmysun) for the Collectionin in learning and practicing of data structure** 
 
--- 
the following comes the solutions and summary of [data structure](https://xytong.github.io/Capacity/2018/07/20/Learning_data_structure.html): 

the previous part **Data type** [click here](https://xytong.github.io/Capacity/2018/07/20/Solution_for_exercise_of_data_structure.html) 

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

+ **Reverse a given linked list(unless otherwise specified, linked lists refer to sigly linked list of number)** 

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

+ **Find *n* th node from the end of a given linked list.** 

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

+ **Sort a given linked list.** 

   + Find and delete a specified node in a given linked list.
    
   ```cpp 
   find_element(node* head, int n, int* target) {
        element = head;
        int flag = 0;
        for(int i = 0; i < n && element != NULL; i++){
            element = element->next
            if(*target == element->next ) {
                flag = 100
                return i;
            }
            if (flag == 0) {
                return 0;
            }
        }
   }

   ``` 
   + **Swap two nodes on a given linked list.** 
   for a linked list with size *n*, if we wanna swap tow nodes (`i and j for 0 =< i, j < n`) 
   named as node_i and node _j.  
   with `find_element` we can easily find the  tow previous and next nodes of *i* and *j* nodes. just named 
   as prenode_i, prenode_j and nextnode_i, nextnode_j. then we can reset `prenode_i->next = node_j`, `node_j->next = nextnode_i` 
   `prenode_j = node_i`, `node_i->next = nextnode_j` . 
   for example 10 nodes linked list and swap 3 and 6, following is the result: 
   `1 2 3 4 5 6 7 8 9 10`
   `1 2 6 4 5 3 7 8 9 10` 