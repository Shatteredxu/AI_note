# 一二章

## 第一章

神经网络的核心原则：线性处理单元与非线性处理单元的交替使用，使用反向传播来更新参数  
深度学习是具有多级表示的表征学习方法，深度学习模型可以看做由许多简单函数复合而成的函数。  
深度学习是端到端的训练，是将系统组合好后，一起训练。

## 第二章

### 环境搭建参考了：

[https://discuss.gluon.ai/t/topic/13576](https://discuss.gluon.ai/t/topic/13576)

### MXNET使用流程：

conda activate gluon  
python

### NDarry

```python
#从MXNET导入ndarry模块：
from mxnet import nd
#创建行向量
x=nd.arange()
#实例的形状
x.shape
#实例中元素的个数
x.size
#改变行向量的形状
x.reshape(())
创建某形状的张量
nd.zeros();nd.ones()
#随机创建均值为0，标准差为1，形状为（3,4）的矩阵
nd.random.normal(0,1,shape=(3,4))
#按矩阵中元素进行运算
X+Y;X*Y;X/Y;X.exp();
#dot矩阵相乘，Y.T矩阵进行转置
nd.dot(X,Y.T)
#矩阵相连，dim=0行上连接，dim=1列上连接
nd.concat(X,Y,dim= )
#将范数X.norm()转换为标量
X.norm().asscalar()
```

### 广播机制

形状不同的矩阵进行元素运算时，会适当复制元素使矩阵形状相同后再进行运算。

### 索引

行列索引均从0开始

```python
#显示X的一到二行，左闭右开。
X[1:3]
#依据索引重新赋值
X[1, 3] = 6
#截取一部分元素赋值
X[1:2, :] = 13 //[1,2)行赋值为13
```

### 运算的内存开销

以上每个操作会开辟新的内存来存储运算的结果，使用id可以比较地址是否相同。  
减少内存开销可以：  
使用zeros\_like\(\)建立形状相同矩阵;  
Z = Y.zeros\_like\(\)  
使用out直接存入;  
nd.elemwise\_add\(X,Y,out=Z\)

## 如果操作的矩阵后续不再使用，可以直接覆盖来减少内存开销：

X += Y

### NDArray和NumPy转换：

```python
#NP->ND:
P = np.ones((2, 3))
D = nd.array(P)
#ND->NP:
D.asnumpy()
```

### 使用autograd模块求梯度。

```python
from mxnet import autograd, nd
x = nd.arange(4).reshape((4, 1))//创建列向量x
x.attach_grad()                 //申请内存储存梯度
with autograd.record()          //要求MXNET记录梯度计算过程
y = 2 * nd.dot(x.T, x)          //定义关于x的函数
y.backward()                    //求梯度
```

同时autograd在默认情况下会把将运⾏模式从预测模式转为训练模式。  
MXNET也可以对python控制流求梯度。
