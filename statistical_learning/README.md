# **统计学习方法**
## **第1章&nbsp;&nbsp;统计学习及监督学习概述**

<br>

**导论：**
- 1.1节叙述统计学习或机器学习的定义、研究对象与方法；
- 1.2节叙述统计学习的分类，基本分类是监督学习、无监督学习、强化学习；
- 1.3节叙述统计学习方法的三要素；模型、策略和算法；
- 1.4节至1.7节相继介绍监督学习的几个重要概念，包括模型评估与模型选择、正则化与交叉验证、学习的泛化能力、生成模型与判别模型；
 - 1.8节介绍监督学习的应用：分类问题，标注问题与回归问题。

<center>

![](./pic/Fig1.png ':size=90%')

</center>

<center>总体学习框架图</center>


### **1.1&nbsp;&nbsp;统计学习**

#### **1.&nbsp;&nbsp;统计学习特点**
（1）统计学习以计算机及网络为平台，是建立在计算机及网络上的；\
（2）统计学习以数据为研究对象，是数据驱动的学科；\
（3）统计学习的目的是对数据进行预测与分析；\
（4）统计学习以方法为中心，统计学习方法构建模型并应用模型进行预测与分析；\
（5）统计学习是概率论、统计学、信息论、计算理论、最优化理论及计算机科学等多个领域的交叉学科，并且在发展中逐步形成独自的理论体系与方法论。
#### **2.&nbsp;&nbsp;统计学习的对象**
数据。
#### **3.&nbsp;&nbsp;统计学习的目的**
统计学习用于对数据的预测与分析，特别是对**未知新数据**的预测与分析。对数据的预测与分析是通过构建概率统计模型实现的。统计学习总的目标就是考虑学习什么样的模型和如何学习模型，以使模型能对数据进行准确的预测与分析，同时也要考虑尽可能地提高学习效率。
#### **4.&nbsp;&nbsp;统计学习的方法**

统计学习的方法是基于数据构建概率统计模型从而对数据进行预测与分析。统计学习由监督学习（supervised learning）、无监督学习（unsupervised learning）和强化学习（reinforcement learning） 等组成。

统计学习方法可以概括如下：
- 从给定的、有限的、用于学习的训练数据（training data）集合出发，假设数据是独立同分布产生的；
- 并且假设要学习的模型属于某个函数的集合，称为假设空间（hypothesis space）；
- 应用某个评价准则（evaluation criterion），从假设空间中选取一个最优模型，使它对己知的训练数据及未知的测试数（test data）在给定的评价准则下有最优的预测，最优模型的选取由算法实现。
- 这样，统计学习方法包括模型的假设空间、模型选择的准则以及模型学习的算法。称其为统计学习方法的三要素，简称为模型 （model）、策略 （strategy）和算法（algorithm）。

实现统计学习的步骤：
1. 得到一个有限的训练数据集合（训练集）
2. 确定模型的假设空间，也就是所有备选模型（模型结构）
3. 确认模型学习的准则，即学习的策略（**怎么学习，设计cost funtion？**）
4. 实现求解最优模型的算法（**如何求解，优化器？**）
5. 通过学习方法选择最优模型
6. 利用学习的最优模型对新数据进行预测或分析（预测）

### **1.2&nbsp;&nbsp;统计学习的分类**

<center>

![](./pic/Fig2.png ':size=90%')

</center>

<center>统计学习的分类总体框架图</center>


#### **1.2.1 基本分类**
1. **监督学习**
> 监督学习 (supervised learning) 是指从标注数据中学习预测模型的机器学习问题。标注数据表示输入输出的对应关系，预测模型对给定的输入产生相应的输出。监督学习的本质是学习输入到输出的映射的统计规律。

- **输入空间与输出空间**
> 在监督学习中，将输入与输出所有可能取值的集合分别称为输入空间 (input space) 与输出空间 (output space) 。输入与输出空间可以是有限元素的集合，也可以是整个欧氏空间。输入空间与输出空间可以是同一个空间，也可以是不同的空间;但通常输出空间远远小于输入空间。

- **特征空间**
> 每个具体的输入是一个实例(instance) ，通常由特征向量 (feature vector) 表示。这时，所有特征向量存在的空间称为特征空间 (feature space) 。特征空间的每一维对应于 个特征。有时假设输入空间与特征空间为相同的空间，对它们不予区分；有时假设输入空间与特征空间为不同的空间，将实例从输入空间映射到特征空间。模型实际上都是定义在特征空间上的。

