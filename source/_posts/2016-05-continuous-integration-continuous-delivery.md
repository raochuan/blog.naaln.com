---
layout: post
title: 持续整合＆持续交付
date: 2016/05/18 00:24:00
categories: 
- 技术
tags: 
---

在公司继续打杂

公司准备弄一套自动部署系统，这两天看了一堆的资料

> 持续部署：业界没有统一明确地定义，简单理解为将集成结果部署到不同的环境供用户使用，并且立即反馈部署结果的实践，其中不同的环境包括：开发环境、测试环境、预发布环境、生产环境

> 持续部署两个核心要素：持续、自动化，自动化是持续的基础

> 持续部署的需求场景：

> 

> - 需要频繁的发布更新

> - 部署规模较大，人工操作费时费力易出错

> - 规范化上线部署流程和配置规范

![](http://pics.naaln.com/blog/2019-01-14-060819.jpg)

我计划的流程如下

- 开发者提交代码到版本仓库

- 自动触发持续集成，`Jenkins`调用`Rundeck`获取部署文件并部署到测试环境

- 在测试环境进行单元测试

- 单元测试完成后，生成`Docker`并部署到开发环境

- 测试人员进行产品验证

- 测试人员在验证通过后，申请发布到生产环境，并手动触发`Jenkins`

- 运维人员触发Rundeck，将`Docker`更新到生产环境

后来发现`Rundeck`和`Jenkins`的集成并不是很稳定，决定尝试`CircleCI` 持续整合＆持续交付工具。

![](http://pics.naaln.com/blog/2019-01-14-060820.jpg)

- `CI`和接入版本控制

- 代码`push`集成单元测试

- 提交代码到开放版本

- 生产`Docker`，并部署到开发环境

- 进行人工测试

- 测试成功后，部署`Docker`到生产环境

----------

