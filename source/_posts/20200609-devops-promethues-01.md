---
title: Prometheus--（一）简介
date: 2020-06-09 22:13:57
tags:
- Monitor
- Prometheus
categories:
- DevOps
---
## 概览

普罗米修斯是一个开源系统监控和警报工具包，最初是在SoundCloud构建的。自2012年成立以来，许多公司和组织都采用了普罗米修斯，该项目拥有一个非常活跃的开发人员和用户社区。它现在是一个独立的开源项目，独立于任何公司进行维护。为了强调这一点，并澄清项目的治理结构，普罗米修斯于2016年加入了云原生计算基金会，成为继Kubernetes之后的第二个托管项目。

### 特性

- 用度量名和键值对识别时间序列数据的多维数据模型
- PromQL，一种多维灵活的查询语言
- 不依赖分布式存储；单服务器节点，服务自治
- 通过HTTP上的pull模型进行时间序列收集
- 通过中间网关可支持推送时间序列
- 通过服务发现或静态配置发现目标
- 支持多种图形和仪表板

### 组件

普罗米修斯生态系统由多个组件组成，其中许多组件是可选的：
- 普罗米修斯服务，用于收集和存储时间序列数据
- 客户端库，用于检测应用程序代码
- 推送网关，支持短期作业
- 支持特定出口，如HAProxy、StatsD、Graphite等。
- 处理警报的警报管理器
- 各种支撑工具

### 架构

此图说明了普罗米修斯的建筑及其生态系统的一些组成部分：

![架构图](https://prometheus.io/assets/architecture.png)


普罗米修斯直接或通过短生命作业的中间推送网关从检测作业中获取度量。

它在本地存储所有刮取的样本，并在此数据上运行规则，以便从现有数据中聚合和记录新的时间序列或生成警报。可以使用Grafana等UI工具，将收集的数据可视化。


### 优点：

普罗米修斯对于记录任何纯数字时间序列都很有效。它既适合以机器为中心的监视，也适合高度动态的面向服务的体系结构的监视。在微服务的世界里，它对多维数据收集和查询的支持是一个特别的优势。

普罗米修斯是为可靠性而设计的，它是一个系统，可以让你在停电时快速诊断问题。每台普罗米修斯服务器都是独立的，不依赖于网络存储或其他远程服务。当基础设施的其他部分损坏时，可以依赖它，而不需要设置广泛的基础设施来使用它。

### 缺点：

普罗米修斯重视可靠性。即使在出现故障的情况下，你也可以始终查看系统的可用统计信息。如果你需要100%的准确度，例如按请求计费，普罗米修斯不是一个好的选择，因为收集的数据可能不够详细和完整。在这种情况下，最好使用其他系统来收集和分析计费数据，并使用普罗米修斯进行其余的监控。

如果做日志监控，建议使用ELK；如果对时序性有强烈的要求，可以使用Influxdb+Grafana做实时监控。









