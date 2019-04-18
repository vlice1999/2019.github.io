# 题目描述
## Goals and Overview

在这个PA中，你将：
###### 学习算法艺术
###### 学习有损图像压缩算法
###### 了解KD树相似的空间划分树
###### 学习加速算法策略的巧妙机制

## Part 1：Inspiration and Background
这项任务的灵感来自一篇关于一位艺术家的文章，他的作品以块状效果再现了经典的肖像。本文没有给出他使用的精确算法，但是我们将使用一种作为常见有损图像压缩算法基础的图像表示策略来创建类似的图像
######
下面的两张图片说明了这个任务的结果。请注意，第二个图像牺牲了原始图像中不包含太多颜色可变性的矩形中的颜色细节，但在包含大量可变性的原始图像区域中使用较小的矩形来保持细节。
######
在指定算法时，我们做了几个常规假设，如下所示：
###### The origin, position (0,0), is in the upper left corner of the image.
###### Rectangles are specified by a pair of points at its upper left and lower right corners
###### The upper left corner of a rectangle is the one nearest to the origin.
Image locations are typically specified as (x,y), where x is a horizontal offset, and y is a vertical offset. 
######
The original image will be represented in memory as a binary tree whose nodes contain information about rectangles.
###### Every node contains upper left and lower right points that specify a rectangle.
###### Every node also contains a pixel that represents the average color over the rectangle in the original image.
###### When a rectangle is split into two smaller rectangles, the parent node contains the whole rectangle, the left child contains the parent’s upper left corner and a new lower right corner, and the right child contains a new upper left corner and the parent’s lower right corner.
###### Rectangles can be split either horizontally or vertically.
进行这种矩形的划分和计算结果是为了最小化颜色的多样性。我们使用的可变性测量是所有像素的平方差与矩阵平均值。我们分别计算RGB三个通道的差异性指数，然后相加得到总的差异分数。用于计算差异分数的公式和它的简化版已经给出，但是在右侧也给出了等价形式。（R表示矩形面积）
#####
为了划分矩形R，我们选择垂直或者水平的划分R1和R2从而最小化这种区域指数。加拿大广场的处理前后的两个图片如下所示。
#####
为了达到这种效果，我们减掉或者修建二叉树的某些部分。使用百分比和公差这两个参数来评估子树是否适合修剪。为了修剪一个节点，我们只需删除它的左子树和右子树。如果至少（>=）其子树中的叶的百分比在其平均值的（<=）公差范围内，则修剪节点。颜色之间的距离计算为每个颜色通道上像素值差的平方和。
## Part2：Coding
#### Problem Specification (Description)
您填写的每个函数都在给定的代码中。这里的函数列表用于检查你写的函数
##### In class stats:
###### long getSum(char channel, pair<int,int> ul, pair<int,int> lr) //通道，左上角与右下角
###### long getSumSq(char channel, pair<int,int> ul, pair<int,int> lr)
###### stats(PNG & im)
###### long getScore(pair<int,int> ul, <pair<int,int> lr) 
###### RGBAPixel getAvg(pair<int,int> ul, pair<int,int> lr)
###### long rectArea(pair<int,int> ul, pair<int,int> lr)
stats类仅仅用来构建twoDtree。选择最佳的分割方案需要对每一个候补的矩形进行统计计算，并且在考虑到递归定义的树中的矩形数量时，这些计算所耗费的时间实在是太昂贵了。相反，相反，我们预计算支持结构，使必要的统计数据能够在常数时间内计算出来。我们要求一组特定的结构（每种颜色的累积和和和平方的累积和），但我们把它作为一个难题留给你去弄清楚如何使用它们来获得你需要的信息。
##### In class TwoDtree
###### void clear()
###### coid copy(const twoDtree & other)
###### twoDtree(PNG & imIn)
###### PNG render()
###### void prune(double pct, int tol)
###### Node * bulidTree(stats & s, pair<int,int> ul, pair<int,int> lr)
twoDtree 类是一个简化的二叉树。我们已经为你定义了Node类，和几个其他的内存管理功能，但是剩下其他的事都交给你了。因为我们将对.h和.cpp文件进行分级，所以欢迎您向类中添加助手函数。
## Getting the Given Code
The source code and test pictures are attached in the website. Please
download it.
######
Your assignment will be judged by the correction and the organization of your
report.
######
Good luck!
