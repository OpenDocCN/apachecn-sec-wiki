<!--yml
category: 防火墙
date: 2022-11-04 11:54:02
-->

# 一种基于svm机器学习的暗网流量识别模型的建立方法 

| 公开号 | CN106953854 A |
| --- | --- |
| 发布类型 | 申请 |
| 专利申请号 | CN 201710156258 |
| 公开日 | 2017年7月14日 |
| 申请日期 | 2017年3月16日 |
| 优先权日 | 2016年12月15日 |
| 发明者 | 苏宏, 陈周国, 丁建伟, 赵越, 郭宇斌 |
| 申请人 | 中国电子科技集团公司第三十研究所 |

## 摘要

本发明公开了一种基于SVM机器学习的暗网流量识别模型的建立方法，包括如下步骤：构建基于SVM的机器学习的流量检测模型；对流量检测模型中的参数进行机器学习，得到纯净匿名流量和纯净非匿名流量的四个特征值；将纯净匿名流量和纯净非匿名流量的四个特征值带入到流量检测模型中进行运算，得到流量检测模型的参数。与现有技术相比，本发明的积极效果是：通过本发明方法，可以非常准确地刻画出匿名网络数据流量识别的数学模型，应用于匿名网络数据流量检测中，检测准确率高，运算简单高效，并且当匿名网络升级之后，由于该方法采用的是基于机器学习的算法，因此只要针对升级后的匿名网络重新进行学习，便可以检测出新的匿名网络数据流量。

## 说明

一种基于SVM机器学习的暗网流量识别模型的建立方法

技术领域

[0001] 本发明涉及一种基于SVM机器学习的暗网流量识别模型的建立方法。

背景技术

[0002] 匿名网络（暗网）流量的分析与控制，特别是流量检测当前正处于探索研究阶段， 目前并没有一种方法能够有效检测所有的匿名网络流量，有的方法可能仅对某种匿名网络 有效，甚至仅对于某个版本有效，因此匿名网络流量的检测是一个永恒的研究课题，需要不 断的跟进研究，以应对匿名网络的不断升级变化，而提高匿名网络流量检测的准确率，关键 在于流量识别模型建立的准确性上。本方法采用机器学习的方法，尽量准确的建立一个匿 名网络流量识别的数学模型，试图将由于匿名网络的升级变化给检测带来的影响降到最 低，可以较准确的检测出匿名网络的流量。

发明内容

[0003] 为了克服现有技术的上述缺点，本发明提供了一种基于SVM机器学习的暗网流量 识别模型的建立方法，旨在为匿名网络的流量识别建立一个动态变化而准确的数学模型。

[0004] 本发明解决其技术问题所采用的技术方案是：一种基于SVM机器学习的暗网流量 识别模型的建立方法，包括如下步骤：

[0005] 步骤一、构建基于SVM的机器学习的流量检测模型；

[0006] 步骤二、对流量检测模型中的参数进行机器学习，得到纯净匿名流量和纯净非匿 名流量的四个特征值；

[0007] 步骤三、将纯净匿名流量和纯净非匿名流量的四个特征值带入到流量检测模型中 进行运算，得到流量检测模型的参数。

[0008] 与现有技术相比，本发明的积极效果是：

[0009] 通过本发明方法，可以非常准确地刻画出匿名网络数据流量识别的数学模型，应 用于匿名网络数据流量检测中，检测准确率高，运算简单高效，并且当匿名网络升级之后， 由于该方法采用的是基于机器学习的算法，因此只要针对升级后的匿名网络重新进行学 习，便可以检测出新的匿名网络数据流量。

附图说明

[0010] 本发明将通过例子并参照附图的方式说明，其中：

[0011] 图1为基于SVM的流量检测模型原理图。

具体实施方式

[0012] —种基于SVM机器学习的暗网流量识别模型的建立方法，包括如下步骤：

[0013] 步骤一、模型建立

[0014] 匿名网络流量的检测均是在建立数学模型的基础上实施的，但目前大多数的检测 模型可能仅对某种匿名网络有效，甚至仅对于某个版本有效，为了解决这一难题，有效应对 匿名网络的不断升级变化，提高匿名网络流量检测的准确率，需要建立一种新型的匿名网 络流量检测模型。

[0015] 本方法中，检测模型采用基于SVM的机器学习的流量检测模型，匿名网络流量检测 模型如图1所示：图中X为输入的特征向量，特征的数量为d;Xn为采集的样本，是d维向量;yn 为期望输出的值（1，-1)，对应是或不是相应的匿名流量。该模型用数学表达式可以等价表 示为：

[0016] y = kx+b

[0017] 其中，k、b为匿名网络流量识别模型的参数，k为d维的权值向量，b为偏置量，在机 器学习阶段需要通过大量的X和y的输入计算出该k和b的值，一旦完成匿名网络流量识别模 型建立即可对待测流量进行检测，当y>0时，可判断待测流量为对应的匿名流量，当y〈0时， 可判断待测流量不是匿名流量。

