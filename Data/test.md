+++
title = "你我似曾相识：如何计算相似度"
date = 2020-03-24T13:55:19+08:00
showonlyimage = false
image = ""
weight = 0
draft = false
+++

相似度计算通常采用距离公式求得。本文主要总结了对不同的数据类型求解对应距离的
几种方法。

<!--more-->


# 距离公式对比

相似度的计算一般采用距离公式求得，比如推荐系统中计算两个人的相似度、两个物品的
差异等。由于数据类型有数值型，也有类别型。前者一般为数字，可为浮点型或整数型；
后者一般为标号，一般为不带任何单位的整数。对于不同的数据类型，需要采用相应的距离公
式求得。

- 数值型
    - 欧几里德距离
    - 曼哈顿距离
    - 切比雪夫距离
- 类别型
    - 余弦距离
    - 杰卡德距离
    - 汉明距离

有时候也会用到组合方法，将采用不同的距离公式分别对不同的变量求解相似度，然后再
汇总成一个总相似度（再求一次距离）。


数值型距离公式对比

| 公式               | 数据      | 空间            | 形态                    |
|:-------------------|:----------|:----------------|:------------------------|
| 欧几里德距离       | 向量      | 欧几里德空间    | 直线                    |
| 曼哈顿距离         | 向量      | Taxicab         | 网格（4方向）           |
| 切比雪夫距离       | 向量      | Taxicab         | 网格（8方向）           |

欧几里德距离与余弦距离对比

| 公式               | 数据      | 空间            | 形态                    |
|:-------------------|:----------|:----------------|:------------------------|
| 欧几里德距离       | 向量      | 欧几里德空间    | 单位相关                |
| 余弦距离           | 向量      |                 | 单位无关                |

类别型距离公式对比

| 公式               | 数据      | 形态                    |
|:-------------------|:----------|:------------------------|
| 余弦距离           | 集合      | 角度                    |
| 杰卡德距离         | 集合      | 韦恩图                  |
| 汉明距离           | 文本      | 整数                    |


# 数值型距离公式

## 欧几里德距离

| 变体                             | 适用范畴                                                           |
|:---------------------------------|:-------------------------------------------------------------------|
| 欧几里德距离                     | 数据大小相对统一，没有极端数据存在                                 | 
| 归一化欧几里德距离               | 数据单位相差太大，存在极端数据                                     |

### 欧几里德距离

<img src="http://rosalind.info/media/Euclidean_distance.png" />

