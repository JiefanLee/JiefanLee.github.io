---
layout: post
title:  "Two dimensional integer knapsack problem"
date:   2018-05-05 16:26:00
categories: algorithm DynamicProgramming
tags: algorithm DP
author: JiefanLee
---
* content
{:toc}

## Two dimensional integer knapsack problem







```
Read an integer W and an integer V, which are the maximum allowed weight and volume capacity of a knapsack, respecitively. Read an integer n and then n types of item; each item type has four attributes: weight (integer), volume(integer), profit (integer), and number of items (integer). An item cannot be divided into pieces. Solve the knapsack problem and print total profit of packed items.
```
```
Sample input:
215  130
10
12  9  16  4
16  4  5  4
15  12  11  3
7  17  5  2
12  9  16  4
13  2  17  1
19  14  6  5
9  8  1  2
14  8  6  5
18  1  12  3

Sample output:
219
```

Because we have already discussed the one dimensional 0-1 package, I will give the modified code directly~

```cpp
#include <iostream>
#include <algorithm>  
#include<vector>
using namespace std;

int main()
{
    int W, V, n, all = 0,w,v,num,p;
    cin >> W >> V >> n;
    vector<int> Weight, Volume, Profit;
    for (int i = 0; i < n; ++i)
    {
        cin>>w>>v>>p>>num;
        for (int j=1; j<=num; j<<=1) { //通过位操作，保证j从1取到2、4、8...这样不必把每个相同的item都放进数组，可以进行合并但同时保证可以构造出任何一个个数，比如：1+2就可以构造出3
        Weight.push_back(w*j);
        Volume.push_back(v*j);
        Profit.push_back(p*j);
        ++all;  
        num-= j;  
        }  
        if (num>0) {  
            Weight.push_back(w*num);
            Volume.push_back(v*num);
            Profit.push_back(p*num);
            ++all;
        }  
    }
    int dp[1000][1000]={0};
    for (int i = 0; i < all; ++i)
        for (int j = W; j >= Weight[i]; --j)
            for (int k = V; k >= Volume[i]; --k)
                dp[j][k] = max(dp[j-Weight[i]][k - Volume[i]] + Profit[i], dp[j][k]);
    cout << dp[W][V];
    return 0;
}

```