[0018] 步骤二、参数确定

[0019] 流量检测模型选定后，需要对模型中的参数进行机器学习以确定其参数值。机器 学习的全过程中将分别学习对应匿名网络纯净的匿名网络流量和纯净的非匿名网络流量 (背景流量）的四个特征，针对收集到的所有流量按host prof iIe格式重新进行分类，一个 主机一个pacp文件，并以下述四个特征值进行匿名网络流量识别的数学模型参数的自学 习，这四个特征分别是:UDP连接数、科学上网权值、UDP流信息熵、流量中Ping-pong相似报文出 现频数。它们的定义和计算方法如下：

[0020] (一) UDP连接数:单位时间内每个Pcap文件不同UDP连接数：

[0021] 计算每个Hostprof ie (pcap)文件中总共的不同IP地址数量K，然后使用K除以 Hos tprof i I e时间T，得到该特征值；

[0022] (二)科学上网权值:对亚马逊服务器、动态网等敏感域名解析的次数乘以权值：

[0023] 维护一个敏感DNS查询列表，不同的域名分配不同的权值，如果Hostprofile中存 在访问敏感DNS的查询，则增加相应的科学上网权值；

[0024] (三)UDP流信息熵:平均每个Host profile中UDP流信息熵大小：

[0025] 对Hostprofi Ie中的每个UDP流进行信息熵计算并求和，然后除以UDP流的总数，信 息熵的定义为

 Figure CN106953854AD00041

[0026](四）相似报文出现频数:Ping-pong相似报文出现次数：

[0027] 统计Hostprofi Ie中连续数据包相似个数，如果相似则次数加1。

[0028] 机器学习完毕，将学习到的纯净匿名流量和纯净非匿名流量的四个特征值反复带 入到匿名网络流量识别模型中进行运算，最后得到匿名网络流量识别模型中的参数k和b， 模型建立完成。

[0029] 步骤三、模型验证

[0030] 构建一个Freegate的匿名网络，在该匿名网络环境中分别抓取足够多的Freegate 匿名流量和非Freegate的背景流量，针对某一台主机分别计算出每个流量的四个特征:UDP 连接数、科学上网权值、UDP流信息熵、流量中Ping-pong相似报文出现频数，然后带入到流量检 测的数学模型中进行运算，计算出模型中的参数k和b，该匿名网络环境的流量检测模型即 构建完成。

[0031]利用已构建的匿名网络流量检测模型在该Freegate匿名网络环境中即可实时检 测到匿名网络的流量数据。在机器学习过程中，学习的时间越长，获取的流量数据越多，构 建的流量检测模型越精确，后续的流量检测也就越准确。

## 权利要求

1. 一种基于SVM机器学习的暗网流量识别模型的建立方法，其特征在于：包括如下步骤： 步骤一、构建基于SVM的机器学习的流量检测模型； 步骤二、对流量检测模型中的参数进行机器学习，得到纯净匿名流量和纯净非匿名流量的四个特征值； 步骤三、将纯净匿名流量和纯净非匿名流量的四个特征值带入到流量检测模型中进行运算，得到流量检测模型的参数。

2. 根据权利要求1所述的一种基于SVM机器学习的暗网流量识别模型的建立方法，其特征在于:所述流量检测模型的等价数学表达式为:y = kx+b，其中：k、b为流量检测模型的参数，k为权值向量，b为偏置量。

3. 根据权利要求2所述的一种基于SVM机器学习的暗网流量识别模型的建立方法，其特征在于：步骤二所述纯净匿名流量和纯净非匿名流量的四个特征值为UDP连接数、科学上网权值、UDP流信息熵和相似报文出现频数。

4. 根据权利要求3所述的一种基于SVM机器学习的暗网流量识别模型的建立方法，其特征在于:所述四个特征值的计算方法分别为： UDP连接数:每个Hostprof ie文件中总共的不同IP地址数量除以Hostprof i Ie时间得到； 科学上网权值:敏感域名解析的次数乘以分配给该域名的权值得到； UDP流信息熵:对Hostprof i Ie中的每个UDP流进行信息熵计算并求和，然后除以UDP流的总数得到； 相似报文出现频数:Hostprof i Ie中连续数据包相似个数的统计值。

5. 根据权利要求4所述的一种基于SVM机器学习的暗网流量识别模型的建立方法，其特征在于:利用流量检测模型对待测流量进行检测时，若y>〇,则判断待测流量为对应的匿名流量，若y〈〇，则判断待测流量不是匿名流量。

## 分类

| | |
| --- | --- |
| 国际分类号 | H04L29/06 |

## 法律事件

| 日期 | 代码 | 事件 | 说明 |
| --- | --- | --- | --- |
| 2017年7月14日 | PB01 |  |  |
| 2017年8月8日 | SE01 |  |  |