图片来源: Rosalind. (n.d.). [Euclidean Distance](http://rosalind.info/glossary/euclidean-distance/)

欧几里德距离，两点必经一线，即两点间的距离。

#### 公式

在欧几里德空间，存在两点$p(x_1, y_1)$和$q(x_2, y_2)$， 

$$d_2(p, q) = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$$

在欧几里德空间，存在两点$p(p_1, p_2, ..., p_n)$和$q(q_1, q_2, ..., q_n)$，

$$d_n(p, q) = \sqrt{\sum\_{i=1}^{n} (q_i - p_i)^2}$$

#### 应用

| 姓名 | 年龄 | 分数 |
|:-----|:----|:------|
| 小明 | 20  | 90    |
| 小李 | 30  | 80    |
| 小王 | 40  | 95    |

小明(`p(20, 90)`)和小李(`q(30, 80)`)的相似度为：

$$d = \sqrt{(20 - 30)^2 + (90 - 80)^2}$$

年龄(`p(20, 30, 40)`)和分数(`q(90, 80, 95)`)的相似度为：

$$d = \sqrt{(20 - 90)^2 + (30 - 80)^2 + (40 - 95)^2}$$

### 归一化欧几里德距离

#### 公式

在欧几里德空间，存在两点$p(p_1, p_2, ..., p_n)$和$q(q_1, q_2, ..., q_n)$，

$$d_n(p, q) = \sqrt{\sum\_{i=1}^{n} \frac{(q_i - p_i)^2}{n}}$$

#### 应用

| 姓名 | 年龄 | 分数 | 身高 | 体重 |
|:-----|:----|:------|:-------|:-------|
| 小明 | 20  | 90    | 1.75   | 1.60   |
| 小李 | 30  | 80    | 1.90   | 3.00   |
| 小王 | 40  | 95    | 1.50   | 0.90   |


小明(`p(20, 90, 1.75, 1.6)`)和小李(`q(30, 80, 1.9, 3.0)`)的相似度为：

$$
d = \sqrt{
    \frac{(20 - 30)^2}{4} + 
    \frac{(90 - 80)^2}{4} +
    \frac{(1.75 - 1.9)^2}{4} +
    \frac{(1.6 - 3.0)^2}{4} 
}
$$

分数(`p(90, 80, 95)`)和身高(`q(1.75, 1.9, 1.5)`)的相似度为：

$$
d = \sqrt{
    \frac{(90 - 1.75)^2}{3} + 
    \frac{(80 - 1.90)^2}{3} + 
    \frac{(95 - 1.50)^2}{3}  
}
$$


## 曼哈顿距离

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/08/Manhattan_distance.svg/566px-Manhattan_distance.svg.png" />

图片来源: Wikipedia. (n.d.). [Manhattan Distance](https://en.wikipedia.org/wiki/File:Manhattan_distance.svg)

曼哈顿距离主要用于计算网格（只允许上下左右移动）搜索空间的距离，比如棋盘、地图中的距离计算。
曼哈顿距离为两点间距离的绝对值的和。

### 公式

在网格空间中，存在两点$p(x_1, y_1)$和$q(x_2, y_2)$，

$$d_2(p, q) = |x_2 - x_1| + |y_2 - y_1|$$

在网格空间中，存在两点$p(x_1, x_2, ..., x_n)$和$q(y_1, y_2, ..., y_n)$，

$$d_n(p, q) = \sum\_{i=1}^n |x_i - y_i|$$

### 应用

在一张二维地图中，存在两个地点A和B。

<img src="https://i.pinimg.com/originals/e5/61/19/e5611940d4d42f6c31372566a83e24c1.png" />

图片来源：101Computing.com. (n.d.). [Manhattan distance calculator](https://www.101computing.net/manhattan-distance-calculator/)


#### 欧几里德距离

<img src="https://i.pinimg.com/originals/a3/3f/3c/a33f3cc227a51a8931255948b43494fe.png" />

图片来源：101Computing.com. (n.d.). [Manhattan distance calculator](https://www.101computing.net/manhattan-distance-calculator/)

<img src="https://i.pinimg.com/originals/b6/7a/6e/b67a6e41e851b5b0f70e8e2283afcaa6.png" />

图片来源：101Computing.com. (n.d.). [Manhattan distance calculator](https://www.101computing.net/manhattan-distance-calculator/)

#### 曼哈顿距离

<img src="https://i.pinimg.com/originals/6d/bb/ad/6dbbad3be99ef211c011b3414e0aa211.gif" />

图片来源：101Computing.com. (n.d.). [Manhattan distance calculator](https://www.101computing.net/manhattan-distance-calculator/)

<img src="https://i.pinimg.com/originals/94/85/7a/94857aa00a840bedc0200314528db3f2.png" />

图片来源：101Computing.com. (n.d.). [Manhattan distance calculator](https://www.101computing.net/manhattan-distance-calculator/)

A和B两点间的距离：

- 欧几里德距离：两点间的最短距离；
- 曼哈顿距离：两点间（只允许上下左右移动）的网格距离。

## 切比雪夫距离

<img src="https://iq.opengenus.org/content/images/2018/12/distance.jpg" />

图片来源：Open Genus. (n.d.). [Euclidean v.s. Manhattan v.s. Chebyshev Distances](https://iq.opengenus.org/euclidean-vs-manhattan-vs-chebyshev-distance/)

### 公式

在网格空间中，存在两点$p(x_1, y_1)$和$q(x_2, y_2)$，

$$d_2(p, q) = \max(|x_2 - x_1|, |y_2 - y_1|)$$

在网格空间中，存在两点$p(x_1, x_2, ..., x_n)$和$q(y_1, y_2, ..., y_n)$，

$$d_n(p, q) = \max_i (|x_i - y_i|)$$

### 应用

在二维地图中，初始点为（0, 0），分别计算从初始点往各方向的欧几里德距离、曼哈顿
距离和切比雪夫距离。

#### 欧几里德距离

<img src="https://i.pinimg.com/originals/76/81/06/7681062c5eb866974f1b7ed7e867cc6f.png" />

图片来源： Chris Ridley. (2018). [Measuring Distance](https://github.com/Chris3606/GoRogue/wiki/Measuring-Distance)

通常情况下，网格地图并不使用欧几里德距离来计算，如果需要用到此公式，则其近似于往8个方向
扩散的圆形。


#### 曼哈顿距离

<img src="https://i.pinimg.com/originals/43/cd/0b/43cd0b0571c1e8abe7efe46af178cbc7.png" />

图片来源：Chris Ridley. (2018). [Measuring Distance](https://github.com/Chris3606/GoRogue/wiki/Measuring-Distance)

在网格空间里，可以往上下左右4个方向移动，曼哈顿距离则为该4方向移动1步、2步或更多。
距离计算如图所示。

#### 切比雪夫距离

<img src="https://i.pinimg.com/originals/41/67/e3/4167e37ada30b457db43e5a1398870ed.png" />

图片来源： Chris Ridley. (2018). [Measuring Distance](https://github.com/Chris3606/GoRogue/wiki/Measuring-Distance)

在网格空间中，切比雪夫距离为周边8个方向的距离，比如在游戏地图中，允许玩家从原地往8个方向
移动。移动步数即为距离，往8个方向中的任一个方位移动，其成本是等价的。


# 类别型距离公式

## 余弦距离

<img src="https://i.pinimg.com/originals/1b/35/7d/1b357d3d3a9025a020116b07f77948b8.png" />

图片来源：Chris Emmery. (2017). [Euclidean vs. Cosine Distance](https://cmry.github.io/notes/euclidean-v-cosine)

如图所示，$\theta$为余弦距离，$d$为欧几里德距离。如果不需要考虑数值单位，如文本距离，
一般使用余弦距离，而非欧几里德距离计算相似度。

### 公式

假设有两个集合A和B，

$$
A \odot B = \parallel A\parallel \parallel B\parallel \cos \theta
$$

那么，

$$
\begin{aligned}
\cos \theta = d(A, B) &= \frac{AB}{\parallel A \parallel \times \parallel B \parallel}  \\\ 
            &= \frac{\sum\_{i=1}^n A\_i \times B\_i}{\sqrt{\sum\_{i=1}^n A\_i^2} \times \sqrt{\sum\_{i=1}^n B\_i^2}}
\end{aligned}
$$

### 应用

假设小明和小李分别对各类兴趣爱好打分（1-10分），分值如下表：

| 兴趣   | 小明 | 小李 |
|:--------|:-----|:----|
| 音乐   | 3 | 10 |
| 阅读   | 8 | 8  |
| 运动  | 7 | 6  |
| 学习   | 5 | 6  |
| 园艺  | 2 | 4  |
| 厨艺 | 9 | 5  |

那么，小明和小李的兴趣相似度为：

$$
\begin{aligned}
d\_\text{John\_and\_Joe} 
&= \frac{3 \times 10 + 8 \times 8 + 7 \times 6 + 5 \times 6 + 2 \times 4 + 9 \times 5}
        {\sqrt{3^2 + 8^2 + 7^2 + 5^2 + 2^2 + 9^2} \times \sqrt{10^2 + 8^2 + 6^2 + 6^2 + 4^2 + 5^2}} \\\ 
&= \frac{219}{15.2315 \times 16.6433} \\\ 
&= 0.8639 
\end{aligned}
$$

## 杰卡德距离

<img src="https://i.pinimg.com/originals/45/f3/0c/45f30ce0f9ad83ea4cf7233f7845eb3f.png" />

图片来源：Euge Inzaugarat. (2019). [How to measure distances in machine learning](https://towardsdatascience.com/how-to-measure-distances-in-machine-learning-13a396aa34ce)

### 公式

假设存在两个集合A和B，两者的相似度为：

$$d(A, B) = \frac{|A \cap B|}{|A \cup B|}$$

### 应用

假设存在两个水果集合A和B，

A = {"苹果", "梨", "树莓"}  
B = {"苹果", "西瓜"}

那么集合A和B的相似度为多少？

$$
\begin{aligned}
d(A, B) &= \frac{|A \cap B|}{|A \cup B|} \\\ 
        &= \frac{1}{4}
\end{aligned}
$$

## 汉明距离

汉明距离主要用于计算两个相同长度的字符串的不同字符位数。

### 应用

以下字符串的汉明距离为：

- ka`rol`in and ka`thr`in is 3.
- k`a`r`ol`in and k`e`r`st`in is 3.
- 10`1`1`1`01 and 10`0`1`0`01 is 2.
- 2`17`3`8`96 and 2`23`3`7`96 is 3.


# 组合方法


## 全局距离和局部距离

组合方法，即多个距离公式组合使用，一般定义一个全局距离
公式以及多个局部距离公式。先计算局部距离数值，再综合计算
一个全局距离。

### 公式

全局距离公式

$$D(p, q) = \sum\_{i=1}^n w\_i d(p, q)$$

其中$d(p, q)$为局部距离公式，局部距离公式可为上述公式的任一种，取决于
需要解决的问题以及数据类型。


# 扩展阅读

- Ratner, B. Pythagoras: Everyone knows his famous theorem, but not who discovered it 1000 years before him. J Target Meas Anal Mark 17, 229–242 (2009). https://doi.org/10.1057/jt.2009.16
- Krause, Eugene F. (1937). Taxicab Geometry : an adventure in non-Euclidean geometry. https://archive.org/details/taxicabgeometrya0000krau/mode/2up

