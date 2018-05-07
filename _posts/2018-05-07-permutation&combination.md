---
layout: post
title:  "Permutation & Combination"
date:   2018-05-06 16:44:00
categories: algorithm recursion LeetCode
tags: algorithm recursion LeetCode
author: JiefanLee
---
* content
{:toc}

## Permutation













```
The set [1,2,3,...,n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for n = 3:

"123"
"132"
"213"
"231"
"312"
"321"
Given n and k, return the kth permutation sequence.

Note:

Given n will be between 1 and 9 inclusive.
Given k will be between 1 and n! inclusive.
```

```cpp
public:
    string getPermutation(int n, int k) {
        vector<vector<int>> all;
        vector<int> one;
        vector<int> set;
        for(int i=1;i<=n;i++)
            set.push_back(i);
        dfs(set,all,0);
        sort(all.begin(),all.end());
        string str="";
        for(int i=0;i<n;i++)
        {
            str+=char(all[k-1][i]+48);
        }
        return str;
    }
private:
    void dfs(vector<int>& nums,vector<vector<int>>& result,int cur)
    {
        if(cur==nums.size())
        {
            result.push_back(nums);
            return;
        }
        for (int i = cur; i < nums.size(); i++) {
		    swap(nums[cur], nums[i]);
		    dfs(nums, result,cur + 1);
		    // reset
		    swap(nums[cur], nums[i]);
		}
    }
```

## Combinations

```
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.
```

```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int>group;
        if(n<k)
            return res;
        combine(res,group,n,k,0,0);
        return res;

    }
private:
    void combine(vector<vector<int>>& res,vector<int>& group,int n,int k,int start,int num)
    {
        if(num==k)
        {
            res.push_back(group);
            return;
        }
        for(int i=start;i<n;++i)
        {
            group.push_back(i+1);
            combine(res,group,n,k,i+1,num+1);
            group.pop_back();
        }
    }
};
```
