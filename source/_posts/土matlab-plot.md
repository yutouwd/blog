---
title: Matlab 画图小技巧笔记
copyright: true
comments: true
tags:
  - Matlab
  - 画图
categories:
  - 科研
abbrlink: 3250640614
date: 2021-06-05 04:03:03
---

记录一下用过的一些Matlab画图技巧📈
持续补充中

<!-- more -->


# 基础知识

## 折线图


## 箱线图

箱线图x轴标签方向
```matlab
boxplot(X, 'Labels', {'40 R-L', '40 L-R', '50 R-L', '50 L-R', '60 R-L', '60 L-R'}, 'LabelOrientation', 'inline');
```

# 修改属性
## 坐标轴相关

### 获取坐标轴对象

```matlab
% 可以直接用gca命令来获取
% get current axis
ax = gca;

% 可以直接更改坐标轴对象的属性
% 更改坐标轴颜色
ax.Color = 'blue'

% 或者使用set来设置坐标轴对象的属性（早期版本只能通过set来设置）
% 更改坐标轴刻度字体大小
set(gca, 'FontSize', 30)
% 设置字体加粗
set(gca, 'FontWeight, 'bold')
```

关于坐标轴对象属性的文档在这里👇：

https://www.mathworks.com/help/matlab/ref/matlab.graphics.axis.axes-properties.html

### 设置显示网格（可以只显示单一轴的网格）

```matlab
% 只显示x轴网格
% 通过on和off来设置显示与否
set(gca, 'XGrid', 'on', 'YGrid', 'off')
```

### 设置是否显示坐标轴刻度

```matlab
% 隐藏坐标轴刻度
% 同样可以控制只隐藏特定轴
set(gca, 'XTickLabel', [], 'YTickLabel',[])
```


## 图例相关

### 获取图例对象

```matlab
leg = legend(...)
```

图例对象的相关属性文档：
https://www.mathworks.com/help/matlab/ref/matlab.graphics.illustration.legend-properties.html

### 设置图例方向

```matlab
% 可以选择横向或竖向
leg.Orientation = 'horizontal';
leg.Orientation = 'vertical';
```

### 设置多列显示

```matlab
% 可以通过调节列的数量来做到多列显示
leg.NumColumns = 2;
```


### 设置每一个图例的大小

```matlab
leg.ItemTokenSize = [216,40];
```



# 美化小技巧

## 颜色搭配

这里推荐知乎博主的搭配：

{% asset_img m1.jpg %}

以及日本传统色这个网站，可以找到很多不错的颜色：
https://nipponcolors.com/

## 画图速查表

非常有用的画图速查表：https://github.com/Pjer-zhang/matlabPlotCheatsheet


{% asset_img m2.png %}


# 参考资料

一些小技巧和基础知识：
https://zhuanlan.zhihu.com/p/82421043
figure对象的相关知识：
https://zhuanlan.zhihu.com/p/47487701
画图颜色搭配：
https://zhuanlan.zhihu.com/p/58810578
画图速查表：
https://github.com/Pjer-zhang/matlabPlotCheatsheet
https://zhuanlan.zhihu.com/p/112229373
图坐标轴相关属性：
https://www.mathworks.com/help/matlab/ref/matlab.graphics.axis.axes-properties.html
图例相关属性：
https://www.mathworks.com/help/matlab/ref/matlab.graphics.illustration.legend-properties.html