在监督学习中，将输入与输出看作是定义在输入(特征〉空间与输出空间上的随机变量的取值。输入输出变量用大写字母表示，习惯上输入变量写作$X$输出变量写$Y$。输入输出变量的取值用小写字母表示，输入变量的取值写作$x$输出变量的取值写作$Y$。变量可以是标量或向量，都用相同类型字母表示。除特别声明外，向量均为列向量 。输入实例$x$的特征向量记作

$$x=(x^{(1)},x^{(2)},x^{(3)},...,x^{(n)}) ^T$$

$x^{(i)}$表示$x$的第$i$个特征。注意$x^{(i)}$与$x_i$ 不同，通常用 $x_i$ 表示多个输入变量中的第$i$个变量，即
$$x=(x^{(1)}_i,x^{(2)}_i,x^{(3)}_i,...,x^{(n)}_i) ^T$$

监督学习从训练数据 (training data) 合中学习模型，对测试数据 (test data) 进行预测。训练数据由输入(或特征向量)与输出对组成，训练集通常表示为
$$T=\{(x_1,y_1),(x_1,y_1),(x_1,y_1),...,(x_N,y_N)\}$$
测试数据也由输入与输出对组成 输入与输出对又称为样本 (sample) 或样本点。


监督学习利用训练数据集学习一个模型，再用模型对测试样本集进行预测。由于在这个过程中需要标注的训练数据集，而标注的训练数据集往往是人工给出的 ，所以称为监督学习。监督学习分为学习和预测两个过程，由学习系统与预测系统完成，可用下图表示。

<center>

![](./pic/Fig3.png ':size=50%')

</center>


监督学习分为学习和预测两个过程，由学习系统与预测系统完成。在学习过程中，学习系统利用给定的训练数据集，通过学习(或训练)得到一个模型，表示为条件概率分布$\hat{P}(Y|X)$或决策函数$Y=\hat{f}(X)$。条件概率分布$\hat{P}(Y|X)$或决策函数$Y=\hat{f}(X)$描述输入与输出随机变量之间的映射关系。在预测过程中，预测系统对于给定的测试样本集中的输入$x_{N+1}$由模型$y_{N+1}=argmax_y\hat{P}(y|x_{N+1})$或$y_{N+1}=\hat{f}(y|x_{N+1})$给出相应的输出$y_{N+1}$。

1. **无监督学习**

> 无监督学习(unsupervised learning) 是指从无标注数据中学习预测模型的机器学习问题。无标注数据是自然得到的数据，预测模型表示数据的类别、转换或概率。

无监督学习的本质是学习数据中的统计规律或潜在结构。模型的输入与输出的所有可能取值的集合分别称为输入空间与输出空间。输入空间与输出空间可以是有限元素集合，也可以是欧氏空间。每个输入是一个实例，由特征向量表示。每一个输出是对输入的分析结果，由输入的类别、转换或概率表示。模型可以实现对数据的聚类、降维或概率估计。

假设$\chi$是输入空间，$\Zeta$是隐式结构空间 。要学习的模型可以表示为函数$z=g(X)$条件概率分布 $P(z|x)$ 或者条件概率分布 $P(x|z)$ 的形式，其中$x\in\chi$是输入，$y_i\in {\rm Y}$是输出。包含所有可能的模型的集合称为假设空间。无监督学习旨在从假设空间中选出在给定评价标准下的最优模型。

无监督学习通常使用大量的无标注数据学习或训练，每个样本是一个实例。训练数据表示为$U=\{x_1,x_2,...,x_N\}$，其中$x_i,i=1,2,...,N$是样本。

无监督学习可以用于对己有数据的分析，也可以用于对未来数据的预测。分析时使用学习得到的模型，即函数 $z = \hat g(x)$ 条件概率分布$\hat P(z|x)$或者条件概率分布 $\hat P(x|z)$ 。预测时，和监督学习有类似的流程。在学习过程中，学习系统从训练数据集学习，得到一个最优模型，表示为函数 $Z=\hat g(x)$ 条件概率分布$\hat P(z|x)$ 或者条件概率分布$\hat P(z|x)$ 。在预测过程中，预测系统对于给定的输入$ x_{N+l}$，由模型$Z_{N+l} = \hat g(X_{N+1})$或$ Z_{N+1} = argmax_z\hat P(z|x_{N+1})$ 给出相应的输出$z_{N+1}$进行聚类或降维，或者由模型$\hat P(x|z)$给出输入的概率$\hat P(x_{N+1}|z_{N+1})$进行概率估计。



<center>

![](./pic/Fig4.png ':size=50%')

</center>

1. **强化学习**

2. **半监督学习与主动学习**

半监督学习 (semi-supervised learning) 是指利用标注数据和未标注数据学习预测模型的机器学习问题。通常有少量标注数据、大量未标注数据，因为标注数据的构建往往需要人工，成本较高，未标注数据的收集不需太多成本。半监督学习旨在利用未标注数据中的信息，辅助标注数据，进行监督学习，以较低的成本达到较好的学习效果。

主动学习 (active learning) 是指机器不断主动给出实例让教师进行标注，然后利用标注数据学习预测模型的机器学习问题。通常的监督学习使用给定的标注数据，往往是随机得到的 ，可以看作是"被动学习" 主动学习的目标是找出对学习最有帮助的实例让教师标注，以较小的标注代价，达到较好的学习效果。

#### **1.2.2 按照模型分类**

1. **概率模型与非概率模型**

在监督学习中，概率模型取条件概率分布形式 $P(y|x)$，非概率模型取函数形式 $y=f(x)$ 其中$x$是输入，$y$是输出。在无监督学习中，概率模型取条件概率分布形式 $P(z|x)$或 $P(x|z)$，非概率模型取函数形式 $z = g(x)$，其中$x$是输入，$z$是输出。在监督学习中，概率模型是生成模型，非概率模型是判别模型。


<center>

![](./pic/Fig5.png ':size=50%')

</center>

条件概率分布$P(y|x)$和函数$y = f(x)$ 可以相互转化(条件概率分布$ P(z|x)$函数 $z = g(x)$ 同样可以) 。具体地，条件概率分布最大后得到函数，函数归一化后得到条件概率分布。

所以，概率模型和非概率模型的区别不在于输入与输出之间的映射关系，而在于模型的内在结构。概率模型一定可以表示为联合概率分布的形式，其中的变量表示输入、输出、隐变量甚至参数。而针对非概率模型则不一定存在这样的联合概率分布。

概率模型的代表是概率图模型 (probabilistic graphical model) ，概率图模型是联合概率分布由有向图或者无向图表示的概率模型，而联合概率分布可以根据图的结构分解为因子乘积的形式。贝叶斯网络、马尔可夫随机场、条件随机场是概率图模型。无论模型如何复杂，均可以用最基本的加法规则和乘法规则进行概率推理。

$$加法规则: P(x)=\sum_{y}^{}P(x,y) $$
$$乘法规则: P(x,y)=P(y|x)P(x) $$

1. **线性模型与非线性模型**

统计学习模型，特别是非概率模型，可以分为线性模型(linear mode)和非线性模型 (non-linear model) 。如果函数 $f(x) = g(x)$或$z = g(x)$ 是线性函数，则称模型是线性模型，否则称模型是非线性模型。


<center>

![](./pic/Fig6.png ':size=50%')

</center>

1. **参数化模型与非参数化模型**

统计学习模型又可以分为参数化模型 (parametric model)和非参数化模型 (nonparametric model)。参数化模型假设模型参数的维度固定，模型可以由有限维参数完全刻画:非参数化模型假设模型参数的维度不固定或者说无穷大，随着训练数据量的增加而不断增大。


<center>

![](./pic/Fig7.png ':size=50%')

</center>


#### **1.2.3 按算法分类**

统计学习根据算法，可以分为在线学习 (online learning) 与批量学习 (batch learning) 。在线学习是指每次接受一个样本，进行预测，之后学习模型，并不断重复该操作的机器学习。与之对应，批量学习次接受所有数据，学习模型，之后进行预测。有些实际应用的场景要求学习必须是在线的。比如，数据依次达到无法存储，系统需要及时做出处理:数据规模很大，不可能 次处理所有数据:数据的模式随时间动态变化，需要算法快速适应新的模式(不满足独立同分布假设)。

在线学习可以是监督学习，也可以是无监督学习，强化学习本身就拥有在线学习的特点。以下只考虑在线的监督学习。

学习和预测在一个系统，每次接受一个输入$x_t$，用己有模型给出预测$\hat f(x_t)$之后得到相应的反馈，即该输入对应的输出$y_t$；系统用损失函数计算两者的差异，更新模型；并不断重复以上操作。


<center>

![](./pic/Fig8.png ':size=50%')

</center>

在线学习通常比批量学习更难，很难学到预测准确率更高的模型，因为每次模型更新中，可利用的数据有限。

#### **1.2.4 按技巧分类**

1. **贝叶斯学习**

贝叶斯学习 (Bayesian learning) ，又称为贝叶斯推理(Bayesian inference) ，是统计学、机器学习中重要的方法。其主要想法是，在概率模型的学习和推理中，利用贝叶斯定理，计算在给定数据条件下模型的条件概率，即后验概率，并应用这个原理进行模型的估计，以及对数据的预测。将模型、未观测要素及其参数用变量表示，使用模型的先验分布是贝叶斯学习的特点。贝叶斯学习中也使用基本概率公式，朴素贝叶斯、潜在狄利克雷分配的学习属于贝叶斯学习。

假设随机变量$D$表示数据，随机变量$\theta $表示模型参数。根据贝叶斯定理，可以用以下公式计算后验概率 $P(\theta |D)$:
$$P(\theta |D)=\frac{P(\theta )P(D|\theta )}{P(D)}$$

其中，$P(\theta )$是先验概率，$P(D|\theta )$是似然函数。

模型估计时，估计整个后验概率分布 $P(\theta|D)$。如果需要给出一个模型，通常取后验概率最大的模型。

预测时，计算数据对后验概率分布的期望值:
$$P(x|D)=\int P(x|\theta ,D)P(\theta |D)d\theta $$

贝叶斯估计与极大似然估计在思想上有很大的不同，代表着统计学中频率学派和贝叶斯学派对统计的不同认识。其实，可以简单地把两者联系起来，假设先验分布是均匀分布，取后验概率最大，就能从贝叶斯估计得到极大似然估计。

<center>

![](./pic/Fig9.png ':size=60%')

</center>

1. **核方法**

核方法 (kernel method) 是使用核函数表示和学习非线性模型的一种机器学习方法，可以用于监督学习和无监督学习。有一些线性模型的学习方法基于相似度计算，更具体地，向量内积计算。核方法可以把它们扩展到非线性模型的学习，使其应用范围更广泛。

把线性模型扩展到非线性模型，直接的做法是显式地定义从输入空间(低维空间)到特征空间(高维空间)的映射，在特征空间中进行内积计算，比如，支持向量机，把输入空间的线性不可分问题转化为特征空间的线性可分问题。核方法的技巧在于不显式地定义这个映射，而是直接定义核函数，即映射之后在特征空间的内积。这样可以简化计算，达到同样的效果。

假设 $X_1$和$X_2$是输入空间的任意两个实例(向量) ，其内积是 $\left \langle  X_1 ,X_2 \right \rangle$ 。假设从输入空间到特征空间的映射是$\varphi $，于是$ X_1$与$ X_2$ 在特征空间的映像是 $\varphi (X_1)$与$\varphi (X_2)$ ,其内积是$\left \langle \varphi ( X_1) ,\varphi (X_2) \right \rangle$。核方法直接在输入空间中定义核函数 $K(X_1 ,X_2)$ 使其满足$K(X_1 ,X_2)=\left \langle \varphi ( X_1) ,\varphi (X_2) \right \rangle$。

### **1.3&nbsp;&nbsp;统计学习方法的三要素**

统计学习方法都是由模型、策略和算法构成的，即统计学习方法由三要素构成，可以简单地表示为:

$$方法=模型+策略+算法$$

1. **模型**

统计学习首要考虑的问题是学习什么样的模型。在监督学习过程中，模型就是所要学习的条件概率分布或决策函数。模型的假设空间 (hypothesis space) 包含所有可能的条件概率分布或决策函数。例如，假设决策函数是输入变量的线性函数，那么模型的假设空间就是所有这些线性函数构成的函数集合。假设空间中的模型一般有无穷多个。

假设空间用$\mathcal{F} $表示。假设空间可以定义为决策函数的集合:
$$\mathcal{F} = \{f|Y=\textit{f}(X)\}$$
其中，$X$和$Y$是定义在输入空间$\mathcal{X}$和输出空间$\mathcal{Y}$上的变量。这时$\mathcal{F} $通常是由一个参数向量决定的函数族：
$$\mathcal{F}=\{f|Y=\textit{f}_{\theta}(X),\theta \in \mathbf{R}^{n}\}$$

参数向量$\theta$取值于$\textit{n}$维欧氏空间$\mathbf{R}^{n}$称为参数空间 (parameter space)。

假设空间也可以定义为条件概率的集合:
$$\mathcal{F}=\{P|P(Y|X)\}$$
其中，$X$和$Y$是定义在输入空间$\mathcal{X}$和输出空间$\mathcal{Y}$上的变量。这时$\mathcal{F} $通常是由一个参数向量决定的条件概率分布族：
$$\mathcal{F}=\{P|P_{\theta}(Y|X) ,\theta\in \mathbf{R}^{n}\}$$

参数向量$\theta$取值于$\textit{n}$维欧氏空间$\mathbf{R}^{n}$称为参数空间。

2. **策略**

有了模型的假设空间，统计学习接着需要考虑的是按照什么样的准则学习或选择最优的模型。统计学习的目标在于从假设空间中选取最优模型。

首先引入损失函数与风险函数的概念。损失函数度量模型一次预测的好坏，风险函数度量平均意义下模型预测的好坏。


监督学习问题是在假设空间$\mathcal{F}$中选取模型$f$作为决策函数，对于给定的输入$X$ 给出相应的输出$\hat{Y}=f(X)$，这个输出的预测值$f(X)$ 与真实值$Y$可能一致也可能不一致，用 个损失函数(loss function) 或代价函数 (cost function) 来度量预测错误的
程度。损失函数是 $f(X)$和$Y$ 的非负实值函数，记作 $L(Y,f(X))$。


**常见损失函数：**

- 0-1损失函数
$$
L(Y,f(X))=\left\{\begin{matrix}
  1,& Y\ne f(X)\\
  0,& Y=f(X)
\end{matrix}\right. 
$$

- 平方损失函数
$$
L(Y,f(X))=(Y-f(X))^2
$$

- 绝对损失函数
$$
L(Y,f(X))=|Y-f(X)|
$$
- 对数损失函数、对数似然损失函数
$$
L(Y,P(Y|X))=-logP(Y|X)
$$

损失函数值越小，模型就越好。由于模型的输入、输出 $(X,Y)$ 是随机变量，遵循联合分布$P(X,Y)$所以损失函数的期望是:

$$
\mathcal{R}_{exp}(f)=E_P[L(Y,f(X))]\\
=\int _{\mathcal{X}\times \mathcal{Y}}L(y,f(x))P(x,y)dxdy
$$

这是理论上模型 $f(X)$ 关于联合分布 $P(X,Y)$ 的平均意义下的损失，称为风险函数(risk function) 或期望损失 (expected loss)。

学习的目标就是选择期望风险最小的模型。由于联合分布 $P(X,Y)$ 是未知的，$R_{exp}(f)$不能直接计算。实际上，如果知道联合分布$P(X|Y)$可以从联合分布直接求出条件概率分布$P(Y|X)$也就不需要学习了。正因为不知道联合概率分布，所以才需要进行学习。这样一来，一方面根据期望风险最小学习模型要用到联合分布，另一方面联合分布又是未知的，所以监督学习就成为 个病态问题 (ill-formed problem)。

给定一个训练数据集
$$
T=\{(x_1,y_1),(x_2,y_2),...,(x_N,y_N)\}
$$
模型 $f(X)$ 关于训练数据集的平均损失称为经验风险 (empirical risk) 或经验损
(empirical loss) ，记作 $\mathcal{R}_{emp}$：
$$
\mathcal{R}_{emp}(f)=\frac{1}{N}\sum_{i=1}^{N}L(y_i,f(x_i))  
$$
期望风险$\mathcal{R}_{exp}(f)$是模型关于联合分布的期望损失，经验风险$\mathcal{R}_{emp}(f)$是模型关于训练样本集的平均损失。根据大数定律 当样本容量 趋于无穷时，经验风险$\mathcal{R}_{emp}(f) $趋于期望风险$\mathcal{R}_{exp}(f)$。所以 很自然的想法是用经验风险估计期望风险。
但是，由于现实中训练样本数目有限，甚至很小，所以用经验风险估计期望风险常常井不理想，要对经验风险进行一定的矫正。这就关系到监督学习的两个基本策略：经验风险最小化和结构风险最小化。

- 经验风险最小化
$$
min_{f\in \mathcal{F}} \frac{1}{N}\sum_{i=1}^{N}L(y_i,f(x_i))  
$$

- 结构风险最小化
$$
min_{f\in \mathcal{F}} \frac{1}{N}\sum_{i=1}^{N}L(y_i,f(x_i))+\lambda J(f)
$$

其中 $J(f)$ 为模型的复杂度，模型$f$越复杂，复杂度$J(f)$ 就越大:反之，模型$f$越简单，复杂度$J(f)$就越小。也就是说，复杂度表示了对复杂模型的惩罚。$\lambda$是系数，用以权衡经验风险和模型复杂度，结构风险小需要经验风险与模型复杂度同时小。结构风险小的模型往往对训练数据以及未知的测试数据都有较好的预测。


3. **算法**

- 神经网络的优化器

算法是指学习模型的具体计算方法。统计学习基于训练数据集，根据学习策略，从假设空间中选择最优模型，最后需要考虑用什么样的计算方法求解最优模型。这时，统计学习问题归结为最优化问题，统计学习的算法成为求解最优化问题的
算法。如果最优化问题有显式的解析解，这个最优化问题就比较简单。但通常解析解不存在，这就需要用数值计算的方法求解。如何保证找到全局最优解，并使求解的过程非常高效，就成为一个重要问题。统计学习可以利用己有的最优化算法，有时也需要开发独自的最优化算法。



### **1.4&nbsp;&nbsp;模型评估与模型选择**

|评价|  训练集准确率   | 测试集准确率 |
| :-:   |  :-:    | :-:   |
|欠拟合| 低  | - |
|过拟合|高  | 低 |
|最佳|高  | 高 |

过拟合：当选择的模型复杂度过大时，过拟合现象就会发生。这样，在学习时就要防止过拟合，进行最优的模型选择，即选择复杂度适当的模型，以达到使测试误差最小的学习目的。

### **1.5&nbsp;&nbsp;正则化与交叉验证**

1. **正则化**

模型选择的典型方法是正则化 (regularization) 。正则化是结构风险最小化策略的实现，是在经验风险上加 个正则化项 (regularizer )或罚项 (penalty term) 。正则化项一般是模型复杂度的单调递增函数，模型越复杂，正则化值就越大。比如，正则化项可以是模型参数向量的范数。

正则化 般具有如下形式:
$$
min_{f\in \mathcal{F}} \frac{1}{N}\sum_{i=1}^{N}L(y_i,f(x_i))+\lambda J(f)
$$

可以取$L_1$范数：

$$
L(\textit{W})= \frac{1}{N}\sum_{i=1}^{N}L(y_i,f(x_i))+\lambda|\textit{W}|
$$

或$L_2$范数：
$$
L(\textit{W})= \frac{1}{N}\sum_{i=1}^{N}L(y_i,f(x_i))+\frac{\lambda}{2}||\textit{W}||^2
$$

正则化符合奥卡姆剃刀 (Occam's razor) 原理。奥卡姆剃刀原理应用于模型选择时变为以下想法:在所有可能选择的模型中，能够很好地解释己知数据并且十分简单才是最好的模型，也就是应该选择的模型。从贝叶斯估计的角度来看，正则化项对于模型的先验概率。可以假设复杂的模型有较小的先验概率，简单的模型有较大的先验概率。

2. **交叉验证**

如果给定的样本数据充足，进行模型选择的 种简单方法是随机地将数据集切分成三部分，分别为训练集(training set) 、验证集 (validation set) 和测试集 (test set) 。训练集用来训练模型，验证集用于模型的选择，而测试集用于最终对学习方法的评估。

- 简单交叉验证

简单交叉验证方法是:首先随机地将己给数据分为两部分，部分作为训练集，另一部分作为测试集(例如，70%的数据为训练集，30% 的数据为测试集)；然后用训练集在各种条件下(例如，不同的参数个数)训练模型，从而得到不同的模型；在测试集上评价各个模型的测试误差，选出测试误差最小的模型。

-  $S$折交叉验证

应用最多的是$S$折交叉验证(S-fold cross validation)，方法如下：首先随机地将已给数据切分为$S$个互不相交、大小相同的子集；然后利用$S-1$个子集的数据训练模型，利用余下的子集测试模型；将这一过程对可能的$S$种选择重复进行；最后选出$S$次评测中平均测试误差最小的模型。

- 留一交叉验证

折交叉验证的特殊情形是$S=N$称为留一交叉验证(Leave-one-out cross validation)，往往在数据缺乏的情况下使用。这里$N$是给定数据集的容量。

### **1.6&nbsp;&nbsp;泛化能力**
**\***

### **1.7&nbsp;&nbsp;生成模型与判断模型**
监督学习的任务就是学习一个模型，应用这一模型，对给定的输入预测相应的输出。这一个模型的一般形式为决策函数:

$$Y=f(X)$$
或者条件概率分布:
$$P(Y|X)$$

监督学习方法又可以分为生成方法 (generative approach) 和判别方法 (discrimine active approach) 所学到的模型分别称为生成模型(generative model)和判别模型(discriminative model)。


生成方法由数据学习联合概率分布 $P(X|Y)$，然后求出条件概率分布$P(Y|X)$为预测的模型，即生成模型:

$$P(Y|X)=\frac{P(X,Y)}{P(X)} $$

这样的方法之所以称为生成方法，是因为模型表示了给定输入$X$产生输出$Y$的生成关系。


在监督学习中，生成方法和判别方法各有优缺点，适合于不同条件下的学习问题。

生成方法的特点：生成方法可以还原出联合概率分布 $P(X|Y)$ 而判别方法则不能；生成方法的学习收敛速度更快，即当样本容量增加的时候，学到的模型可以更快地收敛于真实模型；当存在隐变量时，仍可以用生成方法学习，此时判别方法就不
能用。

判别方法的特点：判别方法直接学习的是条件概率$P(Y|X)$或决策函数$f(X)$直接面对预测，往往学习的准确率更高:由于直接学习 $P(Y|X)$或$ f(X)$ 可以对数据进行各种程度上的抽象、定义特征并使用特征，因此可以简化学习问题。

### **1.8&nbsp;&nbsp;监督学习应用**

|种类|  分类问题   | 回归问题 |
| :-:   |  :-:    | :-:   |
|预测类型| 预测类别 | 预测数值 |


**评价指标：**
<table >
    <tr>
        <td></td> 
        <td></td> 
        <td></td> 
   </tr>
    <tr>
        <td rowspan="2" align="center">真实情况</td>    
  	<td colspan="2" align="center">预测结果</td>
    </tr>
    <tr>
        <td align="center">正例</td> 
        <td align="center">反例</td>    
    </tr>
    <tr>
        <td align="center">正例</td> 
        <td align="center">TP（真正例）</td> 
        <td align="center">FN（假反例）</td> 
   </tr>
   <tr>
        <td align="center">反例</td> 
        <td align="center">FP（假正例）</td> 
        <td align="center">FN（真反例）</td> 
   </tr>
   
</table>

查准率$P$与查全率$R$分别定义为:
$$P=\frac{TP}{TP+FP}$$
$$R=\frac{TP}{TP+FN}$$

查准率和查全率是一对矛盾的度量，一般来说，查准率高时，查全率往往偏低；而查全率高时，查准率往往偏低。例如,若希望将好瓜尽可能多地选出来则可通过增加选瓜的数量来实现，如果将所有西瓜都选上，那么所有的好瓜也必然都被选上了，但这样查准率就会较低；若希望选出的瓜中好瓜比例尽可能高，则可只挑选最有把握的瓜，但这样就难免会漏掉不少好瓜，使得查全率较低.通常只有在一些简单任务中，才可能使查全率和查准率都很高。

## **第2章&nbsp;&nbsp;感知机**

感知机 (perceptron) 类分类的线性分类模型，其输入为实例的特征向量，输出为实例的类别，取 +1 和-1 二值。感知机对应于输入空间(特征空间)中将实例划分为正负两类的分离超平面，属于判别模型。

### **2.1&nbsp;&nbsp;感知机模型**


假设输入空间(特征空间)是 $\mathcal{X} \subseteq \mathcal{R}^n$输出空间是
y = {+1,-1} 。输$x\in \mathcal{X} $表示实例的特征向量，对应于输入空间(特征空间)的点;
输出$y\in \mathcal{Y}$表示实例的类别，由输入空间到输出空间的如下函数:

$$f(x)=sign(w \cdot x + b)$$

称为感知机。其中，$w$和$b$为感知机模型参数， $w\in \mathcal{R}^n$叫作权值 (weight) 或权值向量(weight vector)，$b\in \mathcal{R}$叫作偏置( bias )的内积 $sign$ 是符号函数，即
$$sign(x)=\left\{\begin{matrix}
+1,  & x>=0 \\
-1,  & x<0
\end{matrix}\right.$$



<center>

![](./pic/Fig10.png ':size=40%')

</center>

对应于特征空间 $\mathcal{R}^n$ 中的一个超平面$S$，其中$w$是超平面的法向量，$b$是超平面的截距。这个超平面将特征空间划分为两个部分。位于两部分的点(特征向量)分别被分为正、负两类。因此，超平面 称为分离超平面 (separating hyperplane)，如上图。

感知机学习，由训练数据集(实例的特征向量及类别)
$$T=\{(x_1,y_1),(x_2,y_2),...,(x_N,y_N)\}$$

其中$X_i\in \mathcal{X}, y_i\in \mathcal{Y}=\{+1,-1\},i=1,2,3,..,N$求得感知机模型,即求得模型参数$w$和$b$。感知机预测，通过学习得到的感知机模型，对于新的输入实例给出其对应的输出类别。

### **2.2&nbsp;&nbsp;感知机学习策略**

假设数据集线性可分，感知机学习的目标是求得一个能够将训练集正实例点和负实例点完全正确分开的分离超平面。为了找出这样的超平面，即确定感知机模型参数$w$与$b$ ，需要确定一个学习策略，即定义(经验)损失函数并将损失函数极小化。

损失函数选择是误分类点到超平面$S$的总距
离，这是感知机所采用的。为此，

首先写出输入空间$\mathcal{R}^n$中任一点$x_0$到超平面$S$距离:
$$\frac{1}{||w||}|w\cdot x_0+b|$$
其中，$||w||$是$w$的$L_2$范数。

其次，对于误分类的数据 $(x_i,y_i)$来说，

$$-y_i(w\cdot x_i+b)>0$$

成立。因为当$w\cdot x_i + b > 0$时，$y_i=-1$；而当$w \cdot x_i+b <0$时，$ y_i = +1$。因此，分类点 $x_i$ 到超平面 $S$ 的距离是
$$-\frac{1}{||w||}y_i(w\cdot x_0+b)$$

这样，假设超平面$S$的误分类点集合为$M$那么所有误分类点到超平面$S$的总距离为


$$-\frac{1}{||w||}\sum_{x_i\in M} (w\cdot x_0+b)$$
不考虑$\frac{1}{||w||}$，就得到感知机学习的损失函数。

给定训练数据集
$$T=\{(x_1,y_1),(x_2,y_2),...,(x_N,y_N)\}$$

其中$X_i\in \mathcal{X}, y_i\in \mathcal{Y}=\{+1,-1\},i=1,2,3,..,N$。感知机 $sign(w \cdot x/ + b)$学习的损失函数定义为

$$L(w,b)=-\sum_{x_i\in M} (w\cdot x_i+b)$$
其中$M$为误分类点的集合。这个损失函数就是感知机学习的经验风险函数。

### **2.3&nbsp;&nbsp;感知机学习算法**

感知机学习问题转化为求解损失函数式 (2 .4)的最优化问题，最优化的方法是随机梯度下降法。<!--本节叙述感知机学习的具体算法，包括原始形式和对偶形式，并证明在训练数据线性可分条件下感知机学习算法的收敛性。-->

- 感知机学习算法的原始形式

感知机学习算法是对以下最优化问题的算法。给定训练数据集
$$T=\{(x_1,y_1),(x_2,y_2),...,(x_N,y_N)\}$$

其中$X_i\in \mathcal{X}, y_i\in \mathcal{Y}=\{+1,-1\},i=1,2,3,..,N$，求参数$w$、$b$，使其为以下损失函数极小化问题的解。

$$min_{w,b}L(w,b)=-\sum_{x_i\in M}y_i(w\cdot  x_i+b)$$
其中$M$为误分类点的集合。

感知机学习算法是误分类驱动的，具体采用随机梯度下降法 (stochast gradient descent) 。首先，任意选取一个超平面间$w_0,b_0$，然后用梯度下降法不断地极小化目标函数。极小化过程中不是一次使$M$中所有误分类点的梯度下降，而是一次随机选取一个误分类点使其梯度下降。

假设误分类点集合$M$是固定的，那么损失函数$L(w,b)$的梯度由

$$\bigtriangledown_wL(w,b)=-\sum_{x_i\in M}y_ix_i$$
$$\bigtriangledown_bL(w,b)=-\sum_{x_i\in M}y_i$$

随机选取一个误分类点$(x_i,y_i)$，对$w,b$进行更新:
$$w\longleftarrow w+\eta y_i x_i$$
$$b\longleftarrow b+\eta y_i$$

式中 $\eta(0<\eta<=1)$是步长，在统计学习中又称为学习率(learning rate) 。这样，通过迭代可以期待损失函数$L(w,b)$不断减小，直到为0。

## **第3章&nbsp;&nbsp;K近邻法**
K近邻法 (k-nearest neighbor,K-NN) 是一种基本分类与回归方法。这里只讨论分类问题中的K近邻法。近邻法的输入为实例的特征向量，对应于特征空间的点：输出为实例的类别，可以取多类。K近邻法假设给定一个训练数据集，其中的实例类别己定。分类时，对新的实例，根据其k个最近邻的训练实例的类别，通过多数表决等方式进行预测。因此，近邻法不具有显式的学习过程。K近邻法实际上利用训练数据集对特征向量空间进行划分，并作为其分类的“模型”。K值的选择、距离度量及分类决策规则是K近邻法的三个基本要素。
### **3.1&nbsp;&nbsp;K近邻算法**
K近邻算法简单、直观：给定一个训练数据集，对新的输入实例，在训练数据集中找到与该实例最邻近的一个实例，这一个实例的多数属于某个类，就把该输入实例分为这个类。

输入：训练数据集

$$T=\{(x_1,y_1),(x_2,y_2),...,(x_N,y_N)\}$$

其中$X_i\in \mathcal{X}\subseteq R^n$ 为实例特征向量，$y_i\in \mathcal{Y}=\{c_1,c_2,...,c_k\}$为实例的类别，$,i=1,2,3,..,N$；实例特征向量$x$。
输出：实例$x$所属类$y$。

（1）根据给定的距离度量，在训练集$T$中找出与$x$最邻近的$k$个点，涵盖这$k$点的$x$的邻域记作$N_k(x)$；
（2）$N_k(x)$中根据如分类决策规则(如多数表决)决定$x$的类别$y$:
$$y=argmax_{c_j}\sum_{x_i\in N_k(x)}I(y_i=c_j),i=1,2,...,N;j=1,2,...,K$$
公式中，$I$为指示函数，即当$y_i=c_j$时$I$为1，否则$I$为0。

### **3.2&nbsp;&nbsp;K近邻模型**
K近邻法使用的模型实际上对应于对特征空间的划分。模型由三个基本要素——距离度量、k值的选择和分类决策规则决定。

- 模型

K近邻法中，当训练集、距离度量(如欧氏距离)、 值及分类决策规则(如多数表决)确定后，对于任何 个新的输入实例，它所属的类唯 地确定 这相当于根据上述要素将特征空间划分为一些子空间，确定子空间里的每个点所属的类。这一事实从最近邻算法中可以看得很清楚。

特征空间中，对每个训练实例点$x_i$，距离该点比其他点更近的所有点组成一个区域，叫作单元(cell) 每个训练实例点拥有一个单元，所有训练实例点的单元构成对特征空间的一个划分。最近邻法将实例$x_i$的类$y_i$作为其单元中所有点的类标记 (class label) 这样，每个单元的实例点的类别是确定的。
- 距离度量

特征空间中两个实例点的距离是两个实例点相似程度的反映。K近邻模型的特征空间一般是$n$维实数向量空间$R^n$。使用的距离是欧氏距离，但也可以是其他距离，如更一般的$L_p$距离 $(L_p\ distance)$或$Minkowski$距离$(Minkowski\ distance)$。

设特征空间$\mathcal{X}$是$n$维实数向量空间$R^n$，$x+i,x_j\in \mathcal{X}, x_i=(x_i^{(1)},x_i^{(2)},...,x_i^{(n)})^T，x_j=(x_j^{(1)},x_j^{(2)},...,x_j^{(n)})^T，x_i,x_j$的$L_p$距离定义为
$$L_p(x_i,x_j)=(\sum_{l=1}^{n}|x_i^{(l)}-x_j^{(l)}|^p)^{\frac{1}{p}}$$

> 这里$p>=1$。当 $p=2$ 时，称为欧氏距离 (Euclidean distance) ，即

$$L_2(x_i,x_j)=(\sum_{l=1}^{n}|x_i^{(l)}-x_j^{(l)}|^2)^{\frac{1}{2}}$$

> 当 $p=1$ 时，称为曼哈顿距离 (Manhattan distance) ，即

$$L_1(x_i,x_j)=\sum_{l=1}^{n}|x_i^{(l)}-x_j^{(l)}|$$

> 当 $p=\infty$ 时，它是各个坐标距离的最大值 ，即

$$L_\infty(x_i,x_j)=max_l|x_i^{(l)}-x_j^{(l)}|$$

下图给出了二维空间中$p$取不同值时，与原点的 $L_p$距离为1 $L_p=1$ 的点的图形。


<center>

![](./pic/Fig11.png ':size=40%')

</center>


## **第4章&nbsp;&nbsp;朴素贝叶斯**

设输入空间 $\mathcal{X} \subseteq \mathcal{R}^n$为$n$维向量的集合，输出空间为类标记集合$\mathcal{y} = \{c_1,c_2,...,c_K\}$ 。输入为特征向量$x\in \mathcal{X} $，输出为类标记$y\in \mathcal{Y}$。$X$是定义在输入空间$\mathcal{X}$上的随机向量，$Y$是定义在输出空间$\mathcal{Y}$上的随机变量。$P(X,Y)$是$X$和$Y$的联合概率分布。训练集为
$$T=\{(x_1,y_1),(x_1,y_1),(x_1,y_1),...,(x_N,y_N)\}$$
由$P(X,Y)$独立同分布产生。

朴素贝叶斯法通过训练数据集学习联合概率分布$P(X,Y)$ 。具体为，学习以下先验概率分布及条件概率分布。

- 先验概率分布
$$P(Y=c_k), k = 1,2,...,K$$
- 条件概率分布
$$P(X=x|Y=c_k)=P(X^{(1)}=x^{(1)},...,X^{(n)}=x^{(n)}|Y=c_k), k=1,2,...,K$$
于是学习到联合概率分布$P(X,Y)$。

- 概率公式变换

由
$$P(X,Y) = P(X|Y)P(Y) = P(Y|X)P(X)$$
和
$$P(X) = {\textstyle \sum_{Y}}P(X,Y) = {\textstyle \sum_{i=1}^{k}}P(X,y_i),\\
P(Y) = {\textstyle \sum_{X}}P(X,Y)= {\textstyle \sum_{i=1}^{k}}P(x_i,Y) $$


$$\Rightarrow P(Y|X) = \frac{P(X|Y)P(Y)}{P(X)}$$

条件概率分布 $P(X = x|Y = c_k)$ 有指数级数量的参数，其估计实际是不可行的。事实上，假设 $x^{(j)}$ 可取值有$S_j$个，$j = 1, 2,...,n$ ,$Y$可取值有$K$个，那么参数个数为$K\prod_{j=1}^{n} S_j$。

朴素贝叶斯法对条件概率分布作了条件独立性的假设。由于这是一个较强的假设，朴素贝叶斯法也由此得名。具体地，条件独立性假设是
$$P(X=x|Y=c_k)=P(X^{(1)}=x^{(1)},...,X^{(n)}=x^{(n)}|Y=c_k)\\
=\prod_{j=1}^{n}P(X^{(j)}=x^{(j)}|Y=c_k)$$
由于这一假设，模型包含的条件概率的数量大为减少，朴素贝叶斯法的学习与预测大为简化。因而朴素贝叶斯法高效，且易于实现。其缺点是分类的性能不一定很高。
朴素贝叶斯法实际上学习到生成数据的机制，所以属于生成模型 条件独立假设等于是说用于分类的特征在类确定的条件下都是条件独立的。这一假设使朴素贝叶斯法变得简单，但有时会牺牲一定的分类准确率。

朴素贝叶斯法分类时，对给定的输入$x$通过学习到的模型计算后验概率分布$P(Y = c_k|X = x)$ 将后验概率最大的类作为$x$的类输出。后验概率计算根据贝叶斯定理进行:

$$P(Y=c_k|X=x)=\frac{P(X=x|Y=c_k)P(Y=c_k)}{P(X=x)\Rightarrow\sum_{k}P(X=x|Y=c_k)P(Y=c_k)}$$

将输入$x$分到后验概率最大的类$y$。

$$y=\arg \max _{c_{k}} P\left(Y=c_{k}\right) \prod_{j=1}^{n} P\left(X_{j}=x^{(j)} | Y=c_{k}\right)$$


## **第5章&nbsp;&nbsp;决策树模型**

## **第6章&nbsp;&nbsp;逻辑斯谛回归与最大熵模型**
