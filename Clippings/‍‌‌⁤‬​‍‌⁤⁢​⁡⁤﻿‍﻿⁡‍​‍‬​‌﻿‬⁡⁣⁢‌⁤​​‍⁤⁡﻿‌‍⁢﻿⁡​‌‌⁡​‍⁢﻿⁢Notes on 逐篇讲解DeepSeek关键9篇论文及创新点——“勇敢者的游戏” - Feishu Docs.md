---
title: "‍‌‌⁤‬​‍‌⁤⁢​⁡⁤﻿‍﻿⁡‍​‍‬​‌﻿‬⁡⁣⁢‌⁤​​‍⁤⁡﻿‌‍⁢﻿⁡​‌‌⁡​‍⁢﻿⁢Notes on 逐篇讲解DeepSeek关键9篇论文及创新点——“勇敢者的游戏” - Feishu Docs"
source: "https://echotech.feishu.cn/wiki/BtlFwx2BUiVmV6kq0nccRG4xn8d"
author:
published:
created: 2025-03-06
description:
tags:
  - "clippings"
---
This article presents notes on a video that explains nine key DeepSeek papers and their innovations, covering base models and reasoning models, including details on model architectures, training methods, and performance improvements. Key points include: ​

1.

DeepSeek LLM 7B & 67B ：Open-sourced models, trained on 2T tokens with SFT + DPO post-training. The 67B model outperforms LLaMA - 2 70B. They introduced a multi-step learning rate scheduler and studied the scaling law in detail, making improvements such as expanding its scope and using non-embedding FLOPs/token 𝑀 to represent model size.​

2.

DeepSeek MoE ：Improved MoE LLM by segmenting experts more finely and sharing experts to capture common knowledge. Scaled up from 2B to 145B, achieving similar performance to DeepSeek 67B with less computational cost.​

3.

DeepSeek V2 ：A 236B MoE model with multi-head latent attention to optimize KV cache. It has lower training costs, reduced KV cache usage, and higher inference speed compared to DeepSeek 67B. GRPO was used in post-training.​

4.

DeepSeek-V3 ：A 671B MoE model with new features like auxiliary-loss-free load balancing and multi-token prediction training. It was trained on 14.8T tokens with SFT and RL, and was the first large-scale model trained in FP8 precision.​

5.

DeepSeek-Coder ：A proprietary code model, starting from 1.3B to 33B Dense model, trained on 2T tokens. The V2 version, pre-trained from DeepSeek-V2 with additional data, is comparable to GPT-4 Turbo in code tasks and uses RL in post-training.​

6.

DeepSeekMath ：Continued pre-training of the 7B model using 120B math data. It adopted GRPO, which reduces training complexity by eliminating the need for a Value Model.​

7.

DeepSeek R1 ：Reward Model only considers Accrue Reward and Format Reward. R1-Zero achieved O1-like performance using these two signals, and the model addressed issues like improving reasoning ability and readability during training. ​

[[https://echotech.feishu.cn/wiki/BtlFwx2BUiVmV6kq0nccRG4xn8d]]