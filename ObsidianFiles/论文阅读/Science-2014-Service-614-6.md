## Microprocessors modeled on networks of nerve cells promise blazing speed at incredibly low power—if they live up to hopes

* 2012年，Modha和他的同事们在加利福尼亚州劳伦斯利弗莫尔国家实验室(Lawrence Livermore National Laboratory)使用了一台名为红杉(Sequoia)的IBM超级计算机

  * 模拟人类规模的大脑中的网络通信

  * 该模拟使用了编程的传统电路来模拟5000亿个神经元和100万亿突触之间的通信

  * 红杉所有的150万个处理器芯片和1.5拍字节(1.5千万亿字节)的内存都用于这项任务

  * 模拟的运行速度只有真正大脑的1/1500

  

人类的大脑网络估计包括1000亿个神经元和100万亿个突触。

  

* 20世纪80年代，加州理工学院的电气工程师Carver Mead提出，Nature’s emphasis on parallel process-ing and complexity is at the heart of most attempts at neuromorphic computing.

* HRL实验室的纳拉扬·斯里尼瓦萨(Narayan Srinivasa)，开发了一种硅芯片，它的模拟电路包含576个神经元和73000个突触

* 英国曼彻斯特大学的Stephen Furber 的 SpiNNaker（spiking Nueural Network Architecture）
    * 2w个芯片，每个芯片代表1000个神经元
    * 概念上与红杉模拟相似，但SpiNNaker的设计有望以与生物学相匹配的速度模拟大脑活动

* IBM的TrueNorth
    * Modha和他的同事
    * 100万个晶体管，2.56亿个突触
    * 全新的硬件结构
    * 能够在一个芯片上表示的神经元数量是原来的16倍
    * 2011年，铅笔大小的芯片包含256个神经元和26 2000个突触
    * 目前芯片有三个核阵列
    * 每个核心只有上一代的1/15大小，能量消耗只有1/100
    * 效率是传统芯片的1000多倍
    * 一般芯片每平方厘米50到100瓦，TrueNorth只要20瓦

  

corelet ：采用一种突触芯片语言编写的 a software routine，告诉TrueNorth的神经网络如何执行普通的计算任务