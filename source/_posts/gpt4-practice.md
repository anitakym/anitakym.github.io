---
title: gpt4-practice
date: 2024-04-02 17:43:45
tags:
---
## 内部网关

## 
https://platform.openai.com/docs/api-reference/chat/create
1）choices 默认是 1 个，通过参数 n 可调整
2）choice 里有个 finish_reason，stop 表示已返回完整数据并正常结束

### 

https://developers.google.com/youtube/v3/docs
https://developers.google.com/youtube/v3/docs/captions
https://pypi.org/project/youtube-transcript-api/
https://www.captionsgrabber.com/


https://github.com/malywut/gpt_examples
https://github.com/f/awesome-chatgpt-prompts
https://github.com/langchain-ai/langchainjs
https://js.langchain.com/docs/get_started/introduction
https://python.langchain.com/docs/get_started/introduction
https://js.langchain.com/docs/modules/agents/tools/
https://js.langchain.com/docs/modules/agents/tools/dynamic

## 推荐阅读
- Developing Apps with GPT-4 and ChatGPT.


###
Prompt Engineering 技巧。

1）用 Role + Context + Task 的结构提问，三者均可选，同时顺序不限。
2）请一步一步地思考。
在提示的末尾添加「让我们一步一步地思考」已通过实验证明可以使模型解决更复杂的推理问题。参考： https://arxiv.org/pdf/2205.11916.pdf 。比如「How much is 369 * 1235?」 vs. 「How much is 369 * 1235? Let’s think step by step.」后者会让 GPT 模型的准确性显著提高。
3）小样本学习，即 Few-Shot Learning。参考： https://arxiv.org/pdf/2005.14165.pdf 。说人话就是给一些例子。
4）引导模型在不能解答问题时继续提问。
Did you understand my request clearly? If you do not fully understand my request, ask me questions about the context so that when I answer, you can perform the requested task more efficiently.
4）指定输出格式。
e.g.
The output must be accepted by json.loads.
5）负面提示/negative prompts。
Do not add anything before or after the json text.
Do not explain.
Do not answer anything else, only the keywords.
Only answer one word. （用于构造指令）
If you can answer the question: ANSWER, if you need more information: MORE, if you can not answer: OTHER.
9、微调 Fine-Tuning。
目前，微调仅适用于 davinci 、 curie 、 babbage 和 ada 基础模型。
数据集应该是一个 JSONL 文件，其中每行对应一对提示和完成。
openai tools fine_tunes.prepare_data -f <LOCAL_FILE>
如果您有足够的数据，该工具会询问是否需要将数据分为训练集和验证集。这是一种推荐的做法。
10、LangChain 框架。
LangChain 中有许多预定义的工具。这些包括谷歌搜索、维基百科搜索、Python REPL、计算器、世界天气预报 API 等等。