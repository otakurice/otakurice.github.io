---
title: opencv在python中的哈夫直线变换(Hough Line Transform)
date: 2018-07-12 22:54:01
tags:
- 图像识别
- opencv
categories:
- 翻译
---
### 说明
在做项目中，需要识别图片中的表格，了解到opencv中的哈夫变换，[相关文档](http://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_houghlines/py_houghlines.html)只有英文版，未找到中文版，自行翻译了一遍(能力有限渣翻译)，其中拓展阅读内容引自：[Python OpenCV -- 霍夫线变换（十二）](https://blog.csdn.net/mokeding/article/details/19615873)，可帮助理解，仅供参考。


### 目标

在本章中，我们可以：

- 了解哈夫变换的概念

- 如何使用哈夫变换识别图片中的直线

- 了解以下函数：**cv2.HoughLines()**, **cv2.HoughLinesP()**

### 理论

哈夫变换(Hough Transform)是一种流行的图形识别技术，如果数学模型中的图形可以被肉眼识别，那么即使图形损坏或者有一点扭曲，哈夫变换也可以识别图形，接下来介绍它的工作原理。

直线可以通过类似 y = mx + c 或 极坐标 ρ = x cosθ + y sinθ(其中ρ表示原点到直线的垂直距离，θ是垂直线与水平轴之间的逆时针方向夹角，方向主要取决于如何放置坐标系)来表示。如下图：

![](https://upload-images.jianshu.io/upload_images/5588611-6e9d63d2385d7296.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果线经过原点下方，那就有小于180°的正[RHO][^脚注]和夹角。如果线经过原点上方，相较于使用大于180°的夹角，opencv会选择使用小于180°的夹角，并采用负的RHO。垂直线是0°，水平线是90°。

来看看哈夫变换如何处理线条。任何线条都可以由(ρ,θ)2个参数形容，首先创建一个二维数组或者累加器(存储2个参数的值)，初始化为0。用行表示ρ，用列表示θ，数组的大小取决于精确度需求，假设精确度为1°，则需要180列，ρ最大距离可能是图片对角线的长度，所以设置精确度为1像素，那么行数就是图片对角线长。

***

### 拓展阅读

1、![](https://upload-images.jianshu.io/upload_images/5588611-b048fbc34bce979a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

用 极坐标系 来表示直线，直线的表达式可为:

$$ y = (- \frac{cosθ}{sinθ})x + (\frac{r}{sinθ}) $$

化简得： $ r = x cosθ + y sinθ $

2、一般来说对于点$(x_0,y_0)$, 我们可以将通过这个点的一族直线统一定义为:

$$ r_\theta = x_0 · cos\theta + y_0 · sin\theta $$

这就意味着每一对$(r_\theta, \theta)$ 代表一条通过点$(x_0,y_0)$的直线.

***
假设有一个100*100的图片，有一条水平线在中间，获取这条线的第一个点，已知它的(x, y)值，然后将θ = 0,1,2,……,180放入线条方程中，获取ρ值。对于每个(ρ, θ)单元格，累加器中与之相关的(ρ, θ)单元格每次增加的值为1，所以在累加器中，(50, 90) = 1和一些其他单项相关联。

然后取线条上的第二个点，进行以上相同的动作，增加与之相关联的(ρ, θ)单元格，此时(50, 90) = 2，现在的操作都会增加(ρ, θ)的值。继续为线条上的每个点进行相同的操作，在每个点，(50, 90)单元格可以增值或者计数，其他单元格可能不会被计数。通过这种方式，最后(50, 90)单元格会得到最大的计数。如果在计数器中搜索最大计数，就可以得到(50, 90 )的值，表示在距离原点50，90°角的地方有一条线，在以下动图中显示。

![](https://upload-images.jianshu.io/upload_images/5588611-e15cf762963c683b.gif?imageMogr2/auto-orient/strip)


这就是哈夫变换作用于线条的原理，可以使用numpy来执行它。下图展示了累加模型，图中高亮的位置代表着图片中可能是线条的参数。

![](https://upload-images.jianshu.io/upload_images/5588611-6ecd812e67ec9ffa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

***
### 拓展阅读

1、如果对于一个给定点$(x_0,y_0)$ 我们在极坐标对极径极角平面绘出所有通过它的直线, 将得到一条正弦曲线. 例如, 对于给定点 $x_0 = 8$ 和 $y_0 = 6$我们可以绘出下图 (在平面 $\theta - r$):

![](https://upload-images.jianshu.io/upload_images/5588611-79866e52cbabfb86.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

只绘出满足下列条件的点$r > 0$ 和 $0 < \theta < 2\pi$.

2、我们可以对图像中所有的点进行上述操作. 如果两个不同点进行上述操作后得到的曲线在平面$\theta - r$相交, 这就意味着它们通过同一条直线. 例如, 接上面的例子我们继续对点: $x_1 = 9, y_1 = 4$ 和点$x_2 = 12, y_2 = 3$ 绘图, 得到下图:

![](https://upload-images.jianshu.io/upload_images/5588611-d38f2d6f0d10dff0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这三条曲线在$\theta - r$平面相交于点$(0.925, 9.6)$, 坐标表示的是参数对$(\theta, r)$ 或者是说点$(x_0,y_0)$, 点$(x_1,y_1)$ 和点$(x_2,y_2)$ 组成的平面内的的直线.

3、一条直线能够通过在平面$\theta - r$ 寻找交于一点的曲线数量来**检测**. 越多曲线交于一点也就意味着这个交点表示的直线由更多的点组成. 一般来说我们可以通过设置直线上点的 阈值 来定义多少条曲线交于一点我们才认为**检测** 到了一条直线.

4、这就是霍夫线变换要做的. 它追踪图像中每个点对应曲线间的交点. 如果交于一点的曲线的数量超过了**阈值**, 那么可以认为这个交点所代表的参数对$(\theta, r_\theta)$ 在原图像中为一条直线.

***

### OpenCV中的哈夫变换

上面讲述的是Opencv中的函数，cv2.HoughLines()。它返回(ρ, θ)值的序列，ρ单位像素，θ单位弧度。第一个参数，输入的图片是一个二进制图片，在使用hough变换之前，应用阈值或使用canny边缘检测。第二和第三个参数分别是ρ和θ的精度，第4个参数是阈值，指可以被认为是一个线条的最小计数值。由于计数值的多少取决于线上的点数，所以这代表了可以被识别为线的最小长度。

```python
import  cv2
import  numpy  as  np

img  =  cv2.imread('dave.jpg')
gray  =  cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
edges  =  cv2.Canny(gray,50,150,apertureSize  =  3)

lines  =  cv2.HoughLines(edges,1,np.pi/180,200)
for  rho,theta  in  lines[0]:
    a  =  np.cos(theta)
    b  =  np.sin(theta)
    x0  =  a*rho
    y0  =  b*rho
    x1  =  int(x0  +  1000*(-b))
    y1  =  int(y0  +  1000*(a))
    x2  =  int(x0  -  1000*(-b))
    y2  =  int(y0  -  1000*(a))

    cv2.line(img,(x1,y1),(x2,y2),(0,0,255),2)

cv2.imwrite('houghlines3.jpg',img)
```

认为第9行代码存在一定错误，应为：

```
for i in range(0,len(lines)):
    rho,theta = lines[i][0][0],lines[i][0][1]
```

结果如下：

![](https://upload-images.jianshu.io/upload_images/5588611-a59dc20f46855769.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 概率哈夫变换

在哈夫变换中，可以通过2个变量来检测一条线上的点，但花费大量计算。概率哈夫变换是一个优化的哈夫变换，它不会计算所有的点，而是随机的选取一组足以识别直线的点，所以我们需要减少阈值。看下图中关于哈夫变换和概率哈夫变换在哈夫空间的比较：

![](https://upload-images.jianshu.io/upload_images/5588611-c16b6f62a0c081f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

OpenCV 技术是基于Matas, J. and Galambos, C. and Kittler, J.V.使用概率哈夫变换进行的线条鲁棒检测。它通过cv2.HoughLinesP()来实现,函数有2个新的参数。

- **minLineLength** - 线段的最小长度. Line segments shorter than this are rejected.

- **maxLineGap** - 使程序识别线段为一条线的线段之间最大的空隙

最好是这样，函数直接返回了线条的两个终点，在前面的实例中，必须找到所有的点，而只获取了线的参数。在这个实例中，所有的事都变得简单直接。

```python
import  cv2
import  numpy  as  np

img  =  cv2.imread('dave.jpg')
gray  =  cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
edges  =  cv2.Canny(gray,50,150,apertureSize  =  3)
minLineLength  =  100
maxLineGap  =  10
lines  =  cv2.HoughLinesP(edges,1,np.pi/180,100,minLineLength,maxLineGap)
for  x1,y1,x2,y2  in  lines[0]:
    cv2.line(img,(x1,y1),(x2,y2),(0,255,0),2)

cv2.imwrite('houghlines5.jpg',img)
```

结果如下：

![](https://upload-images.jianshu.io/upload_images/5588611-cfe11f9ad29ff624.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

[^脚注]: 曲线饱满度，RHO 值越小,曲线就越平坦;RHO值越大,曲线就越饱满,RHO<0.5,曲线为椭圆,RHO=0.5时,曲线为抛物线;RHO>0.5时,曲线为双曲线!
