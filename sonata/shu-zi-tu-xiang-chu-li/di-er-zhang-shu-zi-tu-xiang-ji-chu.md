# 第二章 《数字图像基础》

#### 图像形成模型

**概念**

场景元素在照射源下，借助成像系统，完成场景到图像平面的投影。对该图像进行数字表示的过程中，我们将每个像素点的颜色分为不同的幅度$f\(x, y\) &gt; 0$，其中$x、y$表示这个像素点在二维坐标中的位置，$f$值在学术上称为幅度，但其意义是对颜色的精准定义。

另外，函数$f$需要使用两个分量来表示，分别是入射分量和反射分量，两者的乘积得到最终的幅度值。**入射分量**是在某个时间下该物体的平均照度（人话：光照强度），其值取决于光照源。**反射分量**则与物体的材质有关，其值限制在0～1之间。

> 天气晴朗的时候，入射分量可以很大，那我们人为得看某个物体就可以很清楚。但是如果天黑了，那就看不清楚了。
>
> 而反射分量也很典型，比如说不锈钢的反射分量为0.65，黑天鹅绒是0.01，所以在黑暗情况下，我们能分辨出某处有块钢板，但是基本上看不出哪里有个黑天鹅绒，因为它对光线基本上全吸收了。

**灰度级**

在单色图像中，使用灰度级表示每个像素的颜色强度。级别越高，表明该像素点的颜色就越接近于白色。灰度级通常用一个区间$\[0, L-1\]$表示，0表示黑色，$L-1$表示白色，之间的数值则具体表示某一程度的灰色。

**分辨率**

**空间/灰度分辨率**：

每单位距离的线对数或每个单位距离的像素数。灰度分辨率指的是用于量化灰度的比特数。

**分辨率的变化**：

当改变$M、N、k$的大小时，图像的分辨率也会相应的有所改变。

下面假设$M = N$，那么该图像所占用字节数为$N^2\*k = b$ , 另外经过调查发现，K值、N值越大，用户对图像的偏爱程度越高。但是当某张图像中的细节增加时，偏爱曲线会变得垂直，也就是说此时参数的变化对曲线的影响较小，因为对那些具有大量细节的图像，可能只需要较少的灰度级就能表示。

#### 图像取样与量化

**取样原因与过程**

我们知道，对于一幅在灰度（幅度）上连续变化的图像，想要使用数字表示该图像，必须使用部分采样的方式进行离散化，否则连续表示的结果是无穷的。

> 比如在一条从左向右的颜色为由白到黑的丝带，其幅度值是由高到低连续变化的，我们是不可能完整表示一个数组内部的值的，因为是无穷无尽的。

如果要数值化地表示图像，就从该图像的顶部开始，逐一取一条线段AB，并等间隔地取点，赋予这些采样点一个特定的灰度值。然后把这些采样点按照顺序排列，就可以拼接出这幅图的数字表示了。

**量化过程**

前面的介绍已经知道了，在单色图像中，可以用一个灰度级别来表达某像素点的颜色，这个过程就称为量化，也就是把颜色用数值表示。量化需要确定一个离散的灰度级，比如在本书例题中的灰度级是8，是离散的8个灰度，而且数量比较少。

那么，取样过程已经确定了待量化的采样点，接下来就要对每个样本赋予8个离散灰度级中的一个来量化连续灰度级。

**灰度级**

为了让计算机更好地表示每个级别，在量化过程中通常使用2的整数次幂$L = 2^k$作为灰度划分。当k值为4时，表示从白到黑的变化过程中，我们将其分成了16个等级。可以知道，k值越大，进行数值化表示的时候，颜色变化边界就越不明显。当数字图像的平滑区域由于灰度级数不足时，将出现伪轮廓。

**数字图像表示**

将连续的图像函数离散化表示后，进而可以将此图像使用二维矩阵表示，甚至是之后需要使用的向量。假设该图像矩阵为$M \times N$的大小，其左上角表示第一个元素，每个位置上的数值都表示该像素点的灰度级别。当k = 8时，灰度跨越的值域是$\[0, 255\]$。此时每个像素需要8个字节存储，那么该图像所占空间为$b = M \times N \times k$。

**动态范围与对比度**

系统能表示的最高和最低可检测灰度之比就是动态范围，它们的差值则被称为对比度。因此当一幅图像中有高的动态范围时，可认为该图像有高的对比度。当某灰度级超过了饱和度时，就将被裁切掉这个值。

#### 像素之间的一些关系

**基础概念**

**相邻像素**：被分成了四邻域、八邻域、D邻域。

**连接像素**：如果两个像素点是上述三种相邻状态，并且他们的像素都符合一定要求V，那么就说这两个像素是连接的。

**混合邻接**：对于像素p和q而言，假如1. 他们是四邻接的，或2. 两个像素对角邻接且它们4邻域的交集在相似准则的意义下是空集，那么他们就是混合连接的，也可以称为是m连接。

通路、像素连通；

**像素间距离**

1. 欧式距离
2. 曼哈顿距离
3. 棋盘距离
4. 混合距离：其大小不仅与像素的坐标有关，还与像素本身及其邻近像素的属性值有关。

#### 数学工具介绍

**阵列与矩阵**

图像的表达使用的是阵列，与矩阵相近，但阵列之间的运算是基于每个像素的相对位置来进行的。也就是说，假设此时令两个阵列相加，其过程为两个阵列相对位置相同的元素进行相加，成为点运算。

**线性与非线性判断**

$$H\[f\(x, y\)\] = g\(x, y\)$$，其中H是算子。

1. 若H是线性函数，则公式满足加性；若不满足加性，说明该算子就是非线性的。
2. 证明某操作是非线性的时候，只需要直接证明其不满足加性即可。

> 加性：输入和经过其操作的结果 = 输入经过操作后求和

**算术操作**

1. 图像降噪：对带噪声的图像相加后取平均，即对一组噪声数字进行平均操作。

   $$g\(x, y\) = f\(x, y\) + \eta\(x, y\)$$，g 表示的是污染后的图像，而公式的后项表示的是本次污染程度。

   $$\hat g\(x, y\) = \frac{1}{k} \sum^k\_{i=1}g\_i\(x, y\)$$

2. 图像增强（相减）：$g\(x, y\) = f\(x, y\) - h\(x, y\)$
3. 校正阴影：图像相乘，给定一幅图像相乘，横版图像的ROI区域为1。

**逻辑运算**

1. 负像：负像的像素集合A中的灰度为${\(x, y, K - z\) \| \(x, y, z\) \in A}$
2. 与或非、异或

**空间操作**

1. 单像素操作：S = T\(z\) 操作函数为T，原始像素为z；
2. 邻域操作：$S\_xy$是以x、y为中心的一个邻域坐标集，经过某操作后得到某个像素位，故最终得到结果为新图g中的像素值。
3. 几何变换：主要将原图乘上特定矩阵后的所得结果，实现了图像的几何变换。其中包括尺度变换、旋转、平移等。
