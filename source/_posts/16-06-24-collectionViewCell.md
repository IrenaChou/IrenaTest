title: UICollectionView处理翻半页问题
date: 2016-06-24 15:22:58
tags:
---
大部分使用过collectionView的朋友，一定会有遇到过如下问题的，想实现图1的效果，结果确如图2（**我称这种效果为翻半页**）：

**图1**
![图1](http://7xrirn.com1.z0.glb.clouddn.com/collectionView.gif) 


**图2**
![图2](http://7xrirn.com1.z0.glb.clouddn.com/collectionView-1.gif) 
<!-- more -->
本文实现的思路：
---
如cell个数不能正好填充满一整页，填充空cell，使用cell填充满一整页，避开翻半页的效果，**需要注意的是返回cell个数是添加了空cell后的总个数**

计算总cell代码如下
```
/**
 *  计算包含空cell的总cell数
 */
- (NSUInteger)pageSumCount {
  _pageSumCount = [self.items count];
  while (_pageSumCount % kPageCellCount != 0) {
    ++_pageSumCount;
  }
  return _pageSumCount;
}
```

[Demo下载](http://pan.baidu.com/s/1hsEuY2o)
---