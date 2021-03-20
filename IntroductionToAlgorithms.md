# IntroductionToAlgorithms



## 第1章 算法在计算中的作用

### 算法

对于给定的输入，有限时间内给出正确的输出。

- **输入**

- **输出**

- **有穷性**

- **确切性**

- **可行性**



## 第2章 算法基础



### 排序

输出为输入序列的一个特定顺序的排列。

排列的元素成为关键字，输入就是关键字的数组。



### 循环不变式

在排序过程中，每一步都保持顺序的一段序列。

- **初始化**：循环的第一次迭代之前，就是真的。
- **保持**：如果在每次循环前是真的，那么下次循环前仍是真的。
- **终止**：循环终止时，仍是真的。



### 插入排序

第 `n` 次循环时，前 `n-1` 个元素组成的序列为**循环不变式**，此次将第 `n` 个按顺序**插入**到前 `n-1` 个中。

````c++
InsertionSort(A)
    for j = 2 to A.length
    	key = A[j]
        // 插入，通过移位的方式执行。
        i=j-1
        while i >0 and A[i]>key
            A[i+1]=A[i]
            i = i-1
        A[i+1] =key
````



### 分治法

 分治法通常可以使用递归结构，三个步骤：

- **分解**：将原问题分解为若干子问题，这些子问题是原问题的规模较小的实例。
- **解决**：对子问题递归求解，子问题较小时，直接求解。
- **合并**：将子问题的解组合成原问题的解。



### 归并排序

分两段，合并，两倍空间。

````c++
Merge(A,p,q,r)
    n1 = q-p+1
    n2 = r-q
    let L[1..n1+1] and R[1..n_2+1] be new arrays
    for i=1 to n1
        L[i]=A[p+i-1]
    for j=1 to n2
        R[j]=A[p+j-1]
    L[n1+1] = +infin
    R[n2+1] = +infin
    i =1 
    j =1
    for k=p to r
        if L[i] <= R[j]
            A[k]= L[i]
            i+=1
        else
            A[k]= R[j]
            j+=1
            
MergeSort(A,p,r)
    if p <r
        q = (p+r)/2
        MergeSort(A,p,q)
        MergeSort(A,q+1,r)
        Merge(A,p,q,r)
            
````







## 第3章 函数的增长

### 渐进效率

当输入规模足够大，使得只与运行时间的增长量级有关，即算法的渐进效率，忽略较小的增长量级与常数项。

- $\Theta(g(x)) = \{f(x)|\exist c_1,c_2,n_0 ,\forall n\geq n_0,0\leq c_1g(n)\leq f(n) \leq c_2g(n)\}$  ，渐进紧确界，就是说 $f(x)$ 被 $g(x)$ 夹在了中间。
- $O(g(x)) = \{f(x)|\exist c,n_0 ,\forall n\geq n_0,0\leq  f(n) \leq cg(n)\}$  ，渐进上界，就是说 $f(x)$ 在 $g(x)$ 下面。 $g(x)$ 可能同阶，也可能高阶。
- $\Omega(g(x)) = \{f(x)|\exist c,n_0 ,\forall n\geq n_0,0 \leq cg(n)\leq  f(n)\}$  ，渐进下界，就是说 $f(x)$ 在 $g(x)$ 上面。 $g(x)$ 可能同阶，也可能低阶。
- $o(g(x)) = \{f(x)|\exist c,n_0 ,\forall n\geq n_0,0\leq  f(n) < cg(n)\}$  ，非渐进紧确的上界，就是说 $f(x)$ 在 $g(x)$ 下面。 $g(x)$ 高阶。
- $\omega(g(x)) = \{f(x)|\exist c,n_0 ,\forall n\geq n_0,0 \leq cg(n)<  f(n)\}$  ，非渐进紧确的下界，就是说 $f(x)$ 在 $g(x)$ 上面。 $g(x)$ 低阶。



## 第4章 分治策略

 ### 分治法

分治法通常可以使用递归结构，三个步骤：

- **分解**：将原问题分解为若干子问题，这些子问题是原问题的规模较小的实例。
- **解决**：对子问题递归求解，子问题较小时，直接求解。
- **合并**：将子问题的解组合成原问题的解。

在解决问题这步骤中，如果子问题足够大，需要递归求解时，称之为**递归情况**；而子问题足够小，可以直接求解，叫做**基本情况**。



关键点是如何分解成**更小规模**的相同问题。



###  递归式

**递归式通过**更小的输入上的**函数值**来描述一个**函数**。
$$
T(n)=\cases{ \Theta(1) & n=1 \\a T(n/b) + \Theta(n) & n>1 }
$$


### 求解递归式的方法

- **代入法**：猜测一个界，之后用数学归纳法证明其正确性。
- **递归树法**：将递归式转化为一棵树，其节点表示不同层次的递归调用产生的代价。然后采用边界和技术求解递归式。
- **主方法**：解决均分递归式，最常用。



