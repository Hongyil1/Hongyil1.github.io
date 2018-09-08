---
layout:     post
title:      Algorithms in Python
subtitle:   Review the book <Problem Solving with Algorithms and Data Structures using Python>
date:       2018-09-08
author:     Hongyi
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Python
    - Algorithm
    - Data Structure
---

# Sorting and Searching
## Searching
### The Sequential Search
The following image shows the process of sequential search:

![seqsearch](https://user-images.githubusercontent.com/22671087/45251424-3839be80-b389-11e8-8fe9-fc54183b19c0.png)

```
def seqSearch(alist, item):
    found = False
    for num in alist:
        if num == item:
            found = True
    return found

if __name__=="__main__":
    testlist = [1, 2, 32, 8, 17, 19, 42, 13, 0]
    print(seqSearch(testlist, 3))
    print(seqSearch(testlist, 13))
-----------------------------------
False
True
```

**Analysis of Sequential Search**

For searching, it makes sense to count the number of comparisons performed. The time complexity is **O(n)**.

| **Case** | **Best Case** | **Worst Case** | **Average Case** |
|:--------|:-------------|:--------------|:----------------|
| item is present| 1 | n | n/2 |
| item is not present | n | n | n |

**Sorting** the list before doing the seach will increase the efficiency. However, this technique is still **O(n)**.

### The Binary Search
In a ordered list, the binary search will work better than sequential search. 

A binary search will start by examining the middle item. If that item is the one we are searching for, we are done. If it is not the correct item, we can use the ordered nature of the list to eliminate half of the remaining items. If the item we are searching for is greater than the middle item, we know that the entire lower half of the list as well as the middle item can be eliminated from further consideration. The item, if it is in the list, must be in the upper half.

![binsearch](https://user-images.githubusercontent.com/22671087/45251561-8ea7fc80-b38b-11e8-8d77-f0fefcff6bfa.png)

```
def binSearch(alist, item):
    first = 0
    last = len(alist) -1
    found = False
    
    # not found is used to break the loop.
    while first<=last and not found:
        mid_point = (first + last) // 2
        if alist[mid_point] == item:
            found = True
        else:
            if alist[mid_point] > item:
                last = mid_point -1
            else:
                first = mid_point + 1
    return found

if __name__=="__main__":
    testlist = [0, 1, 2, 8, 13, 17, 19, 32, 42, ]
    print(binSearch(testlist, 3))
    print(binSearch(testlist, 13))
------------------------------------------
False
True
```

**A Recursive method**

```
def binSearch(alist, item):
    if len(alist) == 0:
        return False
    else:
        mid_point = len(alist) // 2
        if alist[mid_point] == item:
            return True
        else:
            if alist[mid_point] > item:
                return binSearch(alist[:mid_point], item)
            else:
                return binSearch(alist[mid_point+1:], item)

if __name__=="__main__":
    testlist = [0, 1, 2, 8, 13, 17, 19, 32, 42, ]
    print(binSearch(testlist, 3))
    print(binSearch(testlist, 13))
-----------------------------------------------------
False
True
```

**Analysis of Binary Search**

If we start with n items, about n/2 items will be left after the first comparison. After the second comparison, there will be about n/4. Then n/8, n/16, and so on. When we split the list enough times, we end up with a list that has just one item. Either that is the item we are looking for or it is not. Either way, we are done. The number of comparisons necessary to get to this point is i where **n/2^i=1**. Solving for i gives us i=log(n). Therefore, the binary search is **O(log(n))**

| Number of comparison | Number of resting items |
|:---------------------|:------------------------|
| 1                    | n/2                     |
| 2                    | n/4                     |
| 3                    | n/8                     |
| ...                  | ...                     |
| i                    | n/2^i                   |

Even though a binary search is generally better than a sequential search, it is important to note that for small values of n, the additional cost of sorting is probably not worth it. If we can sort once and then search many times, the cost of the sort is not so significant. However, for large lists, sorting even once can be so expensive that simply performing a sequential search from the start may be the best choice.

### Hashing
In this section we will attempt to go one step further by building a data structure that can be searched in **O(1)** time. This concept is referred to as **hashing**.

A **hash table** is a collection of items which are stored in such a way as to make it easy to find them later. Each position of the hash table, often called a **slot**, can hold an item and is named by an integer value starting at 0. For example, we will have a slot named 0, a slot named 1, a slot named 2, and so on. Initially, the hash table contains no items so every slot is empty. We can implement a hash table by using a list with each element initialized to the special Python value None. 

![hashtable](https://user-images.githubusercontent.com/22671087/45253022-5f9d8500-b3a3-11e8-979f-5824c9b8c48e.png)

The mapping between an item and the slot where that item belongs in the hash table is called the **hash function**. The hash function will take any item in the collection and return an integer in the range of slot names, between 0 and m-1. Assume that we have the set of integer items 54, 26, 93, 17, 77, and 31. Our first hash function, sometimes referred to as the *“remainder method,”* simply takes an item and divides it by the table size, returning the remainder as its hash value (h(item)=item%11). Note that this remainder method (modulo arithmetic) will typically be present in some form in all hash functions, since the result must be in the range of slot names.

| Item  | Hash Value    |
|:------|:--------------|
| 54    | 10            |
| 26    | 4             |
| 93    | 5             |
| 17    | 6             |
| 77    | 0             |
| 31    | 9             |

![hashtable2](https://user-images.githubusercontent.com/22671087/45253271-eb191500-b3a7-11e8-9a36-a546baec3757.png)

Now when we want to search for an item, we simply use the hash function to compute the slot name for the item and then check the hash table to see if it is present. This searching operation is **O(1)**, since a constant amount of time is required to compute the hash value and then index the hash table at that location. 

According to the hash function, two or more items would need to be in the same slot. This is referred to as a **collision** (it may also be called a “clash”). Clearly, collisions create a problem for the hashing technique. We will discuss them in detail later.

**Hash Functions**

Given a collection of items, a hash function that maps each item into a unique slot is referred to as a **perfect hash function**.

One way to always have a perfect hash function is to increase the size of the hash table so that each possible value in the item range can be accommodated. However, it's not practical for large numbers of items.

One way to always have a perfect hash function is to increase the size of the hash table so that each possible value in the item range can be accommodated. 

1. **Folding Method**

The **folding method** for constructing hash functions begins by dividing the item into equal-size pieces (the last piece may not be of equal size). These pieces are then added together to give the resulting hash value. For example, if our item was the phone number 436-555-4601, we would take the digits and divide them into groups of 2 (43,65,55,46,01). After the addition, 43+65+55+46+01, we get 210. If we assume our hash table has 11 slots, then we need to perform the extra step of dividing by 11 and keeping the remainder. In this case 210 % 11 is 1, so the phone number 436-555-4601 hashes to slot 1. Some folding methods go one step further and **reverse** every other piece before the addition. For the above example, we get 43+56+55+64+01=219 which gives 219 % 11=10.

2. **mid-square method**

We first square the item, and then extract some portion of the resulting digits. For example, if the item were 44, we would first compute 44^2=1936. By extracting the middle two digits, 93, and performing the remainder step, we get 5 (93 % 11).

| Item  | square    | Mid-Square    |
|:------|:----------|:--------------|
| 54    | 2916      | 91 % 11 = 3   |
| 26    | 676       | 7 % 11 = 7    |
| 93    | 8649      | 64 % 11 = 9   |
| 17    | 289       | 8 % 11 = 8    |

We can also create hash functions for character-based items such as strings. The word “cat” can be thought of as a sequence of ordinal values.

```
>>> ord('c')
99
>>> ord('a')
97
>>> ord('t')
116
```

**Collision Resolution**

We now return to the problem of collisions. When two items hash to the same slot, we must have a systematic method for placing the second item in the hash table. This process is called **collision resolution**.

One method for resolving collisions looks into the hash table and tries to find another open slot to hold the item that caused the collision. A simple way to do this is to start at the original hash value position and then move in a sequential manner through the slots until we encounter the first slot that is empty. Note that we may need to go back to the first slot (circularly) to cover the entire hash table. This collision resolution process is referred to as **open addressing** in that it tries to find the next open slot or address in the hash table. By systematically visiting each slot one at a time, we are performing an open addressing technique called **linear probing**.

![linearprobing1](https://user-images.githubusercontent.com/22671087/45253524-2b7a9200-b3ac-11e8-895a-18863edaba6c.png)

When we attempt to place 44 into slot 0, a collision occurs. Under linear probing, we look sequentially, slot by slot, until we find an open position. In this case, we find slot 1. Again, 55 should go in slot 0 but must be placed in slot 2 since it is the next open position. The final value of 20 hashes to slot 9. Since slot 9 is full, we begin to do linear probing. We visit slots 10, 0, 1, and 2, and finally find an empty slot at position 3.

**To search** the hash table. Assume we want to look up the item 93. When we compute the hash value, we get 5. Looking in slot 5 reveals 93, and we can return True. What if we are looking for 20? Now the hash value is 9, and slot 9 is currently holding 31. We cannot simply return False since we know that there could have been collisions. We are now forced to do a sequential search, starting at position 10, looking until either we find the item 20 or we find an empty slot.  

A disadvantage to linear probing is the tendency for **clustering**; items become clustered in the table. This means that if many collisions occur at the same hash value, a number of surrounding slots will be filled by the linear probing resolution. 

**Skip Slots**. One way to deal with clustering is to extend the linear probing technique so that instead of looking sequentially for the next open slot, we skip slots, thereby more evenly distributing the items that have caused collisions.

An alternative method for handling the collision problem is to allow each slot to hold a reference to a collection (or chain) of items. **Chaining** allows many items to exist at the same location in the hash table. When collisions happen, the item is still placed in the proper slot of the hash table. As more and more items hash to the same location, the difficulty of searching for the item in the collection increases. 

![chaining](https://user-images.githubusercontent.com/22671087/45254118-c035bd80-b3b5-11e8-8d08-7c4bd73f1a18.png)

When we want to search for an item, we use the hash function to generate the slot where it should reside. Since each slot holds a collection, we use a searching technique to decide whether the item is present. The **advantage** is that on the average there are likely to be many fewer items in each slot, so the search is perhaps more efficient. 

### The Map Abstract Data Type
The map abstract data type is defined as follows. The structure is an unordered collection of associations between a key and a data value. The keys in a map are all unique so that there is a one-to-one relationship between a key and a value. The operations are given below.

* Map() Create a new, empty map. It returns an empty map collection.
* put(key, val) Add a new key-value pair to the map. If the key is already in the map then replace the old value with the new value.
* get(key) Given a key, return the value stored in the map or None otherwise.
* del Delete the key-value pair from the map using a statement of the form del map[key].
* len() Return the number of key-value pairs stored in the map.
* in Return True for a statement of the form key in map, if the given key is in the map, False otherwise.




## Sorting
### The Bubble Sort

### The Selection Sort

### The insertion Sort

### The Shell Sort

### The Merge Sort

### The Quick Sort
