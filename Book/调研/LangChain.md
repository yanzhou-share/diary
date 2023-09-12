# LangChain
## LangChain是什么？
LangChain创建于2022年10月，是围绕LLMs（大语言模型）建立的一个框架，LLMs使用机器学习算法和海量数据来分析和理解自然语言，GPT3.5、GPT4是LLMs最先进的代表，国内百度的文心一言、阿里的通义千问也属于LLMs。

## 组件
一个LangChain应用是通过很多个组件实现的，LangChain主要支持6种组件：
* Models：模型，各种类型的模型和模型集成，比如GPT-4
* Prompts：提示，包括提示管理、提示优化和提示序列化
* Memory：记忆，用来保存和模型交互时的上下文状态
* Indexes：索引，用来结构化文档，以便和模型交互
* Chains：链，一系列对各种组件的调用
* Agents：代理，决定模型采取哪些行动，执行并且观察流程，直到完成为止

## 模型
* LLMS
* 聊天模型
* 文本嵌入模型

[LangChain](https://github.com/langchain-ai/langchainjs)