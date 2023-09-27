---
title: openai-summary
date: 2023-04-28 17:02:23
tags:
---
- azure部署相关
- https://github.com/Yidadaa/ChatGPT-Next-Web/issues/371
- https://github.com/Yidadaa/ChatGPT-Next-Web/blob/main/docs/faq-cn.md



#### voice
- speech - recognize - 端上能力（web-浏览器提供能力，Apple-ios10-speech）
- https://chatgpt.sonng.dev/
- heychatgpt

#### chatgpt
- chat generative pre-training transformer
- natural language processing - NLP
- 对话系统
- 图灵测试
- ChatGPT 在接收到用户的提问输入后，输出的文字并不是一口气直接生成的，而是一个字、一个字生成的，这种逐字生成，即生成式（Generative） 
- 基于规则的 NLP - 符号主义
- 基于统计的 NLP - 连接主义（利用机器学习算法从大量的语料库中学习自然语言的规律特征）标注数据 => 建立模型、确定输入输出 => 训练模型 => 利用已训练好的模型进行工作（在 ChatGPT 中，主要采用预训练（ Pre-training ） 技术来完成基于统计的 NLP 模型学习。最早，NLP 领域的预训练是由 ELMO 模型（Embedding from Language Models）首次引进的，后续 ChatGPT 等各种深度神经网络模型广泛采用了这种方式。）（黑盒不确定性，即规则是隐形的，暗含在参数中）（基于统计的方式能够让模型以最大自由度去拟合训练数据集）
- 基于强化学习的 NLP（ChatGPT 模型是基于统计的，然而它又利用了新的方法，带人工反馈的强化学习（Reinforcement Learning with Human Feedback，RLHF） ）（强化学习就是赋予模型更大的自由度，让模型能够自主学习，突破既定的数据集限制）

#### Transformer 的核心是自注意力机制（Self-Attention）
- 自注意力机制可以将输入序列中的每个位置都表示为一个向量，这些向量可以同时参与计算，从而实现高效的并行计算


#### AI - document - search
- aircodelab
- documate(https://github.com/aircodelabs/documate)