### 最大子数组问题

寻找数组 $A$ 的一个**最大**的**非空连续子数组**。

买卖一次股票以获得最大收益时，将每天的**价格**，**变换**成每天的**涨跌值**，就将问题转化为了最大子数组问题。



递归主要思想是，最大子数组左右边界只有三种情况：

- 全在左面：递归调用
- 全在右面：递归调用
- 跨越中线：从中间向两端找最大值，合并。

````c++
FindMaxCrossingSubarray(A,low,mid,high)
	leftSum = -infin
    sum =0
    for i = min downto low
        sum = sum+A[i]
        if sum>leftSum
           	leftSum = sum
            maxLeft = i
    rightSum = -infin
    sum =0
    for j = mid+1 to high
        sum = sum+A[j]
        if sum>rightSum
           	rightSum = sum
            maxRight = j
    return (maxLeft,maxRight,leftSum+rightSum)
            
FindMaximumSubarray(A,low,high)
    if high == low
        return (low,high,A[low])
    (leftLow,leftHigh,leftSum)=FindMaximumSubarray(A,low,mid)
    (rightLow,rightHigh,rightSum)=FindMaximumSubarray(A,mid+1,high)
    (crossLow,crossHigh,crossSum)=FindMaxCrossingSubarray(A,low,mid,high)
    if leftSum>=rightSum and leftSum >=crossSum
        return (leftLow,leftHigh,leftSum)
    elseif  rightSum>=leftSum and rightSum >=crossSum
    	return (rightLow,rightHigh,rightSum)
    elseif  crossSum>=leftSum and crossSum >=rightSum
    	return (crossLow,crossHigh,crossSum)
        
        
````



### 矩阵乘法 Strassen算法

普通矩阵乘法，使用逐行逐列相乘求和，$O(n^3)$。

普通分治思想，均分四块，分块矩阵乘法，$O(n^3)$。

Strassen算法，均分四块，之后先算10个子矩阵的和，之后再算4个子矩阵与10个和矩阵的7个矩阵乘，之后再把7个矩阵积组合成分块矩阵的正常结果。使用了7次矩阵乘法，而不是普通分块的8次，$O(n^{\lg7})$。

### 带入法求渐进复杂度

根据之前类似结构的算法的渐进效率，估计此算法可能的渐进效率，之后验证。

- 猜测解的形式
- 数学归纳法解出常数，证明正确性。

要选择合适的 $n_0$ ，因为在边界时，很容易出问题。

可以先猜一个比较大的上界，再慢慢缩小。



较强的上界可能会比更较的上界更容易用数学归纳法证明。如 $T(n)= 2T(n/2)+1$ 得到 $T(n)\leq cn$ :

若假设 $T(n)\leq cn$ ，则 $T(n)= 2T(n/2)+1 \leq 2cn/2 +1 = cn+1$ 。无法证明。

若假设 $T(n)\leq cn-d$ ，则 $T(n)= 2T(n/2)+1 \leq 2(cn/2 -d ) +1 = cn-2d+1\leq cn-d$ 。证明。



在证明时，需要证出与归纳假设严格一样的形式，不能合并 $c$ 与常数。如错误证明$T(n)= 2T(n/2)$ 得到 $T(n)\leq cn$ ：$T(n) \leq 2(c[n/2])+n \leq cn +n = O(n)$。

原因在于证出的是$T(n)\leq (c +1 )n$ ，虽然同阶，但不等。实际为$T(n)\leq n\lg(n)$。



可以适当变换变量形式，指数对数变换，方便证明。$T(n) = 2T([\sqrt{n}])+\lg (n)$， $m=\lg n$ ，$S(m)=2S(m/2)+m$ ，$S(m)=O(m \lg m)$， $T(n)=T(2^m)=S(m)=O(m\lg m) = O(\lg n \lg\lg n))$。

### 递归树求渐进复杂度

首先将递归结构展开成树的形式，之后计算每层的复杂度，再求和。用来估计最可能的渐进复杂度，之后用代入法证明。

### 主方法求渐进复杂度

用以求解 $T(n)=aT(n/b)+f(n)$ 型的递归式：

- 若 $f(n)=O(n^{\log_b{a-\epsilon}})$，则 $T(n)=\Theta(n^{\log_b{a}})$
- 若 $f(n)=\Theta(n^{\log_b{a}})$，则 $T(n)=\Theta(n^{\log_b{a}}\lg n)$
- 若 $f(n)=\Omega(n^{\log_b{a+\epsilon}})$，则 $T(n)=\Theta(f(n))$ 

直觉上就是比较递归部分与函数部分的大小。不等则为大的那个；相等则递归树变宽，乘 $\lg n$ 系数。



## 第章



````c++

````



