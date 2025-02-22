---
title: "MLP 神经网络 --- MLP Neural Nets"
source: "http://www.neural-forecasting.com/mlp_neural_nets.htm"
author:
published:
created: 2025-02-22
description:
tags:
  - "clippings"
---
**Join our Newsletter  加入我们的通讯录**

**Contact  联系**

  
**webmaster: Sven F. Crone  网络管理员：Sven F. Crone**

Centre for Forecasting  预测中心  
Lancaster University   兰卡斯特大学  
Management School  管理学院  
Lancaster LA1 4YF  兰卡斯特 LA1 4YF  
United Kingdom  英国

Tel +44.1524.592991  电话 +44.1524.592991  
Fax +44.1524.844885  传真 +44.1524.844885

eMail  sven dot crone (at)  
电子邮件 sven.crone (@)  
neural-forecasting dot com  
神经预测 dot com

Multilayer perceptrons (MLPs) represent the most prominent and well researched class of ANNs in classification, implementing a feedforward, supervised and hetero-associative paradigm \[4, 36, 51\]. MLPs consist of several layers of nodes , interconnected through weighted acyclic arcs from each preceding layer to the following, without lateral or feedback connections \[4, 31, 32, 36\]. Each node calculates a transformed weighted linear combination of its inputs of the form , with the vector of output activations from the preceding layer, the transposed column vector of weights , and a bounded non-decreasing non-linear function, such as the linear threshold or the sigmoid, with one of the weights acting as a trainable bias connected to a constant input \[36\]. Fig. 2 gives an example of a MLP with a \[3-4-1\] topology:  
多层感知器（MLPs）是分类中最为突出且研究最深入的一类人工神经网络，实现了前馈、监督和异联想范式\[4, 36, 51\]。MLPs 由多个节点层组成，通过从每个前一层到下一层的加权无环弧相互连接，没有横向或反馈连接\[4, 31, 32, 36\]。每个节点计算其输入的变换加权线性组合，形式为，其中前一层输出激活的向量、权重的转置列向量以及一个有界非递减的非线性函数，如线性阈值或 S 形函数，其中一个权重作为与常数输入相连的可训练偏置\[36\]。图 2 给出了一个具有\[3-4-1\]拓扑的 MLP 示例：

