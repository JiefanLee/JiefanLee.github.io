---
layout: post
title:  "Quick Sort"
date:   2018-05-04 09:32:00
categories: algorithm sort
tags: algorithm sort
author: JiefanLee
---
* content
{:toc}

## Quick Sort Idea

快速排序是典型的分治思想算法。每一遍排序都从序列中取一个值，以此值为key分区，分区后使这个值左边的数都小于等于这个值，右边的都大于等于这个值，这样把整个序列分为两部分，再对这两部分分别递归执行上述操作。







```
该方法的基本思想是：
1．先从数列中取出一个数作为key。
2．分区过程，将比这个数大的数全放到它的右边，小于或等于它的数全放到它的左边。
3．再对左右区间重复第二步，直到各区间只有一个数。
```



```cpp
class Solution{  
public:  
    void QuickSort(vector<int> &v, int begin, int end){  
        if (begin < end){  
            int mid = Partition(v, begin, end);  
            QuickSort(v, begin, mid - 1);  
            QuickSort(v, mid + 1, end);  
        }
    }  
    int Partition(vector<int> &v, int begin, int end){  
        int key = v[begin];  
        int i = begin, j = begin + 1;  
        while (j <= end && i < end){  
            if (v[j] < key){  
                Exchange(v[j], v[++i]);  
            }  
            j++;  
        }  
        if (i != end && i != begin)  
            Exchange(v[begin], v[++i]);  
        else if (i == end)  
                Exchange(v[begin], v[i]);  
        return i;  
    }  
    void Exchange(int &a, int &b){  
        int tmp = a;  
        a = b;  
        b = tmp;  
    }  
};

```
