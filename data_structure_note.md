# 1-0.数据结构含义、用途、数据结构与算法的区别

数据结构(data structure)：计算机中存储、组织数据的方式。

keywords:

1. 数据：例如手机联系人
2. 存储：手机联系人以列表的方式存储
3. 组织：CRUD

算法：更”高效“，”科学“，”优等“地组织。More effective

需要了解每个数据结构

* 占多少字节
* 怎么存储
* 如何组织

# 2-0.Computational Analysis of algorithms 计算机算法复杂度分析

时间复杂度

空间复杂度

二者由数据结构和算法两方面共同决定

# 3-0.复杂度分析举例

CRUD：对于增删改查4个方面的复杂度分析，首先重点是查，查单个元素的值。

1. 数组查找单个元素的值
   * O(1) T		时间复杂度O(1)
2. 遍历数组
   * O(n) T		时间复杂度O(n)

复杂度对比：

![File:Comparison computational complexity.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7e/Comparison_computational_complexity.svg/512px-Comparison_computational_complexity.svg.png)

# 4-1.Static array 复杂度分析

1. init 初始化
   * O(n) S

2. index 查询
   * O(1) T

3. 更改array[1] = 6
   * O(1) T

4. 插入数据：将原先的数组copy一份，从中插入
   * O(n) T
   * O(n) S
5. 删除（将数据清零）：前面的人删掉了，后面的人要跟进。后面的数据的下标要向前进，同时保证内存是back-to-back的。
   1. 从结尾处删除：O(1) T
   2. 从中间处删除：O(n) T
   3. 从开头处删除：O(n) T

Mark and sweep: 在删除时先标记，当要访问有内容删除的数据结构时，再统一执行前面有可能多次的删除操作。这样可以将多次 O(n) T 操作简化成一次 O(n) T 操作。

我们很少分析空间复杂度，因为空间复杂度是随着使用条件发生改变的。**我们在使用时首先分析时间复杂度，只有当我们认为空间复杂度成为一个问题时，我们才分析它。**

# 4-2.Dynamic Array扩容复杂度分析，剖析Java中ArrayList原理

考虑一个随元素个数增加而增长的[动态数组](https://zh.wikipedia.org/wiki/动态数组)，比如[Java](https://zh.wikipedia.org/wiki/Java)的`ArrayList`或者[C++](https://zh.wikipedia.org/wiki/C%2B%2B)的`std::vector`。如果我们的数组大小从4开始，那么来向其中增加四个元素的时间就是一个常数。然而，若要将第五个元素加入其中，那么会花费更多时间，因为我们此时必须要创建一个两倍于当前数组大小的数组（8个元素），把老元素拷贝到新数组中，然后增加一个新元素。接下来的三次加入操作也同样会花费常数时间，然后在数组被填满后则又需要一轮新的加倍扩充。

![AmortizedPush.png (450×400)](https://upload.wikimedia.org/wikipedia/commons/e/e5/AmortizedPush.png)

一般地，如果我们考虑任意一个任意的*n*大小的数组并对其进行*n* + 1次加入操作。我们注意到，所有的加入操作都是常数时间的，除了最后一个，它会花费O(n)时间在大小加倍上。因为我们进行了*n* + 1次加入操作，我们可以将数组加倍的时间平摊到所有的加入操作上，因此得到加入操作的平均时间是$\frac{nO(1)+O(n)}{n+1}$。它是一个常数。

**Wikipedia reference**: [平摊分析 - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/zh-cn/平摊分析)

# 5-0.Linked list与Singly linked list含义以及复杂度分析举例

## 单向链表

单向链表结构图(Reference: Wikipedia)：

![File:Singly-linked-list.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Singly-linked-list.svg/408px-Singly-linked-list.svg.png)

复杂度分析：

1. 增：在第n个节点处再增加一个节点的复杂度：O(n) T
2. 删：删除第n个节点的复杂度：O(n) T
3. 改：更改第n个节点的复杂度：O(n) T
4. 查：找到第n个节点的复杂度：O(n) T

在头节点处的增删改查复杂度均为：O(1) T

若单向链表没有存储尾指针，则在尾节点处的增删改查复杂度均为：O(1) T

若单向链表存储了尾指针，则在尾节点处的增删改查复杂度均为：O(1) T

## 双向链表

双向链表结构图(Reference: Wikipedia):

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Doubly-linked-list.svg/610px-Doubly-linked-list.svg.png)

复杂度分析：

1. 增：在第n个节点处再增加一个节点的复杂度：O(n) T
2. 删：删除第n个节点的复杂度：O(n) T
3. 改：更改第n个节点的复杂度：O(n) T
4. 查：找到第n个节点的复杂度：O(n) T

若双向链表没有存储尾指针，则在尾节点处的增删改查复杂度均为：O(1) T

若双向链表存储了尾指针，则在尾节点处的增删改查复杂度均为：O(1) T

## 循环链表

循环链表结构图(Reference: Wikipedia):

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/d/df/Circularly-linked-list.svg/350px-Circularly-linked-list.svg.png)

复杂度分析：

1. 增：在第n个节点处再增加一个节点的复杂度：O(n) T

2. 删：删除第n个节点的复杂度：O(n) T

3. 改：更改第n个节点的复杂度：O(n) T

