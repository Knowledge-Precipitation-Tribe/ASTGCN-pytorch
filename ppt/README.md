# ASTGCN: Attention Based Spatial-Temporal Graph Convolutional Networks for Traffic Flow Forecasting

The paper "[Attention Based Spatial-Temporal Graph Convolutional Networks for Traffic Flow Forecasting]()"

## 问题定义

如何有效的提取数据的时空相关性，探索非线性且复杂的时空数据，发现其固有的时空模式，准确地预测交通流。

本篇论文通过以临近、前几日、前几周为周期对于未来时间片的交通流量进行预测。

![image-20200329142010326](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\problem_init.png)

## 相关工作

该论文从三个方面进行相关工作的介绍，分别列举了不同方面的前人工作进展。

![T_F](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\Traffic_forecasting.png)

![C_O_G](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\Convolution_on_graph.png)

![A_M](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\Attention_mechanism.png)

## 方法与模型结构

### 网络定义

将交通网络定义为无向图G = (V, E, A)，如图2(a)所示，其中V为|V | = N个节点的集合;E是一组边，表示节点之间的连通性;A∈R（N\*N）表示图G的邻接矩阵。每个节点检测到F个观测值（速度、流量、时间占有率），代表着该节点的 F个特征，如图2(b)实线所示。本文即利用全网过去T个时间节点的数据（速度、流量和时间占有率）预测未来P个时间点的交通流量，即输入为X∈R（N\*F\*T）, 输出为Y∈R（N\*P），其中N为观测站数据，F=3为每个节点的三个特征，T为输入的T个时间步，P为输出的时间步。

![network](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\network.png)

### 框架总览

这里展示了网络的总体结构，并阐述了三个输入的定义。

![Framework overview](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\framework_overview.png)

### 时空模块 ST block

这部分是网络时空模块的具体实现。

#### SAtt+TAtt

这里对于空间维度和时间维度分别使用了注意力机制去捕捉各维度的关联性。

![SATT](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\satt.png)

![TATT](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\tatt.png)

#### GCN+Conv

在空间维度上使用了图卷积网络进行处理，在时间维度上则使用了标准的卷积网络进行处理。

![GCN](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\gcn.png)

![Conv](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\Conv.png)

### 多特征融合

在最后将三个因素得到的输出进行加权融合。

![Fusion](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\fusion.png)

## Experiment

- Dataset

  - PeMSD4
    If refers to the traffic data in San Francisco Bay Area,containing 3848 detectors on 29 roads.The time  span of this dataset is from January to February in 2018.The first 50 days as the training set,and the remains are the test set.

- Settings
  
    - Chebyshev polynomial K = 3
    - Graph convolution layers use 64 convolution kernels
    - Temporal convolution layers use 64 convolution kernels
    

通过与其他方法的对比，可以看到ASTGCN由于其他模型。并且论文还给出了除去注意力机制的MSTGCN模型，通过对比可以看出加入注意力机制后模型的准确率得到了提升。

![ex](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\ex_picture.png)

并且论文还给出了注意力矩阵，以便于更好的展现注意力机制的应用。

![matrix](C:\Users\14675\Desktop\ASTGCN-pytorch\ppt\images\satt-matrix.png)

这里由于代码暂时还有些问题未处理好，所以暂时不展示自己的实验结果，后期会对于仓库进行更新。

PPT中展示的结果为初步实现结果，不准确

## 参考文献

[1] [Yao, H.; Tang, X.; Wei, H.; Zheng, G.; Yu, Y.; and Li, Z. 2018a.Modeling spatial-temporal dynamics for traffic prediction. *arXiv*  preprint arXiv:1803.01254*.](https://www.researchgate.net/profile/Huaxiu_Yao/publication/323570926_Modeling_Spatial-Temporal_Dynamics_for_Traffic_Prediction/links/5b1e23ea45851587f29f6a61/Modeling-Spatial-Temporal-Dynamics-for-Traffic-Prediction.pdf)

[2] [Yao, H.; Wu, F.; Ke, J.; Tang, X.; Jia, Y.; Lu, S.; Gong, P.; and Ye, J. 2018b. Deep multi-view spatial-temporal network for taxi demand prediction. In *AAAI Conference on Artificial Intelligence*,2588–2595.](https://www.aaai.org/ocs/index.php/AAAI/AAAI18/paper/viewPaper/16069)

[3] [Yu, B.; Yin, H.; and Zhu, Z. 2018. Spatio-Temporal Graph Convolutional Networks: A Deep Learning Framework for Traffic Forecasting. In *International Joint Conference on Artificial Intelligence*, 3634–3640.](https://arxiv.org/abs/1709.04875)

