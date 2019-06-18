---
title: 计算两个经纬度之间的距离
date: 2019-06-18 15:36:10
tags:
---
    本文参考https://blog.csdn.net/xiejm2333/article/details/73297004，但其中有错误之处，会在下面指出
    
 首先，你要想了解清楚经纬度的具体定义，看完后再往下看，便会一目了然。
 
 将地球看成一个球体，A（WA，JA）、B（WB，JB）两点分别为两个点的位置，其中W为纬度，J为经度，O为球心，球半径为R，过A点画出A的纬度圈并与B所在的经度相交与点C，分别过B、C两点做球心O所在直线 的垂线相交与E、H，点B做垂线与CH的延长线相交于点D，OH与BC延长线相交与点F。添加辅助线后的两点距离示意图如图所示。

![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170617095207151.png)

图 两点距离示意图

由示意图可知， H、E分别为A、B两点所在纬度圈的圆心，C点为与A点纬度相同，与B点经度相同，F为BC与HE延长线的交点，△OCF∽△DCB，因此：

![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170617095150226.png)

因为△AHF为直角三角形，所以

![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170617095308479.png)

由于A、C点在同一个纬度圈上，所以AH=CH

设∠ACF为α，则设∠ACB为π-α，根据余弦定理得
![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170617095504386.png)

综上则可以得出：

![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170617095536106.png)

根据A、B两点经纬度可知：
![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170617095606294.png)
      
AB弧长（AB两点的距离）为（注：此处错误，应该是L=2R*sin(AB/2)）
![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170617095738309.png)

最后计算得：
![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170617095831856.png)

具体过程如下图：
![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/20170617095855403.png)

公式中的经纬度均用弧度表示，计算两点距离的核心代码如下：
```java
public static double algorithm(double longitude1, double latitude1, double longitude2, double latitude2) {

              double Lat1 = rad(latitude1); // 纬度

              double Lat2 = rad(latitude2);

              double a = Lat1 - Lat2;//两点纬度之差

              double b = rad(longitude1) - rad(longitude2); //经度之差

              double s = 2 * Math.asin(Math

                            .sqrt(Math.pow(Math.sin(a / 2), 2) + Math.cos(Lat1) * Math.cos(Lat2) * Math.pow(Math.sin(b / 2), 2)));//计算两点距离的公式

              s = s * 6378137.0;//弧长乘地球半径（半径为米）

              s = Math.round(s * 10000d) / 10000d;//精确距离的数值

              return s;

       }

 

       private static double rad(double d) {

              return d * Math.PI / 180.00; //角度转换成弧度

       }
```



我自己的推算流程，有些乱,请见谅，如有疑问，写在评论里
![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/WechatIMG144.jpeg)

![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/WechatIMG141.jpeg)

![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/WechatIMG142.jpeg)

![avatar](https://raw.githubusercontent.com/typ1990/MyImage/master/MyBlog/WechatIMG143.jpeg)
