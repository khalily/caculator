---
title: caculate
date: '2013-06-03'
description: 用go实现的一个计算器
categories: go
---

用 golang 实现的计算器
======================

功能支持
-------

+ 简单四则运算
+ 优先级支持
+ 小括号支持

简单演示
-------

	$ ./caculator 
	Please input express:
	1+2*1-12+2-(1+2*3)
	[1 + 2 * 1 - 12 + 2 - ( 1 + 2 * 3 )]      //中缀表达式
	[1 2 1 * + 12 - 2 + 1 2 3 * + -]			//后缀表达式
	-14										//结果
	
实现流程
-------

![caculate.png](/home/wyang/Cloud/documents/khalily.github.com/media/caculate.png "title")
	

后缀到前缀的转换
--------------
	func pre2stuf(exps []string) (exps2 []string) {
		list1 := list.New()
		list2 := list.New()
	
		for _, exp := range exps {
			if isOperate(exp) {
				if op, ok := isPop(list1, exp); ok {
					for _, s := range op {
						list2.PushBack(s)
					}
				}
				if exp == ")" {
					continue
				}
				list1.PushBack(exp)
			} else {
				list2.PushBack(exp)
			}
		}
	
		for cur := list1.Back(); cur != nil; cur = cur.Prev() {
			list2.PushBack(cur.Value)
		}
	
		for cur := list2.Front(); cur != nil; cur = cur.Next() {
			if curValue, ok := cur.Value.(string); ok {
				exps2 = append(exps2, curValue)
			}
		}
		return
	}
	
代码在[这里](https://github.com/khalily/caculate)	
---------- 
	git clone git@github.com:khalily/caculate.git
	
欢迎交流！^_^
