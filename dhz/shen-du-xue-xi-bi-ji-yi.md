# 第一二章学习笔记

## 一、环境的安装和配置

`注：使用的深度学习框架是MXNet（即操作系统一定要是64位的）`  


> 由于之前一直都在win下使用pycharm来进行深度学习实验，这次尝试在linuix下搭建深度学习环境（曾经使用百度云深度学习服务，也是百度事先搭好环境）， 由于怕装双系统挤爆可怜的C盘小固态，选择虚拟机先试试水。故使用cpu版本。 之前有在win下搭建使用过GPU,奈何显卡垃圾，显存太小，相比百度云的K40显卡体验极差。

### 1.Linux下安装miniconda

首先复制下载地址 [https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/](https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/) 到浏览器中打开（推荐到清华大学开源镜像站下载，不要到官网下载， 因为官网下载速度非常慢），然后下拉到最底部，找到下面这个软件包：

```text
Miniconda3-latest-Linux-x86_64.sh
```

单击它便可以将最新的64位miniconda3的安装包下载到本地。打开终端，切换到刚才下载的miniconda安装包所在目录，执行如下命令来安装：

```text
bash  Miniconda3-latest-Linux-x86_64.sh
```

`执行上面的安装命令时，首先会弹出一个软件协议条款让你阅读，这时候直接按下Ctrl+C便可以跳过阅读过程`  


然后安装过程一直yes就可以了，重启终端之后，便可以使用miniconda了。  


为了日后使用的方便最好是将将conda和pip的软件源修改成清华的源，这样的话，使用miniconda或者pip安装软件速度会快很多。`但是书上提供的方法有问题` 可使用如下指令进行设置:

```text
conda  config  --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda  config  --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda  config  --set show_channel_urls yes

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

## 获取代码

按书上很快就ok了

## 搭建mxnet运行环境

`书上利用配置文件搭建环境没有成功，就自己手打了` 打开命令行终端，然后执行如下命令来创建一个使用Python 3.6的，名为gluon的环境：

```text
conda create -n gluon python=3.6
```

创建环境成功后，执行如下命令来激活gluon环境：

```text
conda activate gluon
```

接下来该安装MXNet了，执行如下命令，安装1.5.0版的mxnet ：

```text
pip install mxnet==1.5.0
```

成功安装MXNet后，接下来，分别执行如下命令，pip install 来安装书本中代码用到的其它软件包。  
 到此，环境搭建完毕。

## 执行jupyter notebook

切换到刚才解压文件所在的目录，然后执行如下两条命令来激活gluon环境和打开jupyter notebook：

```text
conda activate gluon
jupyter notebook
```

## 数据操作NDArray

深度学习中有一个概念`向量化`，向量化是非常基础的去除代码中for循环的艺术（相比for循环运算，向量化真的是快了太多）。  
 这次的NDArray与之前有使用过NumPy感觉两者类似，都是为了深度学习中大量的矩阵运算而创建的，即通过numpy内置函数和避开显式的循环\(loop\)的方式进行向量化，从而有效提高代码速度。在以往的实验中，我一般用来进行数据集预处理，制作混淆矩阵等。在此就不过多叙述，基本上就按书上的走了一遍，复习了一下相关的知识。

