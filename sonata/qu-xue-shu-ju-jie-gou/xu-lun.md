# 绪论

**数据结构基础知识**

**数据**：所有能输入到计算机中的描述客观事物的符号。

**数据元素**：数据的基本单位，也可称为是节点、记录。

**数据项**：数据的最小单位。

**数据对象**：数据元素的集合，是数据的子集。

**数据结构**：相互之间存在一种或多种特定关系的数据元素的集合，是带“结构”的数据元素的集合。

**逻辑结构和存储结构**：

逻辑结构 是数据元素之间的关系，主要可分为以下三种：

1. 线性结构：一对一，如线性表、栈、队列、数组...
2. 树形结构：一对多关系，典型例子就是树结构。
3. 图形结构：多对多关系，如图、网

⚠️ 逻辑结构与数据的存储结构无关，独立于计算机，它是从具体问题中抽象出来的数学模型。

存储结构 是数据元素及其关系在计算机中的存储方式，主要可分为以下三种：

1. 顺序存储：逻辑上相邻的元素在计算机内的存储位置也是相邻的

   顺序存储采用一段连续的存储空间，将逻辑上相邻的元素存储在连续的空间内，中间不允许有空。

   顺序存储可以快速定位第几个元素的地址，但是插入和删除时需要移动大量元素。

2. 链式存储：逻辑上相邻的元素在计算机内的存储位置不一定是相邻的。

   链式存储就像一个铁链子，一环扣一环才能连在一起。每个节点除了数据域，还有一个指针域，记录下一个元素的存储地址。

3. 散列存储：使用散列函数确定数据元素的存储位置与关键码之间的对应关系。

   假设散列表的地址范围为0～9，散列函数为H\(key\)=key %10。输入关键码序列：（24,10,32,17,41,15,49）

   24%10=4：存储在下标为4的位置。 10%10=0：存储在下标为0的位置。 32%10=2：存储在下标为2的位置。 17%10=7：存储在下标为7的位置。 41%10=1：存储在下标为1的位置。 15%10=5：存储在下标为5的位置。 49%10=9：存储在下标为9的位置。

4. 索引存储：建立附加的索引表来表示节点的地址。

**算法复杂度**

**算法特性**：（选择题/填空题） （1）有穷性：算法是由若干条指令组成的有穷序列，总是在执行若干次后结束，不可能永不停止。 （2）确定性：每条语句有确定的含义，无歧义。 （3）可行性：算法在当前环境条件下可以通过有限次运算实现。 （4）输入和输出：有零个或多个输入，一个或多个输出。

**算法好坏**：

（1）正确性：指算法能够满足具体问题的需求，程序运行正常，无语法错误。 （2）易读性：算法遵循标识符命名规则，简洁、易懂，注释语句恰当、适量。 （3）健壮性：算法对非法数据及操作有较好的反应和处理。 （4）高效性：指算法运行效率高，即算法运行所消耗的时间短。（时间复杂度） （5）低存储性：指算法所需要的存储空间低。（空间复杂度）

**时间复杂度**：

算法运行需要的时间，一般将算法基本运算的执行次数作为时间复杂度的度量标准。

```text
sum=0;   //运行1次￼
total=0;  //运行1次￼
​
//运行n+1次，最后依次判断条件不成立，结束￼  
for(i=1; i<=n; i++) {￼ 
    sum=sum+i;  //运行n次￼   
    for(j=1; j<=n; j++)  //运行n*(n+1)次￼     
        total=total+i＊j;   //运行n*n次￼  
}
```

把算法所有语句的运行次数加起来，即1+1+n+1+n+n×\(n+1\)+n×n，可以用一个函数T\(n\)表达：

$$T\(n\) = 2n^2 + 3n + 3$$

当n足够大时，算法运行时间主要取决于第一项，后面的基本可以忽略不计。

如果有$f\(n\)$能够使得 $ \lim\_{n \to +\infty} \frac{T\(n\)}{f\(n\)} = c$，c是不为0的常数，那么时间复杂度的表示为$O\(f\(n\)\)$。

T\(n\) = $2n^2$, $f\(n\) = n^2$

**语句频度**：语句重复执行的次数。

在计算时间复杂度时，可以只考虑对算法运行时间贡献大的语句，而忽略那些运算次数少的语句。但并不是每个算法都能直接计算运行次数的，此时考虑算法的最坏情况，如冒泡排序。

**空间复杂度**：算法占用的空间大小。一般将算法的**辅助空间**作为衡量空间复杂度的标准。

```text
// 交换两数
swap(int x, int y) {
    int temp;
  temp = x;  // temp为辅助空间 （1）
  x = y;   //（2）
  y = temp;   //（3）
}
```

⚠️ 在递归算法中，每一次递推需要一个栈空间来保存调用记录，因此空间复杂度需要计算递归栈的辅助空间。

```text
// 阶乘递归
// 假设 n = 5
fac(int n) {
  if(n < 0) {
    return -1;
  } else if (n == 0 || n ==1 ) {
    return 1;
  } else {
    return n * fac(n - 1);
  }
}  T(n) = n;
```

#### 本章的内容要点

（1）基本概念：数据、数据元素、数据项和数据结构。 （2）数据结构包含逻辑结构、存储结构和运算三个要素。

（3）时间复杂度的衡量标准及渐近上界符号O\(f \(n\)\)表示。 （4）衡量算法的好坏通常会考查算法的最坏情况。 （5）空间复杂度只计算辅助空间。 （6）递归算法的空间复杂度要计算递归使用的栈空间。

