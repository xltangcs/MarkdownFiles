# Always-On Speech Recoginition Using TrueNorth, a Reconfigurable, Neurosynptic Processor

## 使用TrueNorth(可重构神经突触处理器)的常开语音识别

  

### 1 introduction

  

>神经元分为 细胞体和突起

>突起分为树突和轴突

>树突短而分支多 由细胞体扩张突出 接受其他神经元轴突传来的冲动传给细胞体

>轴突长而分支少 接受外来刺激 再由细胞体传出

>树突接受信息，轴突传递信息

  

TrueNorth

- 功耗低

  

语音识别任务通常使用 梅尔频率倒谱系数(MFCC)特征提取和分类器 来实现

  

TrueNorth旨在支持大规模并行、低精度峰值神经网络，并对连接和配置结构有特殊约束，以实现高能源效率。

  

需要一种新的音频特征提取器，以符合TrueNorth结构的计算结构

  

### 2 TrueNorth

TrueNorth芯片是并行的、事件驱动的、可扩展的TrueNorth架构的第一个硅实现

  

神经突触核心有256个神经元和256个轴突

  

Vj(t) : 第j个神经元（neuron）在t时刻的膜电位

Ai(t) : 第i个轴突（axon）收到的脉冲信号

Wi,j : 核心的输入突触权重矩阵？ 1 代表第i个突触和第j个树突相连

Gi ：整数类型，为每个神经元定义权重

Sj^Gi ： 表示第i个轴突和第j个树突(dendrite)的突触(synaptic)权重

入i : 施加于膜电位上的泄漏量

  

当细胞膜电位超过阈值加上PRNG产生的随机值时，神经元就会放电

  

![图2](photo/%E6%89%B9%E6%B3%A8%202022-10-24%20122025.png)

  

TrueNorth的编程主要是通过Corelet编程环境(CPE)使用Corelet语言完成的。

  

MatConvNet使用MFCC和LATTE特征来训练用于识别语音数字的DNN分类器。

  

TureNorth 低精度突触权重

使用传统的卷积神经网络会降低准确性

  

Eedn结构

每层 rows * columns * features

filter 卷积核

  

Eedn 和 传统的卷积神经网络

* Eedn将层和相应的过滤器划分到多个组，以确保过滤器的大小，以便使用单个TrueNorth核心实现

* 三权值

* 具有阈值激活函数的脉冲神经元，这个函数的导数近似训练

  

### 3 Audio Feature Extraction

  

wave -> MFCCs Fig.5.

  

LATTE 降低音频预处理的功率，并在TrueNorth上聚合完整的听觉处理管道

时域到频域

  

TrueNorth 精度适度下降 但是提高了一个数量级以上的能源效率

  

LATTE结构

![Fig.6.](photo/%E6%89%B9%E6%B3%A8%202022-10-24%20154809.png)

  

### 4 CONFIGURABLE PREPROCESSING PIPELINE