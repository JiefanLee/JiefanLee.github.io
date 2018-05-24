---
layout: post
title:  "链表主要功能实现"
date:   2018-05-24 10:28:00
categories: dataStructure sort
tags: dataStructure sort
author: JiefanLee
---
* content
{:toc}








This blog means to provide almost all of the functions of linklist: sort, reverse, remove, insert...

## 头文件

```cpp
//linklist.h：定义链表结点和方法。  
#include<iostream>
using namespace std;

struct Node
{
	int val;
	Node \*next;
	Node(int x) :val(x), next(NULL) {}
};

class LinkList
{
public:
	//构造函数  
	LinkList();
	//在链表头部插入结点  
	void InsertHead(int val);
	//插入结点  
	void Insert(int val, int pos);
	//删除结点  
	void Remove(int pos);
	//得到链表长度  
	int Length();
	//链表反序  
	void Reverse();
	//查找结点位置  
	void Find(int val);
	//打印链表  
	void Print();
	//从大到小排序  
	void Sort();
	//析构函数
	~LinkList();
private:
	Node * head;
	int length;
};
```

## 功能实现

```cpp
//linklist.cpp：链表方法的实现。  
#include <iostream>  
#include "linklist.h"  
using namespace std;

LinkList::LinkList()
{
	head = NULL;
	length = 0;
}

LinkList::~LinkList()
{
	Node \*temp;
	for (int i = 0; i < length; i++)
	{
		temp = head;
		head = head->next;
		delete temp;
	}
}

int LinkList::Length()
{
	return length;
}

void LinkList::InsertHead(int val) {
	Insert(val, 0);
}

void LinkList::Insert(int val, int pos) {
	if (pos < 0)
	{
		cout << "The index must be larger than 0!" << endl;
		return;
	}
	int index = 1;
	Node \*temp = head;
	Node \*node = new Node(val);
	if (pos == 0)
	{
		node->next = head;
		head = node;
		length++;
		return;
	}
	while (temp != NULL && index < pos)
	{
		temp = temp->next;
		index++;
	}
	if (temp == NULL)
	{
		cout << "Fail to insert it!" << endl;
		return;
	}
	node->next = temp->next;
	temp->next = node;
	length++;
	return;
}

void LinkList::Remove(int pos)
{
	if (pos < 0 || length < 1)
	{
		cout << "The index must be larger than 0!" << endl;
		return;
	}
	int index = 1;
	Node \*temp = head;
	if (pos == 0 && length == 1)
	{
		head = NULL;
		length--;
		return;
	}
	if (pos == 0 && length > 1)
	{
		head = temp->next;
		length--;
		return;
	}
	while (temp != NULL && index < pos)
	{
		temp = temp->next;
		index++;
	}

	if (temp&&temp->next&&temp->next->next)
	{
		temp->next = temp->next->next;
		length--;
		return;
	}
	cout << "Fail to delete it" << endl;
	return;
}
void LinkList::Sort()
{
	if (length <= 1)
		return;
	Node \*i = head;
	for (; i != NULL; i = i->next)
		for (Node *j = i; j != NULL; j = j->next)
		{
			if (i->val > j->val)
			{
				int temp = i->val;
				i->val = j->val;
				j->val = temp;
			}
		}
	return;
}

void LinkList::Reverse()
{
	if (length <= 1)
		return;
	Node \*pre = new Node(0);
	pre->next = head;
	Node \*cur = head;
	while (cur&&cur->next)
	{
		Node \*move = cur->next;
		cur->next = move->next;
		move->next = pre->next;
		pre->next = move;
	}
	head = pre->next;
	return;
}

void LinkList::Find(int val)
{
	if (length == 0)
	{
		cout << "Not found" << endl;
		return;
	}
	Node \*p = head;
	int index = 1;
	int count = 0;
	while (p)
	{
		if (p->val == val)
		{
			cout << index++ << " ";
			p = p->next;
			count++;
		}
		else
		{
			p = p->next;
			index++;
		}
	}
	if (count == 1)
		cout << "There is " << 1 << " found." << endl;
	else if (count > 1)
		cout << "There are " << count << " found." << endl;
	else
		cout << "Not found" << endl;;
	return;
}

void LinkList::Print()
{
	if (head == NULL)
	{
		cout << "This is an empty LinkList" << endl;
		return;
	}

	Node \*p = head;
	while (p!=NULL)
	{
		cout << p->val << " ";
		p = p->next;
	}
	cout << endl;
	return;
}
```
