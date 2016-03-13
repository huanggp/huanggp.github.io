--- 
layout: post
title: "推荐系统公式推导"
date: 2016-03-13 11:22:06 -0700
comments: false
---



直接对评分分数进行建模


考虑基于User 和 Item 的评分值矩阵R

对第i个用户，第j个item 的评分值为$r_{ij}$

考虑这个评分值为用户的隐含特征向量与项目的隐含特征向量的内积


$$r_{ij}=<\mathbf{u_i},\mathbf{m_j}>$$


其中


$$ \mathbf{u_i}=[u_1,u_2,\cdots ,u_k] $$

$$\mathbf{m_i}=[m_1,m_2,\cdots ,m_k]$$


k 为隐含向量的维度

那么这样做之后的只是对原来的评分的一个近似。
在经验风险最小化的原则,可以对有评分的项做误差估计。

==================



这样可以得到一个代价函数


$$ J=\frac{1}{2}min\sum_{i,j \in S} (r_{ij}-<\mathbf{u}_i,\mathbf{m}_j>)^2 $$


这里的S就是有打分的用户和被打分项目的集合，针对评分矩阵中有打分的项，也就是说这个代价函数只在有评分得项目上进行评估
这也就是为什么叫经验风险，只是在样本上建立起来的代价函数，对其他的未观测的样本则属于结构风险。

由于评分矩阵的稀疏性，相当于样本数量极少的情况，那么很容易overfit. 那么需要加上Regularation.
由于考虑到隐含因子的分布为高斯分布，所以采用了L2范数表示

重新定义代价函数


$$ J=\frac{1}{2} \min \sum_{i,j \in S}[(r_{ij}-<\mathbf{u}_i,\mathbf{m}_j>)^2+\lambda(\left \| \mathbf{u}_i \right \|^2+\left \| \mathbf{m}_j \right \|^2)] $$



那么剩下的事情就是优化了

通常的做法就是梯度下降法了，但是由于评分矩阵可能非常大，那么在梯度训练的时候性能会非常低下。
考虑这个优化目标函数的结构，是一个典型的二次优化问题，那么用交替优化的方法迭代，性能会有很大的提升
那么关于用户隐含向量求导


$$ \frac{\partial }{\partial \mathbf{u}_i}J=\sum_{i,j \in S}(r_{ij}-<\mathbf{u}_i,\mathbf{m}_j>)\mathbf{m}_j+\lambda \mathbf{u}_i=0 $$


$$ \frac{\partial }{\partial \mathbf{m}_j}J=\sum_{i,j \in S}(r_{ij}-<\mathbf{u}_i,\mathbf{m}_j>)\mathbf{u}_i+\lambda \mathbf{m}_j=0 $$



那么迭代交替求解出用户i的隐含向量和项目j的隐含向量

求解 $\mathbf{u}_i$ 得到


$$  J=\frac{1}{2} \min \sum_{i \in S_i,j \in S_j}[(r_{ij}-<\mathbf{u}_i,\mathbf{m}_j>)^2+\lambda(\left \| \mathbf{u}_i \right \|^2+\left \| \mathbf{m}_j \right \|^2)] $$


$$   \frac{\partial }{\partial \mathbf{u}_i}J=\sum_{j \in S_j}[-(r_{ij}-<\mathbf{u}_i,\mathbf{m}_j>)\mathbf{m}_j+\lambda \mathbf{u}_i]=0 $$

$$ =\sum_{j \in S_j}[-(r_{ij}-\mathbf{u}_i^T\mathbf{m}_j)\mathbf{m}_j+\lambda \mathbf{u}_i]=0 $$

$$ =\sum_{j \in S_j}[-(r_{ij}\mathbf{m}_j-\mathbf{u}_i^T\mathbf{m}_j\mathbf{m}_j)+\lambda \mathbf{u}_i]=0 $$

$$ =\sum_{j \in S_j}[-(r_{ij}\mathbf{m}_j-\mathbf{m}_j\mathbf{u}_i^T\mathbf{m}_j)+\lambda \mathbf{u}_i]=0 $$

$$ =\sum_{j \in S_j}[-(r_{ij}\mathbf{m}_j-\mathbf{m}_j\mathbf{m}_j^T\mathbf{u}_i)+\lambda \mathbf{u}_i]=0 $$

$$ =\sum_{j \in S_j}[-(r_{ij}\mathbf{m}_j-\mathbf{m}_j\mathbf{m}_j^T\mathbf{u}_i)+\lambda \mathbf{u}_i]=0  $$
 


其中，

第二行，是对$\mathbf{u}_i$取偏导，除了第i项是变量，其他的u都是常数，但是j 需要遍历所有的元素
第三行，是把内积转换为矩阵表示
第五行，是因为内积是一个常数，因此可以与矩阵相乘交换顺序
第六，七行，因为内积的矩阵表示是常数，所以常数的转置仍然是常数


继续推导得到，


$$ \sum_{j \in S_j}[(\mathbf{m}_j\mathbf{m}_j^T\mathbf{u}_i)+\lambda \mathbf{u}_i]=\sum_{j \in S_j}r_{ij}\mathbf{m}_j $$


$$ \sum_{j \in S_j}(\mathbf{m}_j\mathbf{m}_j^T+\lambda I_f )\mathbf{u}_i=\sum_{j \in S_j}r_{ij}\mathbf{m}_j $$
​
