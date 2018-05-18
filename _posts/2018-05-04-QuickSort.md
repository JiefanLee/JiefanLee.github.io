---
layout: post
title:  "Sort"
date:   2018-05-18 20:52:00
categories: algorithm sort
tags: algorithm sort
author: JiefanLee
---
* content
{:toc}











## Selection sort

```java

public class SelectionSort {

	public static void main(String[] args) {
		int a[]= {1,2,1,3,1,3,7,2,1};
		// TODO Auto-generated method stub
		int temp,flag;
		for(int i=0;i<a.length-1;++i)
		{
			flag=i;
			for(int j=i+1;j<a.length;++j)
			{
				if(a[flag]>a[j])
				{
					flag=j;
				}
			}
			temp=a[i];
			a[i]=a[flag];
			a[flag]=temp;

		}

		for(int i=0;i<a.length;++i)
			System.out.print(a[i]);
	}

}

```

## Insertion Sort

```java

public class InsertionSort {

	public static void Exc(int[] a,int i,int j)
	{
		int temp=a[i];
		a[i]=a[j];
		a[j]=temp;
	}
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int a[] = { 1, 2, 1, 3, 1, 3, 7, 2, 1 };
		for (int i = 1; i < a.length; ++i) {
			int num = i;
			while (num > 0 && a[num-1] > a[num]) {
				Exc(a, num-1, num);
				--num;
			}
		}
		for (int i = 0; i < a.length; ++i)
			System.out.println(a[i]);
	}

}

```

## Merge Sort

```java

import edu.princeton.cs.algs4.Insertion;
import edu.princeton.cs.algs4.StdRandom;

public class mergeSort {
	public static void merge(int a[],int lo,int mid,int hi)
	{
		int aux[]=new int[a.length];//使用一个新的数组存储原来的元素
		for(int i=lo;i<=hi;++i)
			aux[i]=a[i];
		int i=lo,j=mid+1;
		for(int k=lo;k<=hi;++k)//需要把a数组再次填满，所以从lo到hi进行
		{
			if(i>mid)
				a[k]=aux[j++];
			else if(j>hi)
				a[k]=aux[i++];
			else if(aux[i]>aux[j])
				a[k]=aux[j++];
			else
				a[k]=aux[i++];
		}
	}

	public static void sort(int a[],int lo,int hi)
	{

		if(lo>=hi)
		{
			return;//不要忘记了return的情况，否则数不出结果
		}
		int mid=(lo+hi)/2;
		sort(a, lo, mid);//先sort两边，再merge
		sort(a, mid+1, hi);
		if(a[mid]<=a[mid+1])
			return;
		merge(a, lo, mid, hi);
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int a[]= new int[1000];
		for(int i=0;i<1000;++i)
			a[i]=StdRandom.uniform(1000);
		sort(a, 0, a.length-1);
		for(int i:a)
			System.out.println(i);
	}

}
```


## Quick Sort

快速排序是典型的分治思想算法。每一遍排序都从序列中取一个值，以此值为key分区，分区后使这个值左边的数都小于等于这个值，右边的都大于等于这个值，这样把整个序列分为两部分，再对这两部分分别递归执行上述操作。







```
该方法的基本思想是：
1．先从数列中取出一个数作为key。
2．分区过程，将比这个数大的数全放到它的右边，小于或等于它的数全放到它的左边。
3．再对左右区间重复第二步，直到各区间只有一个数。
```

```java
import edu.princeton.cs.algs4.StdRandom;

public class quickSort {

	public static void sort(int a[],int lo,int hi)
	{
		if(lo>=hi)
			return;
		int key=a[lo],i=lo,j=hi;
		while(i!=j)//不断重复，直到最后比target小的全在左边而比target大的全在右边
		{
			while(i<j&&a[j]>=key)//找到左边比target大的数
				--j;
			while(i<j&&a[i]<=key)//找到右边比target小的数
				++i;
			int temp=a[i];//交换两个数
			a[i]=a[j];
			a[j]=temp;
		}
		a[lo]=a[i];
		a[i]=key;
		sort(a, lo, i-1);
		sort(a, i+1, hi);
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		int a[]=new int [1000];
		for(int i=0;i<1000;++i)
			a[i]=StdRandom.uniform(1000);
		sort(a, 0, a.length-1);
		for(int i:a)
			System.out.println(i);
	}
}
```
