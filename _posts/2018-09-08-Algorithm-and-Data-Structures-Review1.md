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

Even though a binary search is generally better than a sequential search, it is important to note that for small values of n, the additional cost of sorting is probably not worth it. If we can sort once and then search many times, the cost of the sort is not so significant. However, for large lists, sorting even once can be so expensive that simply performing a sequential search from the start may be the best choice.

### Hashing

## Sorting
### The Bubble Sort

### The Selection Sort

### The insertion Sort

### The Shell Sort

### The Merge Sort

### The Quick Sort
