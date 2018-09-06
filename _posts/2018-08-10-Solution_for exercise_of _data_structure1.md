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

### Sort a given linked list. 

+ If you get stucked on this problem, you may also try the following problems first.

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

   ```cpp
   void swap_node(node * element, int i, int j) {
        int k = 0;
        node *prenode_i;
        node *node_i;
        node *nextnode_i;
        node *prenode_j;
        node *node_j;
        node *nextnode_j;
        while (element != NULL) {
            if (k == i-1) {
                prenode_i = element;
            }
            else if (k == i) {
                node_i = element;
            }
            else if (k == i + 1){
                nextnode_i = element;
            }
            else if (k == j-1) {
                prenode_j = element;
            }
            else if (k == j) {
                node_j = element;
            }
            else if (k == j + 1) {
                nextnode_j = element;
            }
            element = element->next;
            k++;
        }
        prenode_i->next = node_j;
        node_j->next = nextnode_i;
        prenode_j->next = node_i;
        node_i->next = nextnode_j;
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
    node * swap_node_adjacent(node * head, int i, int n) {
        int k = 0;
        node * new_element = head->next;
        node *prenode_i = NULL;
        node *node_i = NULL;
        node *node_j = NULL;
        node *nextnode_j = NULL;
        while (new_element) {
            if (k == i-1) prenode_i = new_element;
            else if (k == i) node_i = new_element;
            else if (k == i + 1) node_j = new_element;
            else if (k == i + 2) nextnode_j = new_element;
            if (i == 0) prenode_i = head;
            new_element = new_element->next;
            k++;
        }
        if (prenode_i) prenode_i->next = node_j;
        node_j->next = node_i;
        node_i->next = nextnode_j;
        return node_i;
    }
   ``` 
   for example `swap_node_adjacent(head, 0, 5)`, `5 4 3 2 1` turns to `4 5 3 2 1` and return `5`. 
   then we implement the bubble sort: 
   ```cpp
    void bubble_sort_linked_list(node * head, int n) {
        int i, j;
        for (i = 0; i < n-1; i++) {
            node * element = head->next;
            for (j = 0; j < n-1-i; j++) {
                if ((element->data) > ((element->next)->data)) {
                    element = swap_node_adjacent(head, j, n);
                } else element = element->next;
            }
        }
    }                                                                                                                                                                       
   ``` 


   + **Given an ordered linked list, insert a new number without destroying its order.** 

   ```cpp
    node * finde_node(node * head, int k, int n) {
        node * element = head->next;
        for (int j = 0; j < n && element != NULL; j++) {
            if (j == k) return element;
            element = element->next;
        }
    }

    void insert_order(node * head,  int key_value, int n) {
        node * new_element = new node;
        new_element->data = key_value;
        node * m_node = new node;
        for (int i = 0; i < n; i++) {
            m_node = finde_node(head, i, n);
            if (i == 0 && key_value < m_node->data) {
                head->next = new_element;
                new_element->next = m_node;
                break;
            } else if (i == n-1 && key_value > m_node->data) {
                m_node->next = new_element;
                new_element->next = NULL;
                break;
            } else {
                if (m_node->data <= key_value && m_node->next->data >= key_value) {
                    new_element->next = m_node->next;
                    m_node->next = new_element;
                    break;
                }
            }
        }
        m_node = NULL;
        new_element = NULL;
        delete new_element;
        delete m_node;
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
class Stack {
    int top;
    int* MAX[n];
    int m_top;
public:
    int a[n];
    Stack() {
        top = -1;
        *MAX = INT_MIN;
        m_top = 0;
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
        cout << "after push, MAX = " << *MAX[m_top] << endl;
        return true;
    }
}

int Stack::pop() {
    if (top < 0) {
        cout << " Stack underflow" << endl;
        return 0;
    } else {
        if (&a[top] == MAX[m_top]) --m_top;
        int x = a[top--];
        cout << "after pop, MAX = " << *MAX[m_top] << endl;
        return x;
    }
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

    unfinished->... 



   



   
