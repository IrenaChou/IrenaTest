---
title: Swift-lazy懒加载
date: 2017-04-21 15:56:44
tags: 'Swift'
---

Swift-lazy懒加载
---
```// 懒加载属性
    private lazy var testView : UIView = {
    	let tView = UIView()
    	return tView
    }()
```
