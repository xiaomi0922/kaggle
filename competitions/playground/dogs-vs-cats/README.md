# **猫和狗**

![](/static/images/competitions/playground/dogs-vs-cats.jpg)

> 注意：[项目规范](/docs/kaggle-quickstart.md)

## 比赛说明

* 在本次比赛中，您将编写一个算法来分类图像是否包含狗或猫。这对人类，狗和猫来说很容易。你的电脑会觉得有点困难。

深蓝在1997年在国际象棋比赛中击败卡斯帕罗夫。
沃森在2011 年击败了Jeopardy最聪明的琐事。
你能否在2013年从米登斯那里告诉菲多？

> Asirra数据集

Web服务通常受到人们解决这个难题的挑战，但这对计算机来说很困难。这样的挑战通常被称为 [CAPTCHA](http://www.captcha.net/)  （完全自动公开的图灵测试来告诉计算机和人类）或HIP（人类交互证明）。HIP用于多种用途，例如减少电子邮件和博客垃圾邮件，防止对网站密码进行暴力攻击。

[Asirra](http://research.microsoft.com/en-us/um/redmond/projects/asirra/)（限制访问的动物物种图像识别）是一项HIP，通过询问用户识别猫和狗的照片而工作。这项任务对于计算机来说很难，但研究表明人们可以快速准确地完成任务。许多人甚至认为这很有趣！以下是Asirra界面的一个例子：

Asirra是独一无二的，因为它与全球最大的网站 [Petfinder.com](http://www.petfinder.com/) 合作，  致力于为无家可归的宠物寻找住所。他们向微软研究院提供了超过三百万张猫和狗的图像，由美国各地数千个动物收容所的人员手动分类。Kaggle很幸运能够提供这些数据的一个子集，用于娱乐和研究。 

> 图像识别攻击

虽然随机猜测是最简单的攻击形式，但各种形式的图像识别可以让攻击者做出比随机更好的猜测。照片数据库（各种各样的背景，角度，姿势，照明等）具有巨大的多样性，难以进行准确的自动分类。在多年前进行的一项非正式调查中，计算机视觉专家认为，如果没有现有技术的重大进展，精度高于60％的分类器将很困难。作为参考，60％分类器将12幅图像HIP的猜测概率从1/4096提高到1/459。

> 最先进的

目前的文献表明机器分类器可以在这项任务上得到80％以上的准确度[1]。因此，Asirra不再被认为是安全的。我们创建了这个比赛，以针对这个问题对最新的计算机视觉和深度学习方法进行基准测试 你能破解CAPTCHA吗？你能改善艺术状态吗？你能在猫狗之间创造持久的和平吗？

好的，我们会解决前者。 

> 致谢

我们感谢微软研究院为此次比赛提供数据。

* Jeremy Elson，John R. Douceur，Jon Howell，Jared Saul，Asirra：在计算机和通信安全（CCS）第14届ACM会议论文集计算机械协会会刊上发表的利用调整手动图像分类的CAPTCHA， 2007年10月

## 参赛成员

* 开源组织: [ApacheCN ~ apachecn.org](http://www.apachecn.org/)
* 参与人员: [片刻](https://github.com/jiangzhonglian)

## 比赛分析

* 回归问题：价格的问题
* 常用算法： `回归`、`树回归`、`GBDT`、`xgboost`、`lightGBM`

```
步骤:
一. 数据分析
1. 下载并加载数据
2. 总体预览:了解每列数据的含义,数据的格式等
3. 数据初步分析,使用统计学与绘图:初步了解数据之间的相关性,为构造特征工程以及模型建立做准备

二. 特征工程
1.根据业务,常识,以及第二步的数据分析构造特征工程.
2.将特征转换为模型可以辨别的类型(如处理缺失值,处理文本进行等)

三. 模型选择
1.根据目标函数确定学习类型,是无监督学习还是监督学习,是分类问题还是回归问题等.
2.比较各个模型的分数,然后取效果较好的模型作为基础模型.

四. 模型融合

五. 修改特征和模型参数
1.可以通过添加或者修改特征,提高模型的上限.
2.通过修改模型的参数,是模型逼近上限

六. 提交格式
'''(label: 1=dog, 0=cat)
id,label
1,0
2,0
3,0
etc...
'''
```

## 一. 数据分析

### 数据下载和加载

> 数据获取

* 数据集下载地址：<https://www.kaggle.com/c/dogs-vs-cats/data>

> 特征说明

* Dogs vs. Cats是一个传统的二分类问题。
    * 训练集包含25000张图片，命名格式为<category>.<num>.jpg, 如cat.10000.jpg、dog.100.jpg
    * 测试集包含12500张图片，命名为<num>.jpg，如1000.jpg。
* 参赛者需根据训练集的图片训练模型，并在测试集上进行预测，输出它是狗的概率。
* 最后提交的csv文件如下，第一列是图片的<num>，第二列是图片为狗的概率。