![](http://www.neural-forecasting.com/mlp_neural_nets-Dateien/image002.jpg)

Fig. 2: Three layered MLP showing the information processing within a node, using a weighted sum as input function, the logistic function as sigmoid activation function and an identity output function.  
图 2：三层 MLP 展示节点内的信息处理，使用加权求和作为输入函数，对数几率函数作为 sigmoid 激活函数，恒等函数作为输出函数。

For pattern classification, MLPs adapt the free parameter through supervised training to partition the input space through linear hyperplanes. To separate distinct classes, MLPs approximate a function of the form which partitions the X space into polyhedral sets or regions, each one being assigned to one out of the m classes of Y. Each node has an associated hyperplane to partition the input space into two half-spaces. The combination of the individual, linear node-hyperplanes in additional layers allows a stepwise separation of complex regions in the input space, generating a decision boundary to separate the different classes \[36\]. The orientation of the node hyperplanes is determined by the relative sizes of in including the threshold of a node , modelled as an adjustable weights to all nodes to offset the node hyperplane along for a distance from the origin to allow flexible separation. \[30\] The node non-linearity determines the output change as the distance from x to the node hyperplane. In comparison to threshold activation functions with a hard-limiting, binary class border, the hyperplanes associated with sigmoid nodes implement a smooth transition from 0 to 1 for the separation \[23\] allowing a graded response depending on the slope of the sigmoid function and the size of the weights. The desired output as a binary class membership is often coded with one output node or for multiple classification n nodes with respectively \[23\].  
对于模式分类，MLP 通过监督训练调整自由参数，通过线性超平面划分输入空间。为了分离不同的类别，MLP 近似一个将 X 空间划分为多面集或区域的函数，每个集或区域被分配给 Y 的 m 个类别之一。每个节点都有一个相关的超平面，将输入空间划分为两个半空间。在额外层中，单个线性节点-超平面的组合允许逐步分离输入空间中的复杂区域，生成决策边界以分离不同的类别\[36\]。节点超平面的方向由包括节点阈值在内的相对大小决定，这些阈值被建模为调整所有节点的可调权重，以从原点偏移节点超平面一段距离，从而允许灵活的分离。\[30\]节点非线性决定了从 x 到节点超平面的距离作为输出变化。 与具有硬限定的二进制类别边界的阈值激活函数相比，与 sigmoid 节点相关的超平面实现了从 0 到 1 的平滑过渡，从而允许根据 sigmoid 函数的斜率和权重大小进行分级响应。所需的二进制类别输出通常用一个输出节点编码，对于多分类，则用 n 个节点分别编码\[23\]。

The representational capabilities of a MLP are determined by the range of mappings it may implement through weight variation. \[36\] Single layer perceptrons are capable of solving only linearly separable problems, correctly classifying data sets where the classes may be separated by one hyperplane \[36\]. MLPs with three layers are capable to approximate any desired bounded continuous function. The units in the first hidden layer generate hyperplanes to divide the input space in half-spaces. Units in the second hidden layer form convex regions as intersections of these hyperplanes. Output units form unisons of the convex regions into arbitrarily shaped, convex, non-convex or disjoint regions \[1, 45\]. Fig. 3 exemplifies this in a \[2-6-2-1\] network.  
一个 MLP 的表示能力由它可能通过权重变化实现的映射范围决定。\[36\]单层感知器只能解决线性可分问题，正确分类可能由一个超平面分开的数据集\[36\]。具有三层网络的 MLP 能够逼近任何所需的有限连续函数。第一层隐藏层的单元生成超平面来将输入空间分成半空间。第二层隐藏层的单元形成由这些超平面的交集构成的凸区域。输出单元将这些凸区域组合成任意形状的凸、非凸或不相交的区域\[1, 45\]。图 3 在一个\[2-6-2-1\]网络中展示了这一点。

![](http://www.neural-forecasting.com/mlp_neural_nets-Dateien/image004.jpg)

Fig. 3: Partitioning of the input space by linear threshold-nodes in an ANN with two hidden layers and one output node in the output layer and examples of separable decision regions \[9\]. For sigmoid activation functions smooth transitions instead of hard lined decision boundaries would be formed.  
图 3：具有两个隐藏层和一个输出层节点的 ANN 中输入空间的线性阈值节点划分以及可分决策区域的示例\[9\]。对于 Sigmoid 激活函数，将形成平滑的过渡而不是硬线决策边界。

Given a sufficient number of hidden units, a MLP can approximate any complex decision boundary to divide the input space with arbitrary accuracy, producing a (0) when the input is in one region and an output of (1) in the other \[28\]. This property, known as a universal approximation capability, poses the essential problems of adequate model complexity in depth and size, i.e. the number of nodes and layers, and controlling the network training process to prevent overfitting. As perfect classification on training data does not necessitate generalisation for optimal separation of previously unseen data, simpler models with fewer parameters and training using early-stopping with out-of-sample evaluation on separate datasets are generally preferred. The network paradigm of MLP offers extensive degrees of freedom in modelling for classification tasks. Structuring the degrees of freedom, each expert must decide upon the static architectural properties P, the signal processing within nodes U, learning algorithm L and the pre-processed datasets D \[15\] in order to achieve the design goal, characterised through the objective function or error function O \[22\], calling for decisions upon ANN=\[P, L, U, D, O\]. The topology of the net is determined through the size NS and depth NL, of the network (number of layers, number of nodes in each hidden layer and coding of output vector through nodes in the output layer ), connectivity of the weight matrix K (fully or sparsely connected, shortcut connections etc.) and the activation strategy T (feedforward or with feedback): P=\[NS, NL, K, T\]. The signal processing within nodes, is determined by input function S (weighted sum or product, distance measures etc.), activation function A (tanh, logistic, sin, etc. with offsets, limits etc.) and output function F (linear, winner takes all variants or softmax), leading to U=\[S,A,F\]. Decisions concerning the learning algorithm encompass the choice of learning algorithm G (backpropagation, one of its derivatives, higher order methods or heuristics etc.), the complete vector of learning parameters for each individual layer and different phases in the learning process PTL, the procedure IP and number of initialisations for each network IN and the choice of the stopping method for the selection of the best network solution B. For classification, minimizing a squared error measure as the objective function O is inapplicable, as the goal is maximisation of correct classification. Consequently, the specification requires decisions upon MLP=\[\[NS, NL, K, T\], \[S, A, F\], \[G, PT, IP, IN, B\], D, O\], with the question of data pre-processing pre-determined for all competing methods in an early step of the knowledge discovery process.  
给定足够的隐藏单元，MLP 可以近似任何复杂的决策边界，以任意精度划分输入空间，当输入在一个区域时产生（0），在另一个区域时产生输出（1）\[28\]。这种被称为通用逼近能力的属性，提出了深度和尺寸上适当模型复杂性的基本问题，即节点和层数量，以及控制网络训练过程以防止过拟合。由于在训练数据上的完美分类并不需要推广以实现先前未见数据的最佳分离，因此通常更倾向于使用参数更少且使用早期停止和独立数据集上的样本外评估进行训练的简单模型。MLP 的网络范式在分类任务的建模中提供了广泛的自由度。 结构自由度，每位专家必须决定静态建筑属性 P、节点内的信号处理 U、学习算法 L 和预处理数据集 D\[15\]，以实现设计目标，通过目标函数或误差函数 O\[22\]表征，需要对 ANN=\[P, L, U, D, O\]做出决策。网络拓扑由网络的大小 NS 和深度 NL（层数、每个隐藏层中的节点数和输出层节点的输出向量编码）、权重矩阵的连接性 K（全连接或稀疏连接、快捷连接等）和激活策略 T（前馈或带反馈）确定：P=\[NS, NL, K, T\]。节点内的信号处理由输入函数 S（加权求和或乘积、距离度量等）、激活函数 A（tanh、逻辑、正弦等，带有偏移、限制等）和输出函数 F（线性、胜者全得变体或 softmax）确定，导致 U=\[S, A, F\]。 关于学习算法的决策包括选择学习算法 G（反向传播、其衍生物、高阶方法或启发式等）、每个单独层的完整学习参数向量、学习过程中的不同阶段 PTL、初始化过程 IP 以及每个网络 IN 的初始化次数和选择最佳网络解决方案 B 的停止方法。对于分类，将平方误差作为目标函数 O 是不适用的，因为目标是最大化正确分类。因此，规范要求对 MLP=\[\[NS, NL, K, T\], \[S, A, F\], \[G, PT, IP, IN, B\], D, O\]做出决策，而在知识发现过程的早期步骤中，所有竞争方法的数据预处理问题已经预先确定。