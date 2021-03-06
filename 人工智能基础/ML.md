# 机器学习概观

## 频率视角下的机器学习

机器学习:基于已知数据构造概率模型,反过来再运用概率模型对未知数据进行预测与分析

概率存在两种解读,概率的频率学派和贝叶斯学派

频率学派对概率,统计学和机器学习的认识方式:

* 频率学派认为概率是随机事件发生频率的极限值
* 频率学派执行参数估计时,视参数(分布的参数)为确定取值,视数据为随机变量
* 频率学派主要使用最大似然估计法,让数据在给定参数的似然概率最大化
* 频率学派对应机器学习中的统计学习,以经验风险最小化作为模型选择的准则

通过最大似然估计的公式可以计算出一个分布参数的估计值,也是一个随机变量,而置信区间则划定了真值的取值范围

## 贝叶斯视角下的机器学习

贝叶斯学派给出的概率定义:概率表示的是客观上事件的可信程度,也可以说是主观上主体对事件的信任程度,它是建立再事件对已有知识的基础上的

核心:贝叶斯定理

![](mlimg\01.png)

贝叶斯定理的意义在于将先验概率和后验概率关联起来,刻画了数据对于知识和信念的影响

贝叶斯定理告诉我们,后验概率正比于先验概率和似然概率的乘积,这意味着后验概率的实质上就是用先验概率对似然概率做了个加权处理.先验信息是贝叶斯主义中不可或缺的核心要素

频率统计理论的核心在于待估计的参数是固定不变的常量,而用来估计的数据是随机的变量.而贝叶斯统计则恰恰相反,它将待估计的参数视为随机变量,用来估计的数据反过来是确定的常数,讨论观测数据的概率2分布没有意义

相对于频率主义的最大似然估计,贝叶斯主义在参数估计中倾向于使后验概率最大化,使用最大后验概率估计

贝叶斯方法的缺点:一是对未知变量的积分运算会导致极高的计算复杂度,二是对先验分布的设定包含一定的主观性

贝叶斯学派对概率,统计和机器学习的认识方式:

* 贝叶斯学派认为概率是事件的可信程度或主体对事件的信任程度
* 贝叶斯学派执行参数估计时,视参数为随机变量,视数据为确定取值
* 贝叶斯学派主要使用最大后验概率法,让参数在先验信息和给定数据下的后验概率最大化
* 贝叶斯学派对应机器学习中的概率图模型,可以在模型预测和选择中提供更加完整的信息

## 机器学习的特点与分类

机器学习侧重于将预先设定的准确率等指标最大化,而模式识别更注重于潜在模式的提取与解释

机器学习所解决问题的特点:

* 机器学习适用于解决蕴含潜在规律的问题
* 纯算术问题无需使用机器学习
* 机器学习需要大量数据发现潜在规律

机器学习的任务就是使用数据计算出与目标函数最接近的假设,或者说拟合出最精确的模型

机器学习的分类:

* 输入特征
  * 具体特征:具有明确意义的数字指标
  * 原始特征:原始资料
  * 抽象特征
* 输出结果
  * 分类算法
  * 回归算法
  * 标注算法
* 学习任务
  * 监督学习:训练数据中的每组输入都有其对应的输出结果,适用于预测任务
  * 无监督学习:对没有输出的数据进行学习,适用于描述任务
* 学习策略
  * 批量学习:一口气对整个数据集进行建模与学习
  * 在线学习:对数据一点点地进行建模与学习
  * 主动学习:通过有选择地询问无标签数据的标签来实现迭代式的学习

## 计算学习理论

对于机器学习来说,如果不能通过算法获得存在于训练集之外的信息,学习任务在这样的问题上就是不可行的

在概率中,有界的独立随机变量的求和结果与数学期望的偏离程度存在一个固定的上界,这一关系可以用Hoeffding不等式来表示.

![](mlimg\02.png)

u为真实值(泛化误差),v为估计值(训练误差),N为样本容量,估计的精度只和样本容量N有关,要想提高估计的精度,最本质的方法还是增加样本容量,只要样本容量足够大,估计值与真实值的差值将会以较大的概率被限定在较小的常数e内

Hoeffding不等式是对单个模型在训练集上的错误概率和所有数据上错误概率之间关系的描述,也就是训练误差和泛化误差的关系.它说明总会存在一个足够大的样本容量N使两者近似相等,这时可以根据模型的训练误差来推导其泛化误差,从而获得真实情况的一些信息

让模型取得较小的泛化误差可以分为两步:一是让训练误差足够小,二是让泛化误差和训练误差足够接近

概率近似正确PAC学习理论:机器学习利用训练集来选择出的模型很可能具有较低的泛化误差

PAC可学习性

* ![](mlimg\03.png)

* 描述近似正确准确度参数ε将模型的误差水平限制在极小的范围内

* 描述概率的置信参数δ,由于训练集是随机生成的,所以学好模型只是以1-δ出现的大概率事件,而并非100%发生的必然事件

样本复杂度:保证一个概率近似正确所需要的样本数量

VC维:

* 是对无限假设空间复杂度的一种度量方式,也可以用于给出模型泛化误差在概率意义上的上界.

* 任何VC维有限2的假设空间都是PAC可学习的

* 较小的VC维虽然能够让训练误差和泛化误差更加接近,但这样的假设空间不具备较强的表达能力,训练误差本身难以降低

* 而VC维更大的假设空间表达能力更强,得到的训练误差更小,但会使训练误差和泛化误差之间更可能出现较大的差异

Rademacher复杂度:

* 结合先验信息对函数空间复杂度的度量
* 经验Rademacher复杂度:描述函数空间和随机噪声在给定数据集上的相关性
* Rademacher变量:各以50%的概率取正负1两个值来表示随机噪声
* 没有经验的Rademacher复杂度:函数空间在给定数据分布上拟合噪声的性能
* ![](mlimg\04.png)
* 上式为训练误差和泛化误差之差,S1为训练集,S2为验证集

## 模型的分类方式