4. 查：找到第n个节点的复杂度：O(n) T

若单向循环链表没有存储尾指针，则在尾节点处的增删改查复杂度均为：O(1) T

若单向循环链表存储了尾指针，则在尾节点处的增删改查复杂度均为：O(1) T

## 链表的应用

链表往往是为了**栈**和**队列**服务的。

网页的**前进**和**后退**是典型的双向链表。

数据结构是从**解决问题**的角度思考的。**（用什么方案）**

算法是从**提高效率**的角度思考的。**（提高方案的效率）**

**通常情况下先考虑选用什么数据结构，再考虑针对这个数据结构提高效率选用算法。**

**少数情况下先考虑效率，选择对应的数据结构。**

# 6-0.Hash

Hash function(散列函数)：Hash function是一种**将输入进行加密**的函数(算法)，输入经Hash Function**计算**得到的结果称为Hash sum。得到的Hash sum是**密文**。

![undefined](https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Hash_function.svg/1920px-Hash_function.svg.png)

![undefined](https://upload.wikimedia.org/wikipedia/commons/thumb/5/58/Hash_table_4_1_1_0_0_1_0_LL.svg/1920px-Hash_table_4_1_1_0_0_1_0_LL.svg.png)



## 哈希碰撞：

A Hash function takes different keys as input, but the result is the same hash code.

## 单向散列函数

将输入$I_1$通过单向散列函数$f_1()$可以得到对应的hash code $O_1$。但是由于加密方法$f_1$是未知的，所以通过$O_1$通过$f_1$反推$I_1$是做不到的。

我们只能过通过验证两个hash code $O_2$ 和 $O_1$ 是否相同来验证 $I_2$ 和 $I_1$ 是否相同。

# 6-1.Hash Table(Hash Map)

*A hash table is a data structure that implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a hash function to compute an index, also called a hash code, into an array of buckets or slots, from which the desired value can be found. — Wikipedia*



The hash map is used whenever data is stored as key-value pairs, where values can be added, retrieved, and deleted using keys.



In a hash table, every key is unique. We should use this data structure when the ordering and sorting of data is not needed, because the order of data is not retained here.

**Reference:**  

* https://medium.com/codex/hash-tables-hashing-and-collision-handling-8e4629506572
* https://www.geeksforgeeks.org/comparison-of-an-array-and-hash-table-in-terms-of-storage-structure-and-access-time-complexity/
* [Time and Space Complexity of Hash Table operations (opengenus.org)](https://iq.opengenus.org/time-complexity-of-hash-table/)
* [performance - What is the time complexity of HashMap.containsValue() in java? - Stack Overflow](https://stackoverflow.com/questions/16757359/what-is-the-time-complexity-of-hashmap-containsvalue-in-java)

key -> function ->index。然后将key存储到keys[index]中将value存储到values[index]中。

一切性能取决于function的好坏。

当然Hash碰撞是无法避免的，所以**在一些高级语言中**，当key1和key2**发生Hash碰撞**时，

value1和value2的存储会变成一个链表。

其格式类似为

```c
typedef struct node
{
    int value;
    int* key;
    struct node* next;
} node;
```

![undefined](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Hash_table_5_0_1_1_1_1_1_LL.svg/1920px-Hash_table_5_0_1_1_1_1_1_LL.svg.png)

## 复杂度

[Time complexity](https://en.wikipedia.org/wiki/Time_complexity) **in** [big O notation](https://en.wikipedia.org/wiki/Big_O_notation)

| Operation | **Average** | **Worst case** |
| :-------: | :---------: | :------------: |
|  LookUP   |    Θ(1)     |     O(*n*)     |
|  Search   |    Θ(n)     |     O(*n*)     |
|  Insert   |    Θ(1)     |     O(*n*)     |
|  Delete   |    Θ(1)     |     O(*n*)     |

[Space complexity](https://en.wikipedia.org/wiki/Space_complexity)

| Operation |                         **Average**                          | **Worst case** |
| :-------: | :----------------------------------------------------------: | :------------: |
|   Space   | Θ(*n*)[[1\]](https://en.wikipedia.org/wiki/Hash_table#cite_note-Cormen_et_al-1) |     O(*n*)     |

**Difference between Lookup and Search**

In a database context, a “search” is somewhat open-ended where you’re trying to find one or more records or rows that have a particular property.A “lookup” is where you have a specific record ID - whatever that means in the context of your application - and you want to pull up the details of that specific record.For example, a search is “find anyone in New York City who has two dogs”. A lookup is “Find the details of the person whose Social Security number is 123–45–6789”.This general usage also applies to non-database research-type activities. If you’re doing a “document search”, you’re scanning through a bunch of documents to find those with a specific thing in them, or covering a specific topic you’re interested in. If you’re doing a document lookup, you have a specific document in mind and are using its identifying code or other identifier to find it.

## C 实现

Using Linear Probing in Open Addressing technique to resolve hash collision.

```c
#include <stdio.h>
#include <stdint.h>
#include <stdlib.h>
#include <string.h>

#define Table_Size 10

typedef struct hash_table
{
    size_t size;
    uint32_t num_elements;
    char** keys;
    int32_t* values;
} HashTable;

HashTable* init_table(void);
int32_t hash(char* key);
void put(HashTable* table, char* key, int32_t value);
int32_t get(HashTable* table, char* key);
void remove_key(HashTable* table, char* key);
double load_factor(HashTable* table);
uint32_t num_elements(HashTable* table);

int main (void)
{   
    HashTable* table = init_table();

    char* key_01 = "ab123";
    char* key_02 = "ab231";
    char* key_03 = "ab321";

    put(table, key_01, 100);
    put(table, key_02, 200);
    put(table, key_03, 300);

    printf("%d %d %d %u %lf\n", get(table, key_01), get(table, key_02), get(table, key_03), num_elements(table), load_factor(table));

    remove_key(table, key_02);
    printf("%d %d %u %lf\n", get(table, key_01), get(table, key_03), num_elements(table), load_factor(table));

    remove_key(table, key_03);
    printf("%d %u %lf\n", get(table, key_01), num_elements(table), load_factor(table));

    char* key_test = "bbb";
    printf("%d\n", get(table, key_test));

    free(table->keys);
    free(table->values);
    free(table);

    return 0;
}

HashTable* init_table(void)
{
    HashTable* table = (HashTable*)malloc(sizeof(HashTable));
    if (table == NULL)
    {
        perror("Falied to allocate memory for table.");
        exit(EXIT_FAILURE);
    }

    table->size = Table_Size;
    table->num_elements = 0;

    table->keys = (char**)calloc(table->size, sizeof(char*)); 
    if (table->keys == NULL)
    {
        perror("Falied to allocate memory for keys.");
        free(table);
        exit(EXIT_FAILURE);
    }

    table->values = (int32_t*)calloc(Table_Size, sizeof(int32_t));
    if (table->values == NULL)
    {
        perror("Falied to allocate memory for values.");
        free(table->keys);
        free(table);
        exit(EXIT_FAILURE);
    }

    return table;
}

int32_t hash(char* key)
{
    int32_t hash = 0;
    for (size_t i = 0; i < strlen(key); ++i)
    {
        hash = (hash + key[i]) % Table_Size;
    }
    return hash;
}

void put(HashTable* table, char* key, int32_t value)
{
    int32_t index = hash(key);

    size_t i;

    for (i = 0; i < table->size; ++i)
    {
        if (table->keys[index] == NULL)
        {
            break;
        }
        // Judge if key and keys[index] is same;
        if (strcmp(key, table->keys[index]) == 0)
        {
            table->values[index] = value;
            return;
        }
        index = (index + 1) % table->size;
    }

    if (i == table->size)
    {
        fprintf(stderr, "Hash Table is full\n");
    }

    table->keys[index] = key;
    table->values[index] = value;
    table->num_elements++;
}

int32_t get(HashTable* table, char* key)
{
    int32_t index = hash(key);
    
    for (size_t i = 0; i < table->size; ++i)
    {
        if (table->keys[index] != NULL && strcmp(key, table->keys[index]) == 0)
        {
            return table->values[index];
        }
        index = (index + 1) % table->size;
    }

    fprintf(stderr, "Key not found: %s\n", key);
    return -1;
}

void remove_key(HashTable* table, char* key)
{
    int32_t index = hash(key);

    for (size_t i = 0; i < table->size; ++i)
    {
        if (table->keys[index] != NULL && strcmp(key, table->keys[index]) == 0)
        {
            table->keys[index] = NULL;
            table->values[index] = 0;
            table->num_elements--;
            return;
        }
        index = (index + 1) % table->size;
    }

    fprintf(stderr, "Key not found: %s\n", key);
}

double load_factor(HashTable* table)
{
    return ((double)table->num_elements / (double) table->size);
}

uint32_t num_elements(HashTable* table)
{
    return table->num_elements;
}
```

# 7-0.Stack堆栈原理的实际用途与时间复杂度分析

![undefined](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/Lifo_stack.svg/1920px-Lifo_stack.svg.png)

## 使用Stack的案例

* 剪切板
* 撤销功能
* 操作系统内存管理
* IDE匹配括号功能

## 复杂度分析

1. push: O(1) T
2. pop: O(1) T
3. peeking at the element on the top of the stack: O(1) T
4. peeking the n element of the stack: O(n) T

**Reference**

* [Time and Space Complexity analysis of Stack operations - GeeksforGeeks](https://www.geeksforgeeks.org/time-and-space-complexity-analysis-of-stack-operations/)

## 基于其他的数据结构实现Stack

* Dynamic array
* Single linked list

使用动态数组可以使用一个uint32_t类型的变量存储Stack的top。

使用单向链表可以在插入数据时从head插入。push pop peek操作均在head处进行，复杂度均为O(1) T。

## C语言实现

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define STACK_SIZE 100

typedef struct Stack
{
    int data[STACK_SIZE];
    int top;
} Stack;

void init_stack(Stack* stack);
bool is_empty(Stack* stack);
bool is_full(Stack* stack);
void push(Stack* stack, int value);
int pop(Stack* stack);
int peek(Stack* stack);

int main(void)
{
    Stack s;
    init_stack(&s);
    
    push(&s, 2);
    push(&s, 6);
    push(&s, 67);

    printf("%d\n", pop(&s));
    printf("%d\n", pop(&s));
    printf("%d\n", pop(&s));
    printf("%d\n", is_empty(&s));

}

void init_stack(Stack* stack)
{
    stack->top = -1;
}

bool is_empty(Stack* stack)
{
    return stack->top == -1;
}

bool is_full(Stack* stack)
{
    return stack->top == STACK_SIZE - 1;
}

void push(Stack* stack, int value)
{
    if (is_full(stack))
    {
        fprintf(stderr, "Error: The stack is full\n");
        return;
    }

    stack->top += 1;
    stack->data[stack->top] = value;
}

int pop(Stack* stack)
{
    if(is_empty(stack))
    {
        fprintf(stderr, "Error: The stack is full\n");
        return -1;
    }

    stack->top -= 1;

    return stack->data[stack->top + 1];
}

int peek(Stack* stack)
{
    if(is_empty(stack))
    {
        fprintf(stderr, "Error: The stack is full\n");
        return -1;
    }
    return stack->data[stack->top];
}
```

# 8-0.Queue原理实际应用与时间复杂度分析

![undefined](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/1920px-Data_Queue.svg.png)

## 使用Queue的案例

* 线程池优先级管理
* 搜索算法：广度优先算法
* 网络编程：缓存网络数据包
* 计算机图形学：三维场景的遮挡剔除

## 复杂度分析

**Reference**

* https://www.geeksforgeeks.org/time-and-space-complexity-analysis-of-queue-operations/



## 基于其他结构实现

* dynamic array
* linked list with tail pointer

## C语言实现

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

typedef struct Node
{
    int value;
    struct Node* next;
} Node;

typedef struct Queue
{
    Node* front;
    Node* rear;
} Queue;

Queue* create_queue(void);
bool is_empty(Queue* queue);
void enQueue(Queue* queue, int value);
int deQueue(Queue* queue);
int peek(Queue* queue);
void print_queue(Queue* queue);

int main(void)
{
    Queue* queue = create_queue();

    printf("If this Queue is empty? %d\n", is_empty(queue));

    enQueue(queue, 2);
    enQueue(queue, 3);
    enQueue(queue, 4);

    printf("The first element in the Queue is %d\n", peek(queue));

    print_queue(queue);

    printf("Dequeue the first element of the Queue is %d\n", deQueue(queue));

    print_queue(queue);


}

Queue* create_queue(void)
{
    Queue* queue = (Queue*)calloc(1, sizeof(Queue));
    if (queue == NULL)
    {
        fprintf(stderr, "Failed to allocate memory for a new queue\n");
        exit(EXIT_FAILURE);
    }

    queue->front = NULL;
    queue->rear = NULL;
    return queue;
}

bool is_empty(Queue* queue)
{
    return ((queue->front == NULL) && (queue->rear == NULL));
}

void enQueue(Queue* queue, int value)
{
    Node* node = (Node*)calloc(1, sizeof(Node));
    if (node == NULL)
    {
        fprintf(stderr, "Failed to allocate memory for a new node\n");
        exit(EXIT_FAILURE);
    }
    node->next = NULL;
    node->value = value;

    if (is_empty(queue))
    {
        queue->front = node;
        queue->rear = node;

        return;
    }

    // if Queue is not empty
    queue->rear->next = node;
    queue->rear = node;
}

int deQueue(Queue* queue)
{
    // if Queue is empty
    if (is_empty(queue))
    {
        fprintf(stderr, "Failed to dequeue in this Queue. Because this Queue is empty\n");
        return -1;
    }

    // if Queue is not empty
    Node* node = queue->front;
    // 保存节点中的数据，未来节点内存将会被释放
    int data = node->value;

    // front后移
    queue->front = queue->front->next;

    // 释放dequeue的节点的内存
    free(node);

    return data;
}

// Function to geek the element in the front
int peek(Queue* queue)
{
    if (is_empty(queue))
    {
        printf("This Queue is empty\n");
        return -1;
    }

    // if Queue is not empty
    return queue->front->value;
}

void print_queue(Queue* queue)
{
    if (is_empty(queue))
    {
        printf("This Queue is empty\n");
        return;
    }

    Node* pointer = queue->front;

    while (pointer != NULL)
    {
        printf("%d ", pointer->value);
        pointer = pointer->next;
    }
    printf("\n");
}
```

# 9-0.Tree 含义以及术语

![Lightbox](https://media.geeksforgeeks.org/wp-content/uploads/20240415185343/tree-data-structure-banners-(2).webp)

![img](https://media.geeksforgeeks.org/wp-content/uploads/20221129094006/Treedatastructure.png)

**Reference**

* [Tree Data Structure - GeeksforGeeks](https://www.geeksforgeeks.org/tree-data-structure/)
* [Applications of tree data structure - GeeksforGeeks](https://www.geeksforgeeks.org/applications-of-tree-data-structure/)

## 树的应用

树常被用在处理层级关系的位置，如：

* 公司职位表
* 操作系统文件存储
* 计算机语言设计，如：html
* 搜索引擎中，树结构可以用来存储网页的结构信息
* IDE中的语法分析，表述语法树
* 决策树：表述决策过程
* 菜单->子菜单->子菜单的子菜单

## 常见的树种类

**基本概念**

* 二叉树：每一个节点最多拥有2个子节点。
* k叉树：每一个节点最多拥有k个子节点

**常见的树的种类**

* **Perfect Binary tree**: A **perfect binary tree** is a special type of binary tree in which all the leaf nodes are at the same depth, and all non-leaf nodes have two children.  ------  https://www.geeksforgeeks.org/perfect-binary-tree/
* **Complete Binary tree**: A **complete binary tree** is a special type of binary tree where all the levels of the tree are filled completely except the lowest level nodes which are filled from as left as possible.  ------  https://www.geeksforgeeks.org/complete-binary-tree/
* **Balanced Binary tree**:  A binary tree is balanced if the height of the tree is O(Log n) where n is the number of nodes.  ------  https://www.geeksforgeeks.org/balanced-binary-tree/ 
  *  A balanced binary tree is a binary tree that follows the 3 conditions:
    * **The height of the left and right tree for any node does not differ by more than 1.**
    * The left subtree of that node is also balanced.
    * The right subtree of that node is also balanced.
* **Binary Search tree**: A **Binary Search Tree** is a data structure used in computer science for organizing and storing data in a sorted manner. Each node in a **Binary Search Tree** has at most two children, a **left** child and a **right** child, with the **left** child containing values less than the parent node and the **right** child containing values greater than the parent node. This hierarchical structure allows for efficient **searching**, **insertion**, and **deletion** operations on the data stored in the tree.  ------  https://www.geeksforgeeks.org/binary-search-tree-data-structure/?ref=shm
* **AVL tree**: AVL tree is a self-balancing Binary Search Tree (**BST**) where the difference between heights of left and right subtrees cannot be more than **one** for all nodes.   ------  https://www.geeksforgeeks.org/insertion-in-an-avl-tree/
* **Full Binary tree**: A binary tree is a tree data structure with a maximum of 2 children per node. We commonly refer to them as the left and right child as each element in a binary tree may only have two children.  -------  https://www.geeksforgeeks.org/full-binary-tree/

一些特殊的树：

* 线段树 区间查询、修改 O(log n)
* 字典树 Trie O(M) M->键的长度

## Tree Traversal Techniques

**Tree Traversal techniques** include various ways to visit all the nodes of the tree. Unlike linear data structures (Array, Linked List, Queues, Stacks, etc) which have only one logical way to traverse them, trees can be traversed in different ways.

![Tree-Traversal-Techniques-(1)](https://media.geeksforgeeks.org/wp-content/uploads/20240429140116/Tree-Traversal-Techniques-(1).webp)

**Reference**

https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/

### Tree Traversal Meaning:

**Tree Traversal** refers to the process of visiting or accessing each node of the tree exactly once in a certain order. Tree traversal algorithms help us to visit and process all the nodes of the tree. Since tree is not a linear data structure, there are multiple nodes which we can visit after visiting a certain node. There are multiple tree traversal techniques which decide the order in which the nodes of the tree are to be visited.

### Tree Traversal Techniques:

![Tree-Traversal-Techniques](https://media.geeksforgeeks.org/wp-content/uploads/20240429124251/Tree-Traversal-Techniques.webp)

A Tree Data Structure can be traversed in following ways:

- Depth First Search or DFS
  - Inorder Traversal
  - Preorder Traversal
  - Postorder Traversal
- Level Order Traversal or Breadth First Search or BFS

### [**Inorder Traversal**](https://www.geeksforgeeks.org/inorder-traversal-of-binary-tree/)

Inorder traversal visits the node in the order: **Left -> Root -> Right**

![Preorder-Traversal-of-Binary-Tree](https://media.geeksforgeeks.org/wp-content/uploads/20240429124538/Preorder-Traversal-of-Binary-Tree.webp)

**Algorithm for Inorder Traversal:**

> Inorder(tree)
>
> - Traverse the left subtree, i.e., call Inorder(left->subtree)
> - Visit the root.
> - Traverse the right subtree, i.e., call Inorder(right->subtree)

**Uses of Inorder Traversal:**

- In the case of binary search trees (BST), Inorder traversal gives nodes in non-decreasing order.
- To get nodes of BST in non-increasing order, a variation of Inorder traversal where Inorder traversal is reversed can be used.
- Inorder traversal can be used to evaluate arithmetic expressions stored in expression trees.

**Time Complexity:** O(N)
**Auxiliary Space:** If we don’t consider the size of the stack for function calls then O(1) otherwise O(h) where h is the height of the tree.

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Function to perform inorder traversal
void inorderTraversal(struct Node* root) {
  
    // Empty Tree
    if (root == NULL)
        return;
  
    // Recur on the left subtree
    inorderTraversal(root->left);
  
    // Visit the current node
    printf("%d ", root->data);
  
    // Recur on the right subtree
    inorderTraversal(root->right);
}

// Function to create a new node
struct Node* newNode(int data) {  
    struct Node* node =
      (struct Node*)malloc(sizeof(struct Node));
  
    node->data = data;
    node->left = NULL;
    node->right = NULL;  
    return node;
}

int main() {
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    printf("Inorder traversal: ");
    inorderTraversal(root);
    printf("\n");
    return 0;
}
```

**Time Complexity:** O(N)
**Auxiliary Space:** If we don’t consider the size of the stack for function calls then O(1) otherwise O(h) where h is the height of the tree.

### [**Preorder Traversal**](https://www.geeksforgeeks.org/preorder-traversal-of-binary-tree/)

Preorder traversal visits the node in the order: **Root -> Left -> Right**

![Inorder-Traversal-of-Binary-Tree](https://media.geeksforgeeks.org/wp-content/uploads/20240429124832/Inorder-Traversal-of-Binary-Tree.webp)

**Algorithm for Preorder Traversal:**

> Preorder(tree)
>
> - Visit the root.
> - Traverse the left subtree, i.e., call Preorder(left->subtree)
> - Traverse the right subtree, i.e., call Preorder(right->subtree)

**Uses of Preorder Traversal:**

- Preorder traversal is used to create a copy of the tree.
- Preorder traversal is also used to get prefix expressions on an expression tree.

**Code Snippet for Preorder Traversal:**

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Function to perform preorder traversal
void preorderTraversal(struct Node* root) {
  
    // Base case
    if (root == NULL)
        return;
  
    // Visit the current node
    printf("%d ", root->data);
  
    // Recur on the left subtree
    preorderTraversal(root->left);
  
    // Recur on the right subtree
    preorderTraversal(root->right);
}

struct Node* newNode(int data) {
    struct Node* node = 
      (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return node;
}

int main() {
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    preorderTraversal(root);
    return 0;
}
```

**Time Complexity:** O(N)
**Auxiliary Space:** If we don’t consider the size of the stack for function calls then O(1) otherwise O(h) where h is the height of the tree.

### [**Postorder Traversal**](https://www.geeksforgeeks.org/postorder-traversal-of-binary-tree/)

Postorder traversal visits the node in the order: **Left -> Right -> Root**

![Postorder-Traversal-of-Binary-Tree](https://media.geeksforgeeks.org/wp-content/uploads/20240429125100/Postorder-Traversal-of-Binary-Tree.webp)

**Algorithm for Postorder Traversal:**

> Algorithm Postorder(tree)
>
> - Traverse the left subtree, i.e., call Postorder(left->subtree)
> - Traverse the right subtree, i.e., call Postorder(right->subtree)
> - Visit the root

**Uses of Postorder Traversal:**

- Postorder traversal is used to delete the tree. See [the question for the deletion of a tree ](https://www.geeksforgeeks.org/write-a-c-program-to-delete-a-tree/)for details.
- Postorder traversal is also useful to get the postfix expression of an expression tree.
- Postorder traversal can help in garbage collection algorithms, particularly in systems where manual memory management is used.

**Code Snippet for Postorder Traversal:**

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Function to perform postorder traversal
void postorderTraversal(struct Node* node) {
  
    // Base case
    if (node == NULL)
        return;
  
    // Recur on the left subtree
    postorderTraversal(node->left);
  
    // Recur on the right subtree
    postorderTraversal(node->right);
  
    // Visit the current node
    printf("%d ", node->data);
}

struct Node* newNode(int data) {
    struct Node* node = 
      (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return node;
}

int main() {
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    postorderTraversal(root);
    return 0;
}
```

### Problem of common Depth First Search implemention

The common Depth Fisrt Search funtions are implemented recursively. In some condition, we don't want to use recursion in function. Recursion will occpy more stack in computer system, which will lead to stack overflow.

So how can we implement DFS without recursion?

**Reference**

* https://codingots.medium.com/tree-traversal-without-recursion-221cbea6d004
* https://prepinsta.com/data-structures/preorder-tree-traversal-without-recursion/

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

typedef struct TreeNode
{
    int value;
    struct TreeNode *left;
    struct TreeNode *right;
} TreeNode;

typedef struct StackNode
{
    TreeNode *tree_node;
    struct StackNode *next;
} StackNode;

typedef struct QueueNode
{
    TreeNode *tree_node;
    struct QueueNode *next;
} QueueNode;

typedef struct Queue
{
    QueueNode *front;
    QueueNode *rear;
} Queue;

// Declarations of stack functions
bool isEmpty(StackNode *top);
void push(StackNode **top, TreeNode *tree_node);
TreeNode *pop(StackNode **top);
TreeNode *peek(StackNode *top);

// Declarations of queue functions
void enQueue(Queue *queue, TreeNode *tree_node);
TreeNode *deQueue(Queue *queue);
bool isQEmpty(Queue *queue);

// Declarations of tree functions

/**
 * Function to create a binary tree node by a integer data
 * 
 * Parameters:
 * - data: The data stored in this tree node.
 * 
 * Returns:
 * - A TreeNode which stores the input data.
 * 
 * Note:
 * - Please guard against memory application failure because of using malloc() function.
 */
TreeNode *createNode(int data)
{
    TreeNode *node = (TreeNode *)malloc(sizeof(TreeNode));

    if (node == NULL)
    {
        fprintf(stderr, "Failedto allocate memory for a new TreeNode.\n");
    }

    node->value = data;
    node->left = NULL;
    node->right = NULL;
}

/**
 * Function to create a perfect binary tree by a ordered array.
 *
 * Parameters:
 * - array: The ordered array stored elements for creating the tree.
 * - start: The first element's index.
 * - end: The last element's index.
 *
 * Returns:
 * - The perfect binary tree.
 *
 * Notes:
 * - The function only accept an ordered array, when you want the tree ordered.
 * - The 'start' should be smaller than the 'end'.
 */
TreeNode *createPerfectBinaryTree(int *array, int start, int end)
{
    // when the start is bigger than end, something wrong happened.
    if (start > end)
    {
        return NULL;
    }

    int mid = (start + end) / 2;
    TreeNode *node = createNode(array[mid]);
    node->left = createPerfectBinaryTree(array, start, mid - 1);
    node->right = createPerfectBinaryTree(array, mid + 1, end);

    return node;
}

/**
 * pre oreder traversal a binary tree by recursion.
 *
 * Parameters:
 * - root: The root node of the tree.
 *
 * Returns:
 * - No returns.
 *
 * Notes:
 * - This function is implemented recursively, which may refer to stack overflow.
 */
void preOrderTraversal(TreeNode *root)
{
    if (root == NULL)
    {
        return;
    }
    printf("%d ", root->value);
    preOrderTraversal(root->left);
    preOrderTraversal(root->right);
}

/**
 * pre oreder traversal a binary tree by using stack data strcuture.
 *
 * Parameters:
 * - root: The root node of the tree.
 *
 * Returns:
 * - No returns.
 *
 * Notes:
 * This function is implemented by using stack data strcuture to replace recursion.
 */
void preOrderTraversalStack(TreeNode *root)
{
    if (root == NULL)
    {
        printf("There is nothing in this tree.\n");
        return;
    }

    TreeNode *current = root;
    StackNode *stack = NULL;
    bool is_not_over = true;
    while (is_not_over)
    {
        if (current != NULL)
        {
            printf("%d ", current->value);
            push(&stack, current);
            current = current->left;
        }
        else
        {
            if (!isEmpty(stack))
            {
                current = pop(&stack);
                current = current->right;
            }
            else
            {
                is_not_over = false;
            }
        }
    }
    printf("\n");
}

void inOrderTraversal(TreeNode *root)
{
    if (root == NULL)
    {
        return;
    }

    // Recur on the left subtree
    inOrderTraversal(root->left);

    // Visit the current node
    printf("%d ", root->value);

    // Recur on the right subtree
    inOrderTraversal(root->right);
}

void inOrderTraversalStack(TreeNode* root)
{
    if (root == NULL)
    {
        printf("There is nothing in this tree.\n");
        return;
    }

    TreeNode* current = root;
    StackNode* stack = NULL;
    bool is_not_over = true;
    while (is_not_over)
    {
        if (current != NULL)
        {
            push(&stack, current);
            current = current->left;
        }
        else
        {
            if (!isEmpty(stack))
            {
                current = pop(&stack);
                printf("%d ", current->value);
                current = current->right;
            }
            else
            {
                is_not_over = false;
            }
        }
    }
    printf("\n");
}

void postOrderTraversal(TreeNode *root)
{
    if (root == NULL)
    {
        return;
    }

    // Recur on the left subtree
    postOrderTraversal(root->left);

    // Recur on the right subtree
    postOrderTraversal(root->right);

    // Visit the current node
    printf("%d ", root->value);
}

// TODO
// void postOrderTraversalStack(TreeNode* root)
// {
//     if (root == NULL)
//     {
//         return;
//     }

//     TreeNode* current = root;
//     StackNode* stack = NULL;
//     bool is_not_over = true;
//     while(is_not_over)
//     {
//         if (current != NULL)
//         {
//             if (current->right != NULL)
//             {
//                 push(&stack, current->right);
//             }
//             push(&stack, current);
//             current = current->left;
//         }
        
//         current = pop(&stack);
//         if (current->right == peek(stack))
//         {
//             pop(&stack);
//             push(&stack, current);
//             current = current->right;
//         }
//         else
//         {
//             printf("%d ", current->value);
//         }
//         if (!isEmpty(stack))
//         {
//             is_not_over == false;
//         }
//     }
//     printf("\n");
// }

void postOrderIterative(TreeNode* root)
{
    // Check for empty tree
    if (root == NULL)
        return;

    StackNode* stack = NULL;
    do {
        // Move to leftmost node
        while (root) {
            // Push root's right child and then root to
            // stack.
            if (root->right)
                push(&stack, root->right);
            push(&stack, root);

            // Set root as root's left child
            root = root->left;
        }

        // Pop an item from stack and set it as root
        root = pop(&stack);

        // If the popped item has a right child and the
        // right child is not processed yet, then make sure
        // right child is processed before root
        if (root->right && peek(stack) == root->right) {
            pop(&stack); // remove right child from stack
            push(&stack, root); // push root back to stack
            root = root->right; // change root so that the
                                // right child is processed
                                // next
        }
        else // Else print root's data and set root as NULL
        {
            printf("%d ", root->value);
            root = NULL;
        }
    } while (!isEmpty(stack));
}

void levelOrderTraversal(TreeNode *root)
{
    if (root == NULL)
    {
        return;
    }
    Queue *queue = (Queue *)malloc(sizeof(Queue));
    queue->front = NULL;
    queue->rear = NULL;

    enQueue(queue, root);

    TreeNode* temp;
    while (!isQEmpty(queue))
    {
        temp = deQueue(queue);
        printf("%d ", temp->value);
        if (temp->left != NULL)
        {
            enQueue(queue, temp->left);
        }
        if (temp->right != NULL)
        {
            enQueue(queue, temp->right);
        }
    }
    printf("\n");

    free(queue);
}

int main(void)
{
    int array[] = {1, 2, 3, 4, 5, 6, 7, 8};

    TreeNode *tree = createPerfectBinaryTree(array, 0, 7);

    preOrderTraversal(tree);
    printf("\n");

    preOrderTraversalStack(tree);

    levelOrderTraversal(tree);

    inOrderTraversal(tree);
    printf("\n");

    inOrderTraversalStack(tree);

    postOrderTraversal(tree);
    printf("\n");

    postOrderIterative(tree);
    
    // postOrderTraversalStack(tree);
}

bool isEmpty(StackNode *top)
{
    if (top == NULL)
    {
        return true;
    }
    else
    {
        return false;
    }
}

void push(StackNode **top, TreeNode *tree_node)
{
    StackNode *node = (StackNode *)malloc(sizeof(StackNode));
    node->tree_node = tree_node;
    node->next = *top;
    *top = node;
}

TreeNode *pop(StackNode **top)
{
    if (isEmpty(*top))
    {
        return NULL;
    }
    StackNode *pop_node = *top;
    TreeNode *return_tree_node = pop_node->tree_node;
    *top = pop_node->next;
    free(pop_node);
    return return_tree_node;
}

TreeNode *peek(StackNode *top)
{
    if (isEmpty(top))
    {
        return NULL;
    }
    return top->tree_node;
}

void enQueue(Queue *queue, TreeNode *tree_node)
{
    QueueNode *queue_node = (QueueNode *)malloc(sizeof(QueueNode));
    queue_node->tree_node = tree_node;
    queue_node->next = NULL;
    
    if (isQEmpty(queue))
    {
        queue->front = queue_node;
        queue->rear = queue_node;
        return;
    }

    queue->rear->next = queue_node;
    queue->rear = queue_node;
}

TreeNode *deQueue(Queue *queue)
{
    if (isQEmpty(queue))
    {
        return NULL;
    }

    QueueNode *queue_node_to_free = queue->front;
    TreeNode *return_tree_node = queue_node_to_free->tree_node;
    queue->front = queue_node_to_free->next;
    if (queue->front == NULL)
    {
        queue->rear = NULL;
    }
    free(queue_node_to_free);
    return return_tree_node;
}

bool isQEmpty(Queue *queue)
{
    return ((queue->front == NULL) && (queue->rear == NULL));
}
```



### 关于使用栈实现的深度搜索算法的一些思考

前序搜索

* 输出本节点
* 将本节点push进栈
* 跳转至左节点作为本节点
  * 如果没有左节点，则pop栈中节点（即为本节点的parent），parent的右节点作为本节点
  * 如果右节点也没有，则pop栈中的节点（即为本节点的parent的parent）进入parent的parent的右节点

中序搜索

* 将本节点push进栈
* 跳转至本节点的左节点作为本节点
  * 如果没有左节点，则pop栈中节点（即为本节点的parent）输出parent，parent的右节点作为本节点
  * 如果右节点也没有，则pop栈中的节点（即为本节点的parent的parent），输出parent的parent，进入parent的parent的右节点

后序搜索

* 将本节点push进栈
* 将本节点的右节点push进栈
* 跳转至本节点的左节点作为本节点
  * 如果没有左节点，则pop栈中的节点（本节点的右节点）作为本节点
  * 如果右节点也没有，则pop栈中的节点（本节点），输出本节点

注：由于本节点和本节点的右节点都从栈中pop出，那么如何区分呢？

答：先push本节点的右节点，再push本节点。如果pop后，pop出的节点的右节点与栈顶节点相同，则为本节点。此时应pop处栈顶的右节点，并将本节点重新push进栈。

注：按照上面的方法，在栈顶时，pop出的节点的右节点为NULL，此时栈顶也为NULL，则会将本节点重新放入栈进行无限输出，如何解决？



思考：其实前序搜索中，栈中存放的并不是本节点，而是本节点的右节点，因为能通过本节点找到右节点，故push本节点。重要的是将需要输出的节点按照想要的顺序放进栈中，依次输出。

### [Level Order Traversal ](https://www.geeksforgeeks.org/level-order-tree-traversal/)

**Level Order Traversal** visits all nodes present in the same level completely before visiting the next level.

![Level-Order-Traversal-of-Binary-Tree](https://media.geeksforgeeks.org/wp-content/uploads/20240429134701/Level-Order-Traversal-of-Binary-Tree.webp)

**Algorithm for Level Order Traversal**

> LevelOrder(tree)
>
> - Create an empty queue Q
> - Enqueue the root node of the tree to Q
> - Loop while Q is not empty
>   - Dequeue a node from Q and visit it
>   - Enqueue the left child of the dequeued node if it exists
>   - Enqueue the right child of the dequeued node if it exists

**Uses of Level Order:**

- Level Order Traversal is mainly used as Breadth First Search to search or process nodes level-by-level.
- Level Order traversal is also used for [Tree Serialization and Deserialization ](https://www.geeksforgeeks.org/serialize-deserialize-binary-tree/).