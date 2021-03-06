---
layout:     post
title:      Data Structure in Python
subtitle:   Review the book <Problem Solving with Algorithms and Data Structures using Python>
date:       2018-09-10
author:     Hongyi
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Python
    - Algorithm
    - Data Structure
---

# Basic Data Structure
## What is Stack?
A **stack** (sometimes called a “push-down stack”) is an ordered collection of items where the addition of new items and the removal of existing items always takes place at the same end. This end is commonly referred to as the “top.” The end opposite the top is known as the “base.”

This ordering principle is sometimes called **LIFO, last-in first-out**. It provides an ordering based on length of time in the collection. Newer items are near the top, while older items are near the base.

![](http://interactivepython.org/courselib/static/pythonds/_images/simplereversal.png)

For example, every web browser has a Back button. As you navigate from web page to web page, those pages are placed on a stack (actually it is the URLs that are going on the stack). The current page that you are viewing is on the top and the first page you looked at is at the base. If you click on the Back button, you begin to move in reverse order through the pages.

**The Stack Abstract Data Type**

Stacks are ordered LIFO. The stack operations are given below.
* Stack() creates a new stack that is empty. It needs no parameters and returns an empty stack.
* push(item) adds a new item to the top of the stack. It needs the item and returns nothing.
* pop() **removes** the top item from the stack. It needs no parameters and returns the item. The stack is modified.
* peek() returns the top item from the stack but **does not remove** it. It needs no parameters. The stack is not modified.
* isEmpty() tests to see whether the stack is empty. It needs no parameters and returns a boolean value.
* size() returns the number of items on the stack. It needs no parameters and returns an integer.

For example, if **s** is a stack that has been created and starts out empty, then Table below shows the results of a sequence of stack operations.

| **Stack Operation** | **Stack Contents** | **Return Value** |
|:--------------------|:-------------------|:-----------------|
| s.isEmpty()         |	[]	               | True             |
| s.push(4)	          | [4]	               |                  |
| s.push('dog')	      | [4,'dog']          |                  |	 
| s.peek()	          | [4,'dog']	       | 'dog'            |
| s.push(True)	      | [4,'dog',True]     |                  |	 
| s.size()	          | [4,'dog',True]	   | 3                |
| s.isEmpty()	      | [4,'dog',True]	   | False            |
| s.push(8.4)	      | [4,'dog',True,8.4] |                  | 	 
| s.pop()	          | [4,'dog',True]	   | 8.4              |
| s.pop()	          | [4,'dog']	       | True             |
| s.size()	          | [4,'dog']	       | 2                |

**Implementing a Stack in Python**

The following stack implementation assumes that the end of the list will hold the top element of the stack. As the stack grows (as push operations occur), new items will be added on the end of the list. pop operations will manipulate that same end.

```
class Stack:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop()

    def peek(self):
        return self.items[-1]

    def size(self):
        return len(self.items)

if __name__=="__main__":
    s = Stack()
    print(s.isEmpty())
    s.push(4)
    print(s.items)
    s.push('dog')
    print(s.items)
    print(s.peek(), s.items)
    s.push(True)
    print(s.size())
    print(s.isEmpty())
    s.push(8.4)
    print(s.items)
    print(s.pop())
    print(s.pop())
    print(s.size())
```

**Converting Decimal Numbers to Binary Numbers**

![](http://interactivepython.org/courselib/static/pythonds/_images/dectobin.png)

**Stack is a good data structure to handle this problem.**

```
def DecToBin(decNumber):
    stack = []
    while decNumber > 0:
        rem = decNumber % 2
        stack.append(rem)
        decNumber = decNumber // 2

    binString = ""
    while len(stack) != 0:
        binString += str(stack.pop())

    return binString

def BinToDec(binNumber):
    bin_string = str(binNumber)
    dec_number = 0
    index = 0
    for char in bin_string:
        dec_number += int(char) * pow(2, len(bin_string) - 1 - index)
        index += 1

    return dec_number
print(DecToBin(42))
print(BinToDec(101010))
-----------------------------
101010
42
```

## What is Queue?
A queue is an ordered collection of items where the addition of new items happens at one end, called the “rear,” and the removal of existing items occurs at the other end, commonly called the “front.” As an element enters the queue it starts at the rear and makes its way toward the front, waiting until that time when it is the next element to be removed.

The most recently added item in the queue must wait at the end of the collection. The item that has been in the collection the longest is at the front. This ordering principle is sometimes called **FIFO, first-in first-out**. It is also known as “first-come first-served.”

![](http://interactivepython.org/courselib/static/pythonds/_images/basicqueue.png)

**The Queue Abstract Data Type**

The queue operations are given below. 
* Queue() creates a new queue that is empty. It needs no parameters and returns an empty queue.
* enqueue(item) adds a new item to the rear of the queue. It needs the item and returns nothing.
* dequeue() removes the front item from the queue. It needs no parameters and returns the item. The queue is modified.
* isEmpty() tests to see whether the queue is empty. It needs no parameters and returns a boolean value.
* size() returns the number of items in the queue. It needs no parameters and returns an integer.

As an example, if we assume that q is a queue that has been created and is currently empty, then Table below shows the results of a sequence of queue operations. 

| **Queue Operation** | **Queue Contents** | **Return Value** |
|:--------------------|:-------------------|:-----------------|
| q.isEmpty()	      | []	               | True             |
| q.enqueue(4)	      | [4]                |                  |	 
| q.enqueue('dog')	  | ['dog',4]          |                  |	 
| q.enqueue(True)	  | [True,'dog',4]	   |                  |
| q.size()	          | [True,'dog',4]	   | 3                |
| q.isEmpty()	      | [True,'dog',4]	   | False            |
| q.enqueue(8.4)	  | [8.4,True,'dog',4] |                  |	 
| q.dequeue()	      | [8.4,True,'dog']   | 4                |
| q.dequeue()	      | [8.4,True]	       | 'dog'            |
| q.size()	          | [8.4,True]	       | 2                |

```
class Queue:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def enqueue(self, item):
        self.items.insert(0, item)

    def dequeue(self):
        return self.items.pop()

    def size(self):
        return len(self.items)
```

**Hot Potato Game**

One of the typical applications for showing a queue in action is to simulate a real situation that requires data to be managed in a FIFO manner. To begin, let’s consider the children’s game Hot Potato. In this game (see Figure) children line up in a circle and pass an item from neighbor to neighbor as fast as they can. At a certain point in the game, the action is stopped and the child who has the item (the potato) is removed from the circle. Play continues until only one child is left.

![](http://interactivepython.org/courselib/static/pythonds/_images/hotpotato.png)

To simulate the circle, we will use a queue (see Figure below). Assume that the child holding the potato will be at the front of the queue. Upon passing the potato, the simulation will simply dequeue and then immediately enqueue that child, putting her at the end of the line. She will then wait until all the others have been at the front before it will be her turn again. 
After num dequeue/enqueue operations, the child at the front will be removed permanently and another cycle will begin. This process will continue until only one name remains (the size of the queue is 1).

![](http://interactivepython.org/courselib/static/pythonds/_images/namequeue.png)

```
def hotPotato(name_list, num):
    queue = Queue()
    for name in name_list:
        queue.enqueue(name)

    while queue.size() > 1:
        for i in range(num):
            circle_name = queue.dequeue()
            queue.enqueue(circle_name)

        # delet the name
        queue.dequeue()

    return queue.dequeue()

print(hotPotato(["Bill","David","Susan","Jane","Kent","Brad"],7))
------------------------------------------------------------------
Susan
```


## What is Deque?


## What is List?

# Recrsion
