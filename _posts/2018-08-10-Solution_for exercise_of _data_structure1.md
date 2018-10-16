---
layout: post
title: Part I
---
# Basic data structures
 
## Abstract 

**thanks for the help by [simonmysun](https://github.com/simonmysun) for the Collectionin in learning and practicing of data structure** 
 
--- 
the following comes the solutions and summary of [data structure](https://xytong.github.io/Capacity/2018/07/20/Learning_data_structure.html): 

the previous part **Data type** [click here](https://xytong.github.io/Capacity/2018/07/20/Solution_for_exercise_of_data_structure.html) 

## Linked list 

### Use arrays to implement linked lists. 

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


### Reverse a given linked list(unless otherwise specified, linked lists refer to sigly linked list of number) 

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

### Find *n* th node from the end of a given linked list. 


```cpp 
node * find_r_n_node(node * head， int n) {
    node * slow = head;
    node * fast = head->next;
    for (int i = 0; i < n-1; i++) {
        fast = fast->next;
    }
    while (fast != NULL && fast->next != NULL) {
        fast = fast->next;
        slow = slow->next;
    }
    return slow;
}
``` 


### Find the middle node of a given linked list. 

```cpp 
node * slow = head;
node * fast = head->next; 
while(fast != NULL && fast->next != NULL) {
    slow = slow->next;
    fast = fast->next->next;
}
return slow;
``` 

### Sort a given linked list. 

+ If you get stucked on this problem, you may also try the following problems first.

   + Find and delete a specified node in a given linked list.
    
   ```cpp 
   void find_element(node* head, int* target) {
        element = head;
        while (element != target) {
            element = element->next;
        }
        element->pre->next = element->next;
        element->next->pre = element->pre;
   }

   ``` 
   + **Swap two nodes on a given linked list.** 
   for a linked list with size *n*, if we wanna swap tow nodes (`i and j for 0 =< i, j < n`) 
   named as node_i and node _j.  
   with `find_element` we can easily find the  tow previous and next nodes of *i* and *j* nodes. just named 
   as prenode_i, prenode_j and nextnode_i, nextnode_j. then we can reset `prenode_i->next = node_j`, `node_j->next = nextnode_i` 
   `prenode_j = node_i`, `node_i->next = nextnode_j` . 

   ```cpp
  void swap_node(node* a, node* b) {
      node * temp_a = new node;
      node * temp_b = new node;
      *temp_a = *a;
      *temp_b = *b;
      *a = *b;
      a->pre = temp_a->pre;
      a->next = temp_a->next;
      *b = *temp_a;
      b->pre = temp_b->pre;
      b->next = temp_b->next;
      delete temp_a;
      delete temp_b;
  } 
   ``` 
   for example 10 nodes linked list and swap 3 and 6, following is the result: 
   `1 2 3 4 5 6 7 8 9 10` 
   `1 2 6 4 5 3 7 8 9 10` 


   + **Implement *bubble sort* on linked lists.** 

   classic bubble sort for array in *c++* [WiKi](https://en.wikipedia.org/wiki/Bubble_sort): 

   ```cpp 
    #include <iostream>
    #include <algorithm>
    using namespace std;
    template<typename T> //整數或浮點數皆可使用,若要使用物件(class)時必須設定大於(>)的運算子功能
    void bubble_sort(T arr[], int len) {
        int i, j;
        for (i = 0; i < len - 1; i++)
            for (j = 0; j < len - 1 - i; j++)
                if (arr[j] > arr[j + 1])
                    swap(arr[j], arr[j + 1]);
    }
    int main() {
        int arr[] = { 61, 17, 29, 22, 34, 60, 72, 21, 50, 1, 62 };
        int len = (int) sizeof(arr) / sizeof(*arr);
        bubble_sort(arr, len);
        for (int i = 0; i < len; i++)
            cout << arr[i] << ' ';
        cout << endl;
        float arrf[] = { 17.5, 19.1, 0.6, 1.9, 10.5, 12.4, 3.8, 19.7, 1.5, 25.4, 28.6, 4.4, 23.8, 5.4 };
        len = (int) sizeof(arrf) / sizeof(*arrf);
        bubble_sort(arrf, len);
        for (int i = 0; i < len; i++)
            cout << arrf[i] << ' ';
        return 0;
    }
   ``` 

   base on this code we can implement bubble sort for **Linked List**. 
   first build a module for swap two adjacent elements of the linked list. this function returns the element which was 
   beyond the another and after swapping goes to be behind it. and `i` is the swap position for `i` and `i+1`, `n` is the 
   length of linked list.  
   ```cpp 
    void bubble_sort(node * head) {
        do {
            node * element = head;
            while (element != find_r_n_node(head, i)) {
                if element->data > element->next->data;
                swap_node(element, element->next);
                element = element->next;
                i++;
            }
        } while (head->next = find_r_n_node(head, i))
    }
   ``` 



   + **Given an ordered linked list, insert a new number without destroying its order.** 

   ```cpp
    void insert_ordered_ll(node ** head, node * new_e) {
        if (new_e->data < head->data) {
            new_e->next = *head;
            *head = new_e;
            return;
        }
        for (node * element = *head; element != NULL; element = element->next) {
            if (element->next == NULL) {
                if (new->data >= element->data) {
                    element->next = new;
                    return;
                }
            }
            if (new_e->data >= element->data && new_e->data <= element->next->data) {
                element->next = new_e;
                new_e->next = element->next;
                return;
            }
        }
    }
   ``` 
   following is the result of an example: 

   `1 2 9 10 11` -> `1 2 6 9 10 11` 



   + **Implement insertion sort on linked lists.** 
   fisrt of all we build a **double linked list**. struct `node` contains 3 elements: **value** of single node, pointer to 
   **next node**, pointer to **previous node**. 

   ```cpp 
    struct node {
        int data;
        struct node * pre;
        struct node * next;
    };
   ```
   with function `create_node(int val)` to create every node in loop. 

   ```cpp 
    node* create_node(int val) {
        node * newnode = (node*)malloc(sizeof(node));
        if (newnode == NULL) {
            cout << "out of memory !" << endl;
            return NULL;
        } else {
            newnode->data = val;
            newnode->next = NULL;
            newnode->pre = NULL;
            return newnode;
        }
    }
   ``` 

   `node * insert_double_linked_list(node * head, node * tail, int val)` to connect current tail with new node and 
   return new tail. 

   ```cpp 
    node * insert_double_linked_list(node * head, node * tail, int val) {                                                             node *newnode = create_node(val);
        if (!tail) {
            head->next = newnode;
            newnode->pre = head;
            tail = newnode;
        }
        else {
            tail->next = newnode;
            newnode->pre = tail;
            tail = newnode;
        }
        return tail;
    }
   ``` 

   based on **insert sort** for *array* [WiKi](https://en.wikipedia.org/wiki/Insertion_sort): 

   ```cpp 
    void insertion_sort(int arr[],int len){
            for(int i=1;i<len;i++){
                    int key=arr[i];
                    int j;
                    for(j=i-1;j>=0 && key<arr[j];j--)
                            arr[j+1]=arr[j];
                    arr[j+1]=key;
            }
    }
   ``` 

   we can easily implement insert sort for linked list: 

   ```cpp 
    void insertion_sort(node * head) {
        for (node * m_node = head->next; m_node != NULL; m_node = m_node->next) {
            int key = m_node->data;
            node * s_node;
            for (s_node = m_node->pre; s_node != NULL && key < s_node->data; s_node = s_node->pre) {
                s_node->next->data = s_node->data;
            }
            if (s_node) s_node->next->data = key;
            else head->data = key;
        }
    }
   ``` 

   following is the left code: 

   ```cpp 
    int main() {
        int arr[100];
        int n;
        cin >> n;
        for (int i = 0; i < n; i++) cin >> arr[i];
        node * tail;
        node * head;
        for (int i = 0; i < n; i++) {
            if (i == 0) {
                head = create_node(arr[i]);
            } else tail = insert_double_linked_list(head, tail, arr[i]);
        }
        for (node * element = head; element != NULL; element = element->next) cout << element->data << " ";
        cout << endl;
        for (node * element = tail; element != NULL; element = element->pre) cout << element->data << " ";
        cout << endl;
        insertion_sort(head);
        for (node * element = head; element != NULL; element = element->next) cout << element->data << " ";
        cout << endl;
    }
   ``` 

   here is the result: 
   **input**: 
   10 

   10 5 2 7 6 8 3 9 1 4 

   **output**:  


   10 5 2 7 6 8 3 9 1 4 

   4 1 9 3 8 6 7 2 5 10 

   1 2 3 4 5 6 7 8 9 10 

   + **Given a linked list, divide them into two even halves.** 

   + **Given two ordered linked lists, merge them into one ordered linked list.** 

   + **Implement merge sort on linked lists.** 

    these three we can solve in a row. 

    if we wanna implement **merge sort**, first we need divide linked list into **two halves**  
    hence we use double pointer `node** head_1` and `node** head_1` to receive the two head of lists which was spilted 
    
    ```cpp 
    void divide_node(node * head, node** head_1, node** head_2) {
        if (!head) return;
        *head_1 = head;
        node * slow = head;
        node * fast = head->next;
        while(fast) {
            if (fast->next) fast = fast->next->next;
            else break;
            slow = slow->next;
        }
        *head_2 = slow->next;
        slow->next = NULL;
    }
    ``` 


    then we build a function `node * merge_node(node* head_1, node* head_2)` which based on **recursion**. input **two**  
    heads of linked lists and output one head of linked lsit which is merged by these two linked list. 

    ```cpp 
    node * merge_node(node * head_1, node * head_2) {
        node * head = NULL;
        if (!head_1) return head_2;
        if (!head_2) return head_1;
        if (head_1->data < head_2->data) {
            head = head_1;
            head->next = merge_node(head_1->next, head_2);
        }
        else {
            head = head_2;
            head->next = merge_node(head_1, head_2->next);
        }
        return head;
    }
    ``` 

    finally we implement a **merge sort** , but we must consider that using recursion to spilt node as single and then merge 

    every two adjacent sublists. 

    ```cpp 
void merge_sort(node** head) {
    node * head_1;
    node * head_2;
    node * p_head = *head;
    if (!p_head || !p_head->next) return;
    cout << "OK" << endl;
    divide_node(p_head, &head_1, &head_2);
    merge_sort(&head_1);
    merge_sort(&head_2);
    *head = merge_node(head_1, head_2);
}
    ``` 

    + **Given a linked list, divide them into two halves(might not be even) and meanwhile let each number in the first half be greater than all numbers in the second half.** 

    + **Implement quick sort on linked lists.** 

    we can solve these two questions as a row. 

    first we need a **swap** fucction to swap two nodes. 

    ```cpp
    void swap_node(node* a, node* b) {
        node * temp_a = new node;
        node * temp_b = new node;
        *temp_a = *a;
        *temp_b = *b;
        *a = *b;
        a->pre = temp_a->pre;
        a->next = temp_a->next;
        *b = *temp_a;
        b->pre = temp_b->pre;
        b->next = temp_b->next;
        delete temp_a;
        delete temp_b;
    }
    ``` 

    then we build a function `partion` to put the numbers lower than **pivot** to the left and the numbers greater than pivot 
    to the right. 

    ```cpp 
    node* get_partion(node* head, node * end) {
        int key = head->data;
        node* p = head;
        node* q = p->next;

        while(q != end) {
            if(q->data < key) {
                p = p->next;
                swap_node(p, q);
            }
            q = q->next;
        }
        swap_node(p, head);
        return p;
    }
    ``` 

    the main function for quick sort. Recur for the list before pivot and after the pivot element. 

    ```cpp 
    void quick_sort(node * head, node * end) {
        if (head != end) {
            node * partion = get_partion(head, end);
            quick_sort(head, partion);
            quick_sort(partion->next, end);
        }
    }
    ```


### Given a linked list(assume it is), tell whether there is a loop and find the entry of it. 

```cpp 
#include <iostream>
using namespace std;

int main() {
    node * slow = head->next;
    node * fast = head->next->next;
    while (fast) {
        if (slow == fast) break;
        slow = slow->next;
        fast = fast->next->next;
    }
    node * p = slow;
    node * new_element = head;
    while(new_element == p) {
        new_element = new_element->next;
        p = p->next;
    }
    node * entry = p;
}
``` 


### Given two linked list, tell whether and where they intersect each other. What if there can be loops? 


```cpp 
find_intersection_point(node * head1, node * head2) {
    for (node * element1 = head1; element1 != NULL; element1 = element1->next)
        for(node * element2 = head2; element2 != NULL; elemnt2 = element2->next)
            if (element1 == element2) return element1;
}
``` 

```cpp 
node * find_intersection_point_loop(node * head1, node * head2) {
    if (head1 == head2) return head1
    node * fast = head1->next;
    node * slow = head1;
    node * tail;
    while(fast != slow) {
        if (fast->next || fast->next->next) {
            fast->next = head;
            tail = fast;
        }
        fast = fast->next->next;
        slow = slow->next;
    }
    node * p = slow;
    node * new_element = head1;
    while(new_element == p) {
        new_element = new_element->next;
        p = p->next;
    }
    tail->next = NULL;
    return p;
}
```

## Stack 

### Use array to implement stacks. 

+ Push a node into a given stack. 

+ Pop a node from a given stack. 

+ Peak the top node of a given stack. 

+ Empty a given stack. 


```cpp 
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

#define n 1000
class Stack {
    int top;
public:
    int a[n];
    Stack() { top = -1;}
    bool push(int x);
    int pop();
    bool empty();
};

bool Stack::push(int x) {
    if (top >= n-1) {
        cout << " Stack overflow" << endl;
        return false;
    } else {
        a[++top] = x;
        return true;
    }
}

int Stack::pop() {
    if (top < 0) {
        cout << " Stack underflow" << endl;
        return 0;
    } else {
        int x = a[top--];
        return x;
    }
} 

void Stack::empty() {
    top = -1;
}

int Stack::peak_top() {
    if (top >= 0) return a[top];
}
```


### Use pointers or references to implement stacks. Including the operations above. 


```cpp 
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <iostream>
using namespace std;

struct StackNode {
    int data;
    struct StackNode* next;
};

void * push(StackNode** top, int value) {
    StackNode * new_node = (StackNode*) malloc(sizeof(StackNode));
    new_node->data = value;
    new_node->next = *top;
    *top = new_node;
    cout << new_node->data << " pushed to stack" << endl;
}

int pop(StackNode** top) {
    if(!*top) return -1;
    StackNode* temp = *top;
    *top = (*top)->next;
    int popped = temp->data;
    free(temp);
    return popped;
}

int peak(StackNode* top) {
    if (!top) return -1;
    return top->data;
}

int main() {
    StackNode* top = NULL;
    push(&top, 1);
    push(&top, 2);
    push(&top, 3);
    cout << "poped is " << pop(&top) << endl;
    cout << "top is " << peak(top) << endl;
}
``` 


### Given a sequence of push operations and a sequence of pop operations, tell whether it can be valid. 

see the first quiz... 

### Implement a queue supporting push(). pop() and getMin(). 

```cpp 
#include <iostream>
#include <bits/stdc++.h>
#include <limits>
#include <cstring>
using namespace std;

#define n 1000
class Stack {
    int top;
    int* *MAX;
    int* *MIN;
    int m_top;
    int min_top;
    int a[n];
    int MIN_INT = INT_MIN;
    int MAX_INT = INT_MAX;
public:
    Stack() {
        top = -1;
        m_top = 0;
        min_top = 0;
        MAX = new int* [n];
        MIN = new int* [n];
        *MAX = &MIN_INT;
        *MIN = &MAX_INT;
    }
    bool push(int x);
    int pop();
    int peak_top();
    void empty();
};

bool Stack::push(int x) {
    if (top >= n-1) {
        cout << " Stack overflow" << endl;
        return false;
    } else {
        a[++top] = x;
        if (x >= *MAX[m_top]) MAX[++m_top] = &a[top];
        if (x <= *MIN[min_top]) MIN[++min_top] = &a[top];
        cout << "after push, MAX = " << *MAX[m_top] << " MIN = " << *MIN[min_top] << endl;
        return true;
    }
}

int Stack::pop() {
    if (top < 0) {
        cout << " Stack underflow" << endl;
        return 0;
    } else {
        if (&a[top] == MAX[m_top]) --m_top;
        if (&a[top] == MIN[min_top]) --min_top;
        int x = a[top--];
        cout << "after pop, MAX = " << *MAX[m_top] << " MIN = " << *MIN[min_top] << endl;
        return x;
    }
}

void Stack::empty() {
    top = -1;
}

int Stack::peak_top() {
    if (top >= 0) return a[top];
}

int main() {
    Stack stack1;
    stack1.push(2);
    stack1.push(5);
    stack1.push(3);
    stack1.push(6);
    stack1.push(1);
    stack1.push(9);
    cout << stack1.peak_top() << endl;
    cout << stack1.pop() << endl;
    stack1.empty();
}
``` 

after push, MAX = 2 MIN = 2 

after push, MAX = 5 MIN = 2 

after push, MAX = 5 MIN = 2 

after push, MAX = 6 MIN = 2 

after push, MAX = 6 MIN = 1 

after push, MAX = 9 MIN = 1 

9 

after pop, MAX = 6 MIN = 1 

9 


### Implement undo/redo functionality(or back/forward navigation in explorer). 

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





### Without recursion, use backtracking to solve n queens problem. 

```cpp 
#include <iostream>
#include <stdio.h>
#include <stack>
#define N 16
using namespace std;

class Operation {
    int b[N][N];
    int x;
    int y;
    stack <int> stack_alpha;
public:
    Operation() {
        for (int i = 0; i < N; i++) for (int j = 0; j < N; j++) b[i][j] = 0;
        x = 0;
        y = 0;
    }

    bool execute() {
        for (; x < N; x++) {
            if (is_Safe()) {
                stack_alpha.push(x);
                b[x][y] = 1;
                y++;
                x = 0;
                return true;
            }
        }
        return false;
   }

    bool is_Safe() {
        int i ,j;
        for (i = 0; i < y; i++) if (b[x][i]) return false;
        for (i = x, j = y; i >= 0 && j >= 0; --i, --j) if (b[i][j]) return false;
        for (i = x, j = y; j >= 0 && i < N; ++i, --j) if (b[i][j]) return false;
        return true;
    }

    bool put_into_stack() {
        do {
            if (execute()) { }
            else {
                y--;
                x = stack_alpha.top();
                stack_alpha.pop();
                cout << "x = " << x << endl;
                b[x++][y] = 0;
            }
            if (y >= N) return true;
        } while (x >= 0 && y >= 0);
        return false;
    }

    void print_solution() {
        if (put_into_stack()) {
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < N; j++) {
                    cout << b[i][j] << " ";
                }
                cout << endl;
            }
        } else cout << "not exist" << endl;
    }

};

int main() {
    Operation _operation;
    _operation.print_solution();
}
``` 


using ` class Stack` above. 

```cpp 
class Operation {
    int b[N+1][N+1];
    int x;
    int y;
    int diag_a[2*MAXN];
    int diag_b[2*MAXN];
    short pre[MAXN];
    short next[MAXN];
    Stack stack_alpha;
    int s;
    int s1;
public:
    Operation() {
        for (int i = 1; i <= N; i++)
            for (int j = 1; j <= N; j++) b[i][j] = 0;
        memset(diag_a, 1, sizeof(diag_a));
        memset(diag_b, 1, sizeof(diag_b));
        for (int k = 1; k <= N; k++) {
            pre[k] = k-1;
            next[k] = k+1;
        }
        pre[N+1] = N;
        next[0] = 1;
        x = 0;
        y = 1;
        s = 0;
        s1 = 0;
    }

    int put_into_stack() {
        do {
            if (stack_alpha.bot() <= N/2+1) {
                if (y > N) {
                    if (stack_alpha.bot() == N/2+1) s1++;
                    else s++;
                    y--;
                    x = stack_alpha.peak_top();
                    diag_a[x+y] = 1;
                    diag_b[x-y+N] = 1;
                    next[pre[x]] = x;
                    pre[next[x]] = x;
                    b[x][y] = 0;
                    stack_alpha.pop();
                    x = stack_alpha.peak_top();
                    stack_alpha.pop();
                    y--;
                }
                else {
                    if (x != 0) {
                        diag_a[x+y] = 1;
                        diag_b[x-y+N] = 1;
                        next[pre[x]] = x;
                        pre[next[x]] = x;
                    }
                    x = next[x];
                    while (x <= N) {
                        if (diag_a[x+y] && diag_b[x-y+N]) break;
                        x = next[x];
                    }
                    if (x > N) {
                        y--;
                        x = stack_alpha.peak_top();
                        b[x][y] = 0;
                        stack_alpha.pop();
                        continue;
                    }
                    stack_alpha.push(x);
                    diag_a[x+y] = 0;
                    diag_b[x-y+N] = 0;
                    next[pre[x]] = next[x];
                    pre[next[x]] = pre[x];
                    b[x][y] = 1;
                    y++;
                    x = 0;
                }
            }
        } while (stack_alpha.bot() <= N/2+1);
        if (n%2 == 0) s*=2;
        else s = 2*s + s1;
        return s;
    }
};

int main() {
    Operation _operation;
    int c = _operation.put_into_stack();
    cout << c << endl;
}
``` 

for `N = 16` it has 14772512 solutions. 


### Based on the expression evaluator above, add × and ÷ support. 

### Based on the expression evaluator above, add brackets support. 


```cpp 
#include <iostream>
#include <stack>
#include <cstring>
using namespace std;
#define N 100
class Caculator {
    stack<double> num;
    stack<char> op;
    stack<double> pre;
    char *s;
    int k;
    char c;
    int end;
public:
    Caculator(char _s[]) {
        op.push('\0');
        s = new char[strlen(_s) + 1];
        strcpy(s, _s);
        k = 0;
        end = 0;
        c = s[k];
    }

    double transform_num() {
        int flag = 0;
        double x = 0.0;
        double y = 0.1;
        while (s[k] >= '0' && s[k] <= '9' || s[k] == '.') {
            if (s[k] >= '0' && s[k] <= '9') {
                if (flag == 0) x = x*10 + (s[k] - '0');
                else {
                    x = x + y*(s[k] - '0');
                    y*=0.1;
                }
            }
            else flag = 1;
            k+=1;
        }
        return x;
    }
    int priority(char opx) {
        int k;
        switch (opx) {
            case '*' : k = 2; break;
            case '/' : k = 2; break;
            case '+' : k = 1; break;
            case '-' : k = 1; break;
            case '(' : k = 0; break;
            case ')' : k = 0; break;
            default : k = -1; break;
        }
        return k;
    }

    void caculate() {
        int x, y;
        cout << s << endl;
        int i = 0;
        while (!end) {
            if (c >= '0' && c <= '9' || c == '.') {
                num.push(transform_num());
            }
            else if (c == '(' || priority(c) > priority(op.top())) {
                op.push(c);
                k++;
            }
            else if (c == ')' && op.top() == '(') {
                op.pop();
                k++;
            }
            else if (c == 'a') {
                num.push(pre.top());
                k+=3;
            }
            else if (c == '\0' && op.top() == '\0') end = 1;
            else if (priority(c) <= priority(op.top())) {
                x = num.top();
                num.pop();
                y = num.top();
                num.pop();
                c = op.top();
                op.pop();
                switch (c) {
                    case '+' : y = x + y; break;
                    case '-' : y = y - x; break;
                    case '*' : y = x * y; break;
                    case '/' : y = x / y; break;
                }
                num.push(y);
            }
            c = s[k];
            i++;
        }
        cout << "ans = " << num.top() << endl;
        pre.push(num.top());
    }
};

int main() {
    char _s[100];
    cin >> _s;
    Caculator caculator(_s);
    caculator.caculate();
    int exit = 0;
};
``` 


## Queue 

###Use arrays to implement queue.
+ Enqueue a node into a given queue. 

+ Dequeue a node from a given queue. 

+ Empty a queue. 

```cpp 
#include <stdio.h>
#include <iostream>
#include <limits.h>

struct Queue {
    int front;
    int rear;
    int size;
    unsigned capacity;
    int* a;
};

Queue * create_queue(unsigned capacity) {
    Queue * queue = (Queue*) malloc(sizeof(Queue));
    queue->capacity = capacity;
    queue->front = queue->size = 0;
    queue->rear = capacity - 1;
    queue->a = (int*) malloc(queue->capacity * sizeof(int));
    return queue;
}

void enqueue(Queue * queue, int data) {
    if (queue->size == queue->capacity) {
        cout << "Queue overflow" << endl;
        return;
    }
    queue->rear = (queue->rear+1)%queue->capacity;
    queue->a[queue->rear] = data;
    queue->size = queue->size + 1;
    cout << "enqueued to queue " << data << endl;
}

int dequeue(Queue * queue) {
    if (queue->size == 0) {
        cout << "Queue underflow" << endl;
        return;
    }
    int data = queue->a[queue->front];
    queue->size = queue->size - 1;
    return data;
}

int front(Queue * queue) {
    return queue->a[queue->front];
}

int rear(Queue * queue) {
    return queue->a[queue->rear];
} 
``` 

### Use pointers or references to implement linked lists. 

```cpp 
#include <stdio.h>
#include <stdlib.h>
#include <limits.h>
#include <iostream>
using namespace std;

struct Queue {
    int data;
    struct Queue* next;
};

void * push(Queue** bot, int value) {
    StackNode * new_node = (StackNode*) malloc(sizeof(StackNode));
    new_node->data = value;
    new_node->next = *bot;
    *bot = new_node;
    cout << new_node->data << " pushed to stack" << endl;
}

int pop(StackNode** bot) {
    if(!*bot) return -1;
    StackNode* temp = *bot;
    *bot = (*bot)->next;
    int popped = temp->data;
    free(temp);
    return popped;
}

int peak(StackNode* top) {
    if (!top) return -1;
    for (element = bot; element != NULL && element->next != NULL; element = element->next) {}
    return element;
} 
``` 

### Implement a circular buffer. // TODO: Better problem needed 


### Implement a message queue. // TODO: Better problem needed 


## Tree 

### Explain binary tree, full binary tree, complete binary tree. 

>In computer science, a binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child. 

>A full binary tree (sometimes referred to as a proper[15] or plane binary tree)[16][17] is a tree in which every node has either 0 or 2 children. 

>In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2^h nodes at the last level h. 


### Given the root node of a tree, print its pre-order traversal, in-order traversal, post-order traversal and level-order traversal. 

```cpp 
#include <iostream>
#include <stdlib.h>
using namespace std;

struct BiNode {
    int data;
    struct BiNode *l_child, *r_child;
};

class BiTree {
public:
    void Create_Root(BiNode * root, int root_value) {
        root->data = root_value;
    }
    void Create_BiTree(BiNode ** T);
    bool is_Empty(BiNode* T);
    int BiTree_Depth(BiNode* T);
    void pre_Order(BiNode* T);
    void in_Order(BiNode* T);
    void post_Order(BiNode* T);
};

void BiTree :: Create_BiTree(BiNode ** T) {
    int value;
    cin >> (value);
    if (!cin.good()) {
        *T = NULL;
        cin.clear();
        cin.ignore();
    }
    else {
        * T = (BiNode*) malloc(sizeof(BiNode));
        (*T)->data = value;
        Create_BiTree(&(*T)->l_child);
        Create_BiTree(&(*T)->r_child);
    }
}

bool BiTree :: is_Empty(BiNode* T) {
    if(T) return false;
    else return true;
}

int BiTree :: BiTree_Depth(BiNode* T){
    int i, j;
    if (T == NULL) return 0;
    if (T->l_child) i = BiTree_Depth(T->l_child);
    else i = 0;
    if (T->r_child) j = BiTree_Depth(T->r_child);
    else j = 0;
    return i>j? i+1:j+1;
}

void BiTree :: pre_Order(BiNode* T) {
    if (T != NULL) {
        cout << T->data << " ";
        pre_Order(T->l_child);
        pre_Order(T->r_child);
    }
}

void BiTree :: in_Order(BiNode* T) {
    if (T != NULL) {
        in_Order(T->l_child);
        cout << T->data << " ";
        in_Order(T->r_child);
    }
}

void BiTree :: post_Order(BiNode* T) {
    if (T != NULL) {
        post_Order(T->l_child);
        post_Order(T->r_child);
        cout << T->data << " ";
    }
}

int main() {
    BiNode * root;
    BiTree bitree;
    //bitree.Create_Root(root, 1);
    bitree.Create_BiTree(&root);
    bitree.pre_Order(root);
}
```  

   + **Same problem, without recursion.** 

   ```cpp 
    void BiTree :: nr_pre_Order(BiNode* T) {
        stack<BiNode*>lr;
        BiNode * element = T;
        cout << element->data << " ";
        do {
            if (element->l_child != NULL) {
                lr.push(element);
                cout << element->l_child->data << " ";
                element = element->l_child;
            }
            else {
                if (element->r_child != NULL) cout << element->r_child->data << " ";
                do {
                    if (lr.empty()) return;
                    element = lr.top()->r_child;
                    lr.pop();
                } while(element == NULL && !lr.empty());
                if(element != NULL) {
                    cout << element->data << " ";
                }
                else return;
            }
        } while (true);
    }
   ``` 


### Given the post-order traversal and in-order traversal of a tree, print its pre-order traversal. 


```cpp
int BiTree :: find(int arr[], int start, int end, int value) {
    int i;
    for(i = start; i <= end; i++)
        if (arr[i] == value) return i;
}

BiNode* BiTree :: reconstruction_i_p(int in[], int pre[], int in_start, int in_end) {
    static int pre_i = 0;
    if (in_start > in_end) return NULL;
    BiNode* t_node = Create_BiNode(pre[pre_i++]);
    if (in_start == in_end) return t_node;
    int in_i = find(in, in_start, in_end, t_node->data);
    t_node->l_child = reconstruction_i_p(in, pre, in_start, in_i-1);
    t_node->r_child = reconstruction_i_p(in, pre, in_i+1, in_end);
    return t_node;
}

BiNode* BiTree :: reconstruction_i_post(int in[], int post[], int in_start, int in_end) {
    static int post_i = in_end;
    if (in_start > in_end) return NULL;
    BiNode* t_node = Create_BiNode(post[post_i--]);
    if (in_start == in_end) return t_node;
    int in_i = find(in, in_start, in_end, t_node->data);
    t_node->r_child = reconstruction_i_post(in, post, in_i+1, in_end);
    t_node->l_child = reconstruction_i_post(in, post, in_start, in_i-1);
    return t_node;
}
``` 


### Given a tree with a in-order traversal of which the data are in increasing order, i.e. BST, insert a new node while keeping this property. 

   + Implement a sorting algorithm with it (tree sort). 

```cpp 
void BiTree :: insert_BiNode(BiNode* T, BiNode** last, int target) {
    if (T != NULL) {
        insert_BiNode(T->l_child, last, target);
        if (flag == 1) return;
        cout << T->data << endl;
        if (target <= T->data) {
            cout << target << " <= " << T->data << endl;
            if ((*last)->r_child == NULL) {
                BiNode* new_node = Create_BiNode(target);
                (*last)->r_child = new_node;
            } else {
                BiNode* new_node = Create_BiNode(target);
                T->l_child = new_node;
            }
            flag = 1;
            return;
        }
        else cout << target << " > " << T->data << endl;
        *last = T;
        insert_BiNode(T->r_child, last, target);
    }
}
``` 



```cpp 
BiNode* BiTree :: insert_BiNode(BiNode* T, int target) {
    if (T == NULL) {
        cout << "OK, root" << endl;
        T = Create_BiNode(target);
        return T;
    }
    if (target < T->data) T->l_child = insert_BiNode(T->l_child, target);
    else T->r_child = insert_BiNode(T->r_child, target);
    return T;
}

BiNode* BiTree :: insertion_sort(int d[], int n) {
    BiNode* tree = NULL;
    cout << "OK, start" << endl;
    for (int i = 0; i < n; i++) tree = insert_BiNode(tree, d[i]);
    return tree;
}
``` 

### Given n, how many structurally unique BST’s (binary search trees) that store values 1…n? 

we can use **Catalan Numbers** to solve this problem. 

The **n**th **Catalan number** is given directly in terms of binomial coefficients by$$C_{n} = \frac{n+1}{1}\bigl( \begin{smallmatrix} 2n \\ n \end{smallmatrix} \bigr) = \frac{(2n)!}{(n+1)!n!} = \prod_{k=2}^{n}\frac{n+k}{k}$$ 


### Analyze the complexity of BST, tell in which situation it behaves bad. 

best case, the height *h* equals to O(n), which means `complexity = O(logn)` 
because the time complexity depends on height of BST. 

the worst case it behaves bad when BST degenerate to Single tree branch. 

`complexity = O(n)` 

### Implement a binary heap. 

+ Consider a **complete binary tree**. Can it be properly stored in an array? How to get parent / child node of a given node? 

absolutly. 

one Node with index `i`, index of its left child and right child are$$2i+1, 2i+2$$ 

parent node (if exist) is$$\frac{2}{i-1}$$ 



    unfinished->... 



   



   
