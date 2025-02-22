---
title: "Understanding Parameter Calculation in Transformer-Based Models (simplified)"
source: "https://medium.com/@geosar/understanding-parameter-calculation-in-transformer-based-models-simplified-e8c7f4e059d8"
author:
  - "[[George Sarmonikas]]"
published: 2024-06-12
created: 2025-02-22
description: "Transformer-based models, particularly in the field of natural language processing (NLP), have revolutionized how machines understand and generate human language. A fundamental aspect of these models…"
tags:
  - "clippings"
---


![George Sarmonikas](https://miro.medium.com/v2/resize:fill:88:88/1*r5gLvspUjTRlevW1f9z8KQ.jpeg)

](https://medium.com/@geosar?source=post_page---byline--e8c7f4e059d8---------------------------------------)

Looking to hide highlights? You can now hide them from the “•••” menu.

![](https://miro.medium.com/v2/resize:fit:1400/1*DHz1FEwn1H8OahG8lchjTA.jpeg)

Transformer-based models, particularly in the field of natural language processing (NLP), have revolutionized how machines understand and generate human language. A fundamental aspect of these models is their sheer size, often measured by the number of parameters they contain, e.g. Llama-3–8B, where 8B is the total trained parameters of the model, in this case 8 Billion, and 3 is the version of the Llama model.  
基于 Transformer 的模型，尤其是在自然语言处理（NLP）领域，彻底改变了机器理解和生成人类语言的方式。这些模型的基本特征是它们的规模，通常通过它们包含的参数数量来衡量，例如 Llama-3–8B，其中 8B 是模型的全部训练参数，在这种情况下为 80 亿，而 3 是 Llama 模型的版本。  
Understanding how to calculate these parameters is crucial when working with such models but also if attempting to build your own model.  
理解如何计算这些参数对于使用此类模型至关重要，同时如果尝试构建自己的模型也是如此。  
This blog post delves into the intricacies of calculating the number of parameters in a Transformer-based model.  
本博客文章深入探讨了计算基于 Transformer 模型的参数数量的复杂性。  
(Updated: Added some additional details related to the print out of the model architecture)  
(更新：添加了一些与模型架构打印输出相关的额外细节)

## Introduction to Transformers  
Transformer 简介

Transformers, the “T” in GPT, introduced in the paper “[Attention is All You Need” by Vaswani et al. (2017)](https://arxiv.org/abs/1706.03762), use a mechanism called self-attention to process input data. Unlike traditional sequential models like RNNs and LSTMs, Transformers can handle long-range dependencies and parallelize computations efficiently, making them highly effective for a range of NLP tasks.  
Transformer，GPT 中的“T”，由 Vaswani 等人于 2017 年发表的论文《Attention is All You Need》中引入，使用一种称为自注意力的机制来处理输入数据。与传统的序列模型如 RNN 和 LSTM 不同，Transformer 可以处理长距离依赖并有效地并行计算，这使得它们在众多 NLP 任务中非常有效。

A Transformer model typically consists of an encoder and a decoder, each made up of several identical layers. Each layer includes multi-head self-attention mechanisms and position-wise feed-forward networks.  
一个 Transformer 模型通常由一个编码器和一个解码器组成，每个都由几个相同的层构成。每一层包括多头自注意力机制和位置前馈网络。

![](https://miro.medium.com/v2/resize:fit:1400/0*ckOlh1QRKCUCMOyl.png)

## Components of a Transformer  
变压器组件

1\. **Embedding Layer**: Maps input tokens to continuous vectors.  
嵌入层：将输入标记映射到连续向量。  
2\. **Positional Encoding**: Adds information about the position of each token.  
2\. 位置编码：添加每个标记的位置信息。  
3\. **Multi-Head Attention**: Allows the model to focus on different parts of the input sequence simultaneously.  
3\. 多头注意力：允许模型同时关注输入序列的不同部分。  
4\. **Feed-Forward Networks**: Apply a series of linear transformations and non-linear activations.  
4\. 前馈网络：应用一系列线性变换和非线性激活。  
5\. **Layer Normalization**: Normalizes the inputs to each sub-layer.  
5\. 层归一化：对每个子层的输入进行归一化。

A print out of the GPT-Large model is as follows:  
GPT-Large 模型的打印输出如下：

![](https://miro.medium.com/v2/resize:fit:1400/1*YvxoWQpnJ8sLQPhP9rAqCg.png)

## Calculating Parameters  计算参数

To calculate the number of parameters in a Transformer model, we need to consider each component:  
计算 Transformer 模型中参数数量时，需要考虑每个组件：

**Step 1 — Calculating the Embedding layer parameters:  
第一步 — 计算嵌入层参数：**

1. Embedding parameters**:**  嵌入参数：

- This is the Embedding layer (**wte** — **w**eight **t**oken **e**mbedding) responsible for embedding our input tokens. (where the 50257 is the number of tokens in the model vocabulary size, and for each token there is a embedding representation vector of size 1280 that represents each token.)  
这是嵌入层（wte — 权重标记嵌入），负责嵌入我们的输入标记。（其中 50257 是模型词汇量的大小，并且对于每个标记，都有一个表示每个标记的 1280 维嵌入表示向量。）
- If the **vocabulary size** is ***V*** and the **embedding dimension** is ***E***, the number of parameters is ***V x E***.  
如果词汇量大小为 V，嵌入维度为 E，则参数数量为 V x E。
- In this case and for simplicity, we assume embeddings are tied (shared between input and output).  
在这种情况下，为了简化，我们假设嵌入是绑定的（输入和输出之间共享）。
- Notice: ***E*** is also referred to as “***dmodel***” is some research papers.  
注意：E 也被一些研究论文称为“dmodel”。  
For example GPT3-small , dmodel=768, indicating the dimension of the model’s hidden size, as shown in the Figure below:  
例如 GPT3-small，dmodel=768，表示模型隐藏层的大小，如图下所示：

![](https://miro.medium.com/v2/resize:fit:1400/1*YwYaOzLfJYV6GAve4ZxEkg.png)

2\. Positional Encoding:  2\. 位置编码

- This is the “***wpe”*** (**w**eight **p**osition **e**mbedding), part of the embedding layer, responsible for embedding the positions of our input tokens.  
这是“wpe”（权重位置嵌入），嵌入层的部分，负责嵌入我们输入标记的位置。
- There are 1024 possible positions for each token, and each position has a fixed vector of 1280 that is learnable.  
每个标记有 1024 个可能的位置，每个位置都有一个可学习的固定向量，大小为 1280。
- Therefore, to capture the *order of words* in a sequence, positional embeddings are added to the token embeddings. If the **sequence length** is ***L*** (this the maximum sequence length that our model can handle and for GPT2 this is 1024), then this requires ***L* x *E​*** parameters. The maximum sequence length (***L***) is also referred to as the “**context window.**”  
因此，为了捕捉序列中单词的顺序，我们将位置嵌入添加到标记嵌入中。如果序列长度为 L（这是我们模型可以处理的最大序列长度，对于 GPT2 来说，这是 1024），那么这需要 L x E 参数。最大序列长度（L）也被称为“上下文窗口”。

The total **Embedding Layer parameters** are:  
总嵌入层参数为：  
Embedding\_Parameters + Positional\_Encoding = (***V* x *E***)+(***L* x *E***)  
嵌入参数 + 位置编码 = (V x E) + (L x E)

**Step 2 — Calculating the Transformer layer parameters:  
第二步 — 计算 Transformer 层的参数：**

3\. Multi-Head Attention:  3\. 多头注意力

- Each attention head has three sets of weights: Query (Q), Key (K), and Value (V).  
每个注意力头包含三组权重：查询（Q）、键（K）和值（V）。
- Suppose the model embedding dimension is ***E***, the number of heads is ***h***, and each head has a dimension of ***E\_h = E/h***.  
假设模型嵌入维度为 E，头数为 h，每个头的维度为 E\_h = E/h。
- The number of parameters for Q, K, and V in a *single head* is  
一个头中 Q、K 和 V 的参数数量  
***3 x (E x E\_h) = 3 x (E x E/h) = 3E²/h***
- Since there are ***h*** heads, the total number of parameters for Q, K, and V is simplified to: ***3E²*** .  
由于有 h 个头，Q、K 和 V 的总参数数量简化为：3E²。
- We need to add also a **bias vector** of size ***3E.***  
我们需要添加一个大小为 3E 的偏置向量。
- The output of multi-head attention is a weighted sum of the heads, which requires an additional projection with weights ***Wo*** of size ***E x E***. Thus, the number of parameters here is ***E²***.  
多头注意力的输出是头的加权和，需要额外的投影，其权重为 Wo，大小为 E x E。因此，这里的参数数量是 E²。  
In this case we add yet another **bias vector** of size ***E.***  
在这种情况下，我们添加另一个大小为 E 的偏置向量。
- Total parameters for **multi-head attention**: ***3E² + 3E + E² + E= 4E²+4E***.  
多头注意力机制的参数总数：3E² + 3E + E² + E = 4E² + 4E.

4\. Feed-Forward Networks:  
4\. 前馈网络：

- or “multi-layer perceptron” layer, and it responsible for providing most of the computation of the transformer.  
或“多层感知器”层，它负责提供 transformer 的大部分计算。
- It is typically comprised for four sublayers: ***c\_fc, c\_proj, act*** and ***dropout.***  
它通常由四个子层组成：c\_fc、c\_proj、act 和 dropout。
- ***c\_fc*** is responsible for projecting the output of the Attention layer into a hidden space — ***Hidden space (H),*** where ***H =*** ***4E.***  
c\_fc 负责将注意力层的输出投影到隐藏空间——隐藏空间（H），其中 H = 4E。
- The ***c\_fc*** is of size ***E*** by ***H*** plus a bias vector of size ***H.  
c\_fc 的大小为 E 乘以 H，再加上一个大小为 H 的偏置向量。  
***Therefore, ***c\_fc=E x H + H***  
因此，c\_fc=E x H + H
- Next, ***c\_proj*** is responsible for projecting the output of the first feed-forward layer back into the embedding space. Therefore ***c\_proj*** is equal to: ***H x E + E*** (as a bias vector).  
接下来，c\_proj 负责将第一层前馈网络的输出投影回嵌入空间。因此，c\_proj 等于：H x E + E（作为一个偏置向量）。
- ***act***, is the activation layer, usually GELU, or SwiGLU in most recent implementation. There are no learnable parameters here.  
act，是激活层，通常是 GELU，或最新实现中的 SwiGLU。这里没有可学习的参数。
- ***dropout***, is responsible for dropping out a fraction of the activations, usually 10%. There are no learnable parameter here either.  
dropout，负责丢弃一部分激活，通常为 10%。这里也没有可学习的参数。
- Adding ***c\_fc + c\_proj = E H + H + E H + E = 2 E H + E +H***  
添加 c\_fc + c\_proj = E H + H + E H + E = 2 E H + E + H

5\. Layer Normalization:  5\. 层归一化

- Layer ***ln\_1*** or ***LayerNorm***, is responsible for “normalizing” the input before it is passed to the attention layer. It normalizes across the last dimension, which is the embedding dimension. This means that the values along the embedding dimension will be normally distributed with a mean of 0 and a standard deviation of 1.  
层 ln\_1 或 LayerNorm 负责在输入传递到注意力层之前进行“归一化”。它在最后一个维度上进行归一化，即嵌入维度。这意味着沿着嵌入维度的值将以均值为 0 和标准差为 1 的正态分布。
- according to [this reference](https://pytorch.org/docs/stable/generated/torch.nn.LayerNorm.html), Layer normalization formula is :  
根据此参考，层归一化公式是：

![](https://miro.medium.com/v2/resize:fit:936/1*U3jROpSdoeCsgTbswCd-yQ.png)

- **γ** and ***β*** are learnable parameters of size ***E***, therefore the parameters here are : ***2E***  
γ和β是大小为 E 的可学习参数，因此这里的参数是：2E
- There is also a second ***LayerNorm***, ***ln\_2***, which is basically the same as the previous one. Parameters again are: ***2E***  
也存在第二个 LayerNorm，即 ln\_2，基本上与之前的一个相同。参数再次是：2E
- In total here we have ***ln\_1 + ln\_2 = 2E+2E = 4E***  
总共这里我们有 ln\_1 + ln\_2 = 2E+2E = 4E
- Finally there is also ***ln\_f*** exactly the same as the previous, with again ***2E*** learnable paparameters.  
最后，ln\_f 也与之前完全相同，再次具有 2 个可学习的参数。

**Step 3 — Total Parameters in a Single Layer  
步骤 3 — 单层中的总参数数**

Combining all these components, the total number of parameters in a single Transformer layer is:  
将所有这些组件组合起来，单个 Transformer 层的参数总数为：

**EmbeddingLayer + Layers \*(MultiheadAttention + FeedForwardLayer + LayerNormalization) + FinalLayerNormalization  
嵌入层 + 层 \*(多头注意力 + 前馈层 + 层归一化) + 最终层归一化**

where **Layers** ***(L)*** is the number of layers in the model architecture.  
层（L）是模型架构中的层数。

Plugging in the values we calculated before, we get:  
插入我们之前计算出的值，我们得到：

***VE***+***LE*** + ***L(4E²+4E + 2EH +E+H + 4E) + 2E***

**Example Calculation for GPT2:  
GPT2 的示例计算：**

As a realistic example, we will use the value of GPT2, where  
作为一个现实示例，我们将使用 GPT2 的值，其中  
V = 50257, E=768, L=12, H=4E

We get that GPT2 has Total Parameters = 123M  
我们明白 GPT2 的总参数量=123M

**Example Calculation for GPT3–13B:  
GPT3–13B 的示例计算：**

As a realistic example, we will use the value of GPT3–13B, where  
作为一个现实示例，我们将使用 GPT3–13B 的值，其中  
V = 50257, E=5140, L=40, H=4E

We get that GPT3–13B has Total Parameters = 13B, as expected!  
我们了解到 GPT3–13B 的总参数量为 13B，正如预期！

**Conclusion  结论**

Calculating the number of parameters in a Transformer-based model involves summing the contributions from the embedding layer, multi-head attention mechanisms, feed-forward networks, and layer normalization. This detailed understanding allows practitioners to design and optimize models effectively, ensuring a balance between performance and computational efficiency.  
计算基于 Transformer 的模型中参数数量涉及将嵌入层、多头注意力机制、前馈网络和层归一化的贡献相加。这种详细的理解使从业者能够有效地设计和优化模型，确保性能和计算效率之间的平衡。

Understanding these calculations is crucial, as it directly impacts the model’s memory requirements, training time, and ultimately its performance on NLP tasks. By mastering these details, you can better appreciate the complexities and capabilities of modern Transformer-based models.  
理解这些计算至关重要，因为它直接影响模型的内存需求、训练时间，以及最终在 NLP 任务上的表现。通过掌握这些细节，您可以更好地欣赏现代基于 Transformer 的模型的复杂性和能力。

For experimentation with additional parameters, an online Parameter Calculator is found here:  
用于实验额外参数，在线参数计算器在此处可找到：

[https://transformerparameters-calculator.streamlit.app/](https://transformerparameters-calculator.streamlit.app/)

In the upcoming post, we will explore why the Total Parameter is impacting Pretraining and Inference time and costs, and how to calculate the optimal training time and optimal datasets.  
在即将发布的文章中，我们将探讨总参数如何影响预训练和推理的时间和成本，以及如何计算最佳训练时间和最佳数据集。