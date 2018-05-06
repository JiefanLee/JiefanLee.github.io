---
layout: post
title:  "Search a 2D Matrix-Binary Search"
date:   2018-05-06 18:52:00
categories: algorithm Binary
tags: algorithm Binary
author: JiefanLee
---
* content
{:toc}

## Search a 2D Matrix









```
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
```
```
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
Output: true
```

## Solution 1

We can get the number of the row that the target may be in, and then search in that row.

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int row=matrix.size();
        if(!row)
            return false;
        int col=matrix[0].size(),i;
        if(!col)
            return false;
        for(i=0;i<row;++i)
            if(matrix[i][0]<=target&&matrix[i][col-1]>=target)
                break;
        if(i==row)
            return false;
        else
        {
            for(int j=0;j<col;++j)
                if(matrix[i][j]==target)
                    return true;
        }
        return false;
    }

};
```

## Solution 2-Binary Search

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m=matrix.size();
        if(m==0)
            return false;
        int n=matrix[0].size();
        if(n==0)
            return false;
        return binarySearch(matrix,0,m*n-1,target,n);
    }
private:
    bool binarySearch(vector<vector<int>>& matrix,int l,int r,int target,int n)
    {
        if(l>=r&&matrix[l/n][l%n]!=target)
            return false;
        int mid=(l+r)/2;
        if(target>matrix[mid/n][mid%n])
            return binarySearch(matrix,mid+1,r,target,n);
        else if(target<matrix[mid/n][mid%n])
            return binarySearch(matrix,l,mid-1,target,n);
        else
            return true;
    }
};
```
