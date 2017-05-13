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
  集成方法是机器学习中的一类算法，其基本思想是构建多个不同的预测模型；此时的预测各个模型之间可以是同质，如：都采用决策树个体分类器，或都采用神经网络个体分类器，此类学习器个体之间有强关联采用算法以`Boosting系列`算法为代表，此类学习器个体之间有弱关联以‘Bagging和RandomForests系列算法’为代表；也可以是异质的，如：个体学习器可以采用支持向量机，逻辑回归，朴素贝叶斯等。然后将其输出做某种组合作为最终的输出，例如：可以通过对不同预测模型取平均值或采用投票方式来完成对于模型预测结果的集成。
  <br></br>
#### 分类学习
#### 惩罚性回归
惩罚性回归方法是由最小二乘法（OLS）衍生出来的。惩罚性回归设计之初的想法是为了克服最小二惩罚的根本缺陷——过拟合。

### 机器学习算法原理
#### 随机森林（RandomForest）
随机森林由LeoBreiman（2001）提出，顾名思义，是用随机的方式建立一个森林，森林里面有很多的决策树组成，随机森林的每一棵决策树之间是没有关联的。具体而言，它通过自助法（bootstrap）重采样技术，从原始训练样本集N中有放回地重复随机抽取k个样本生成新的训练样本集合，然后根据自助样本集生成k个分类树组成随机森林，新数据的分类结果按分类树投票多少形成的分数而定。其实质是对决策树算法的一种改进，将多个决策树合并在一起，每棵树的建立依赖于一个独立抽取的样品，森林中的每棵树具有相同的分布，分类误差取决于每一棵树的分类能力和它们之间的相关性。特征选择采用随机的方法去分裂每一个节点，然后比较不同情况下产生的误差。能够检测到的内在估计误差、分类能力和相关性决定选择特征的数目。单棵树的分类能力可能很小，但在随机产生大量的决策树后，一个测试样品可以通过每一棵树的分类结果经统计后选择最可能的分类。在得到森林之后，当有一个新的输入样本进入的时候，就让森林中的每一棵决策树分别进行一下判断，看看这个样本应该属于哪一类（对于分类算法），然后看看哪一类被选择最多，就预测这个样本为那一类。
<br>在随机森林中，最重要的是如何构造一个随机森林。假设数据样本数为N，那么每棵决策树采样的样本数也就是N，每个样本的属性个数为M，在每个决策树构造过程中，每个节点随机选择m个属性计算最佳分裂方式进行分裂。具体步骤如下:</br> 
* 有放回地随机选择N个样本，用这N个样本来训练一棵决策树;
* 每个样本有M个属性，在决策树中需要分裂节点时，从这M个属性中随机选取m个属性，一般来说m << M，然后从这m个属性中采用某种策略选择最佳属性作为当前节点的分裂属性;
* 每棵决策树的每个节点的分裂都按照步骤（2）迭代进行，直到不能分裂为止;
* 对于每棵决策树都这样建立，就得到了随机森林;
<br>随机森林的随机性体现在每棵树的训练样本是随机的，树中每个节点的分裂属性也是随机选择的。有了这两个随机因素，即使每棵决策树没有进行剪枝，随机森林也不会产生过拟合的现象。随机森林中有两个人为控制参数：森林中树的数量（一般选取值较大）和m值的大小（一般选取为M的平方根）。</br>
<br>随机森林原理是逐步进化而来的，其中ID3树，C4.5树，CART树与之有演进关联，具体实现上Bagging方法和属性随机选择方法结合而来。</br>
##### ID3树
##### C4.5树
##### CART树
##### Scikit-learn库中RT调参
<br>关于决策树的参数：</br>
* criterion: ”gini” or “entropy”(default=”gini”)是计算属性的gini(基尼不纯度)还是entropy(信息增益)，来选择最合适的节点。
* splitter: ”best” or “random”(default=”best”)随机选择属性还是选择不纯度最大的属性，建议用默认。
* max_features: 选择最适属性时划分的特征不能超过此值。
<br>当为整数时，即最大特征数；当为小数时，训练集特征数*小数；</br>
* if “auto”, then max_features=sqrt(n_features).
* If “sqrt”, thenmax_features=sqrt(n_features).
* If “log2”, thenmax_features=log2(n_features).
* If None, then max_features=n_features.
* max_depth: (default=None)设置树的最大深度，默认为None，这样建树时，会使每一个叶节点只有一个类别，或是达到min_samples_split。
* min_samples_split:根据属性划分节点时，每个划分最少的样本数。
* min_samples_leaf:叶子节点最少的样本数。
* max_leaf_nodes: (default=None)叶子树的最大样本数。
* min_weight_fraction_leaf: (default=0) 叶子节点所需要的最小权值
* verbose:(default=0) 是否显示任务进程
<br>关于随机森林特有的参数：</br>
* n_estimators=10：决策树的个数，越多越好，但是性能就会越差，至少100左右（具体数字忘记从哪里来的了）可以达到可接受的性能和误差率。 
bootstrap=True：是否有放回的采样。  
* oob_score=False：oob（out of band，带外）数据，即：在某次决策树训练中没有被bootstrap选中的数据。多单个模型的参数训练，我们知道可以用cross validation（cv）来进行，但是特别消耗时间，而且对于随机森林这种情况也没有大的必要，所以就用这个数据对决策树模型进行验证，算是一个简单的交叉验证。性能消耗小，但是效果不错。  
* n_jobs=1：并行job个数。这个在ensemble算法中非常重要，尤其是bagging（而非boosting，因为boosting的每次迭代之间有影响，所以很难进行并行化），因为可以并行从而提高性能。1=不并行；n：n个并行；-1：CPU有多少core，就启动多少job
* warm_start=False：热启动，决定是否使用上次调用该类的结果然后增加新的。  
* class_weight=None：各个label的权重。  

<br>进行预测可以有几种形式：<br>
* predict_proba(x)：给出带有概率值的结果。每个点在所有label的概率和为1.  
* predict(x)：直接给出预测结果。内部还是调用的predict_proba()，根据概率的结果看哪个类型的预测值最高就是哪个类型。  
* predict_log_proba(x)：和predict_proba基本上一样，只是把结果给做了log()处理。

#### 提升决策树（Boosted Decision Tress）
#### 决策树构造比较（Comparison Of Three Methods:Bagging,Boosting,and Randomization）
#### 支持向量机(Support Vector Machines)
#### 朴素贝叶斯（NaiveBayes）

### 附录：
