# 机器学习算法笔记
## 内容提要：
* 学习方法概述
  * 分类学习
  * 集成学习
  * 回归问题
* 机器学习算法
  * 随机森林（RF）
   * ID3决策树
   * C4.5决策树
   * CART决策树
  * 提升决策树（BSTDT）
  * 投票决策树（BAGDT）
  * 决策树比较（Bagging,Boosting,Randomization）
  * 支持向量机(SVM)
  * 朴素贝叶斯（NB）
### 学习方法概述

#### 集成学习
  集成方法是机器学习中的一类算法，其基本思想是构建多个不同的预测模型；此时的预测各个模型之间可以是同质，如：都采用决策树个体分类器，或都采用神经网络个体分类器，此类学习器个体之间有强关联采用算法以`Boosting系列`算法为代表，此类学习器个体之间有弱关联以‘Bagging和RandomForests系列算法’为代表；也可以是异质的，如：个体学习器可以采用支持向量机，逻辑回归，朴素贝叶斯等。<br>  然后将其输出做某种组合作为最终的输出，例如：可以通过对不同预测模型取平均值或采用投票方式来完成对于模型预测结果的集成。</br>
#### 分类学习
#### 回归问题

### 机器学习算法原理
#### 随机森林（RandomForest）
#### 提升决策树（Boosted Decision Tress）
#### 决策树构造比较（Comparison Of Three Methods:Bagging,Boosting,and Randomization）
#### 支持向量机(Support Vector Machines)
#### 朴素贝叶斯（NaiveBayes）

### 附录：
