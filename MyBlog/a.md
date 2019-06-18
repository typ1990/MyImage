---
title: Rtree算法
date: 2019-04-10 14:38:46
tags: LBS
---
注：部分来源于网络

Rtree是为解决二维及二维以上的数据索引问题的。常用于解决空间问题。

空间数据经常是多维的，并不能用一些点来简单的表示。例如地图里面的街道、村庄等。对空间数据的一个典型操作是查找某个区域的所有目标（例如查找中关村大街上所有的餐馆等）。

对空间数据建立索引是一种好的想法，但传统数据库的一维索引并不适合对多维数据的查找。例如 hash 等结构也不适合，因为搜索的时候有一定的范围。而类似 B-Tree 的一些结构不能实现对多维数据的查找。

算法原理：
![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170410084842668.jpg)



空间内二维数据多变新是不规则矩形，我们以一种统一的矩形对对多边形来进行处理，采用最小外包矩形来标识多边形。

使用左下角点和右上角点来表示矩形
![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170410084842355.jpg) 

![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/WX20190410-162112%402x.png)

对所有矩形构建索引，矩形分为P1,P2,P3,P4
![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170410084846733.jpg)








本算法使用的Rree算法是来自于：https://github.com/davidmoten/rtree



算法使用：

    //初始化Rtree
    RTree<Object, Rectangle> stashTree = RTree.create();
    //给矩形添加索引，注意矩形定义的是（x1,y1,x2,y2）,分别为左下角点和右上角点
    stashTree=stashTree.add(Entries.<Object, Rectangle>entry(1+"",rectangle(1, 1, 2, 2)));
    stashTree=stashTree.add(Entries.<Object, Rectangle>entry(2+"",rectangle(2, 2, 4, 4)));
    //查询坐标点(2,2),是否在矩形（1，1，2，2）和矩形（2，2，4，4）中
    List<Entry<Object, Rectangle>> list=stashTree.search(Geometries.point(2,2)).toList().toBlocking().single();
            for (Entry<Object, Rectangle> t:list) {
        System.out.println(t.geometry().area());
    }
    
    打印结果：
    1.0
    4.0
    

以上例子中首先创建索引，然后对两个矩形添加索引，最后出搜索点所在的矩形，打印矩形面积。

    创建RTree
    RTree<String, Geometry> tree = RTree.create();
    如果确定存储类型，例如Rectangle，也可指定类型创建
    RTree<Object, Rectangle> tree = RTree.create();
    添加结点到Rtree，需要指定该结点的平面位置或范围。Geometries提供了以下几种构造结点的方法
    

    
        