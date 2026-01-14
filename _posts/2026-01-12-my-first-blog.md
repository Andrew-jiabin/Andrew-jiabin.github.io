---
layout: post
title: "我的第一篇自建博客"
date: 2026-01-12
category: "技术杂谈"
---

## hello-agents进阶篇 | 202601 Blog
以下是关于Task 00 的一些思考

### Task00:环境配置，前言
hello-agents课程讲义中,第一章部分对于agent的发展史做了很详细的介绍, 以及对于Agent行为理论框架的建模,在后续的章节都可以借鉴（写这篇时已经看到了第四章）,其中比较受用的是这张图片，后续的Plan-Solve，reflection 等都可以用这一张图理解。

![原理图](https://raw.githubusercontent.com/datawhalechina/Hello-Agents/main/docs/images/1-figures/1757242319667-5.png)

报这门课之前尝试过用Gemini去按照我的意图来写一个股票交易的AI交易员,我希望它可以自己查股票数据,自己判断应该买哪一个,同时能够自己操作我的电脑, 最开始是尝试了fastmcp来构建这个系统，去用Gemini按我的目的写出对应的MCP-Tool，可是这个过程中很多细节都没有仔细看就交给AI了，这最终导致了最终在某一时刻我的报错已经复杂到Gemini和我都看不懂，这样代码的修改难度大幅提升。   
  
最开始我尝试的是，希望基于Ollama本地接口给我的Agent调用，这样可以减少后期项目真正跑起来时候的费用，但是使用Base64传递图片时卡在了我和AI都理解不了的问题上。于是我们改用DeepSeek和Doubao的付费/免费API来重构,但是在2026年1月8日左右我发现了这个课程,并且想起一位AI researcher的话, 不能闭门造车, 去学一门系统的LLM课程会比这个意义大很多,于是我报了这门课,后续我将把我基于课程讲义(课本)中的一些例程修改之后的版本放在这里. 希望能通过这个课程获得成长, 能最终构建起如上的那样系统的认识, 当我拿到一个问题时,我知道如何使用Agent基于PAES框架去拆解和实现问题.

```python
# 这里就算做我的课程第一行代码吧
print("Hello World")
```

### [课程&上述图片来源]：  
Hello-Agents(https://raw.githubusercontent.com/datawhalechina/Hello-Agents)