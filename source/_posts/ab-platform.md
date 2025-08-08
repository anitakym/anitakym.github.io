---
title: ab-platform
date: 2024-03-07 10:15:31
tags:
---
- featureProbe
- 调试阶段，自己拉项目进行部署

- https://github.com/FeatureProbe
- https://gitee.com/featureprobe/FeatureProbe/blob/main/README_CN.md
目前是没有特性发布的状态，Android端客户端SDK有BUG，但是只能使用方自行兜底处理；
（https://github.com/FeatureProbe/client-sdk-mobile/tree/main）

```
FeatureProbe适用于哪些场景
根据我们的经验，FeatureProbe可以在以下场景中提升软件研发的效能:

『特性粒度』灰度发布: 每个功能独立灰度发布给用户。可迅速关闭受BUG影响的功能，同时不影响其他正常功能的使用。
降低测试环境搭建成本: 节约测试环境搭建和线下测试时间成本。利用线上环境小流量测试，环境真实同时影响可控。
降低故障恢复时间:故障发生时通过降级策略调整服务行为，保障用户主路径不受影响。
简化研发协同方式: 用功能开关替代传统分支开发的团队协同模式。真正实现主干开发、持续部署。减少分支合并冲突，显著加快迭代速度。
统一的配置管理中心: 通过用户友好的操作页面，统一操作线上配置，实时修改功能参数，让运营活动生效更简单。
```

- feature probe已经两年没有维护了

- https://github.com/openflagr/flagr
- openflagr/flagr is a community-driven OSS effort of advancing the development of Flagr.
openflagr/flagr 是一个由社区驱动的开源项目，旨在推进 Flagr 的发展。

Flagr is an open source Go service that delivers the right experience to the right entity and monitors the impact. It provides feature flags, experimentation (A/B testing), and dynamic configuration. It has clear swagger REST APIs for flags management and flag evaluation.
Flagr 是一个开源的 Go 服务，为合适的实体提供合适的功能体验，并监控其影响。它提供功能标志、实验（A/B 测试）和动态配置。它具有清晰的 swagger REST API 用于标志管理和标志评估。


- https://openfeature.dev/
- # OpenFeature 平台解析

OpenFeature 是一个开源的功能标志（Feature Flag）**标准化框架**，它不是一个具体的功能标志服务，而是一个规范和接口层。

## OpenFeature 的核心定位

OpenFeature 提供了一个与供应商无关的、开放的 API 标准，用于实现功能标志和 A/B 测试功能。其主要价值在于：

### 1. 标准化 API
- 提供统一的功能标志 API 规范
- 支持多种编程语言（Java、Go、JavaScript、.NET等）
- 使用相同的概念模型和功能集

### 2. 供应商中立
- **不绑定**到任何特定的功能标志服务提供商
- 允许在不修改应用代码的情况下切换不同的功能标志后端

### 3. 插件化架构
- 通过"提供者"（Providers）连接不同的功能标志服务
- 可以集成到现有平台如 LaunchDarkly、Split、Flagr 等

## 工作原理

OpenFeature 通过以下方式工作：

```
应用代码 → OpenFeature SDK → 提供者(Provider) → 功能标志后端服务
```

1. 开发者使用标准化的 OpenFeature API
2. "提供者"负责与特定的功能标志平台通信
3. 可以轻松切换或集成不同的功能标志服务

## 与其他平台的关系

- **与 FeatureProbe/Flagr 的关系**：这些是功能标志的具体实现平台，而 OpenFeature 提供标准 API 来使用这些平台
- **CNCF 项目**：OpenFeature 是云原生计算基金会（CNCF）的孵化项目，致力于功能标志技术的标准化

## 主要优势

1. **避免供应商锁定**：可以轻松迁移到不同的功能标志平台
2. **简化开发**：开发者只需学习一套 API
3. **统一体验**：在不同语言和框架中保持一致的功能标志体验
4. **生态系统**：促进开放、互操作的功能标志生态系统

OpenFeature 本质上是连接应用程序和各种功能标志服务的中间层，提供了标准化的方式来实现功能标志，而不是一个完整的功能标志平台。

# 从FeatureProbe迁移到Flagr（使用OpenFeature）

如果您已经通过OpenFeature接入了功能标志系统，从FeatureProbe迁移到Flagr的过程相对简单，主要涉及替换Provider而不需要修改应用代码。

## 迁移步骤

1. **创建相同的功能标志**:
   - 在Flagr平台上创建与FeatureProbe中相同的功能标志
   - 确保功能标志名称、规则和配置与原有系统一致

2. **替换Provider**:
   ```java
   // 原FeatureProbe的Provider
   // FeatureProbeProvider featureProbeProvider = new FeatureProbeProvider(config);
   // OpenFeatureAPI.getInstance().setProvider(featureProbeProvider);
   
   // 替换为Flagr的Provider
   FlagrProvider flagrProvider = new FlagrProvider(flagrConfig);
   OpenFeatureAPI.getInstance().setProvider(flagrProvider);
   ```

3. **更新配置**:
   - 更新连接信息、API密钥等Flagr特定配置
   - 验证功能标志评估正确性

4. **灰度迁移**（推荐）:
   - 先在非关键环境测试
   - 逐步迁移到生产环境

## SDK冲突问题

关于FeatureProbe SDK和OpenFeature SDK可能的冲突:

1. **若同时使用两套SDK**:
   - **会产生冲突**：两者使用不同的初始化方式、缓存机制和评估逻辑
   - **维护成本增加**：需要维护两套功能标志代码和配置
   - **行为不一致**：可能导致同一功能标志在不同SDK中行为不一致

2. **推荐做法**:
   - **选择一种方式**：要么使用OpenFeature + Provider，要么直接使用平台SDK
   - 如果已经使用OpenFeature，继续使用它并仅替换Provider
   - 如果直接使用FeatureProbe SDK，则需要重构代码以适应Flagr的SDK

## 最佳实践

- OpenFeature的设计初衷就是避免这种迁移的痛苦
- 使用OpenFeature作为统一接口，只需更换Provider而不必修改业务代码
- 避免在同一项目中混合使用不同的功能标志SDK

使用OpenFeature的最大优势就是在这种平台迁移场景中体现 - 您只需替换"Provider"部分，而应用代码无需任何改变。


### featbit
- https://github.com/featbit/featbit
-Features  特性
FeatBit offers a range of features including:
FeatBit 提供一系列功能，包括：

SDKs for .NET(C#), JavaScript, React, React Native, NodeJs, Java, Python, Go, and OpenFeature Providers, with more to come.
适用于 .NET(C#)、JavaScript、React、React Native、NodeJs、Java、Python、Go 以及 OpenFeature 提供者的 SDK，未来还将推出更多。

Managing Feature flags: Create, manage, and filter feature flags.
管理功能标志：创建、管理和筛选功能标志。

Targeting users with flags: Assign individual users to specific flag variations.
使用标志定位用户：将单个用户分配到特定的标志变体。

Reusable Segments: Include or exclude users from a segment based on user attributes.
可重用分段：根据用户属性将用户包含或排除在分段中。

Insights: Gain insights into feature usage during the rollout.
洞察：在功能发布期间了解功能使用情况。

IAM: Define access levels to projects, environments, or teams to enforce your policies.
身份和访问管理：定义对项目、环境或团队的访问级别以执行您的策略。

Experimentation: Run feature-level A/B tests anywhere in your stack to make data-driven decisions.
实验：在您的技术栈中的任何位置运行功能级别的 A/B 测试，以做出数据驱动的决策。

Audit Log: Keep track of feature flag and segment changes.
审计日志：跟踪功能开关和分段的变更。

Feature Workflow: Control your use of feature flags by creating complex automated workflows within FeatBit (Flag Triggers, Scheduled Flag Changes, Change Approve Requests).
功能工作流：通过在 FeatBit 中创建复杂的自动化工作流来控制功能开关的使用（标志触发器、计划标志变更、变更审批请求）。

Web APIs, automate your workflow with Web APIs.
Web API，通过 Web API 自动化您的流程。

SSO, integrate with your existing Identity Provider.
SSO，与您现有的身份提供者集成。

Platform-level, manage your flags in multiple projects and environments.
平台级，在多个项目和环境中管理您的功能标志。

Pro Solution for Big Data, a professional version tailored for teams and companies to accommodate in excess of millions of daily online users with feature usage, custom events, and A/B testing insights.
适用于大数据的专业解决方案，专为团队和企业设计，可容纳数百万日在线用户，支持功能使用、自定义事件和 A/B 测试洞察。

Relay Proxy/Agent: Host a feature flag service in your customers' private environments or reduce network latency for your end users.
Relay 代理/代理：在客户的私有环境中托管功能开关服务，或减少最终用户的网络延迟。

Powerful Integrations: Our feature-rich WebHook allows seamless integration with various tools and workflows: DataDog, New Relic Ones, Grafana, Growthbook, Slack and more.
强大的集成：我们功能丰富的 WebHook 允许与各种工具和工作流程无缝集成：DataDog、New Relic Ones、Grafana、Growthbook、Slack 等。

ChatGPT Tech Debt Reduction (experimental features): Utilize ChatGPT4 and FeatBit's VSCode extension to minimize technical debt associated with feature flagging.
ChatGPT 技术债务减少（实验性功能）：利用 ChatGPT4 和 FeatBit 的 VSCode 扩展，以减少与功能开关相关的技术债务。

OpenTelemetry Integration: Enhance system visibility with OpenTelemetry for logs, traces, and metrics.
OpenTelemetry 集成：通过 OpenTelemetry 增强系统可见性，用于日志、跟踪和指标。

Helm Charts Installation, FeatBit can be installed on-premises, in the cloud, or in a hybrid environment through Helm Charts.
Helm Charts 安装，FeatBit 可以通过 Helm Charts 在本地、云端或混合环境中进行安装。

### growthbook
GrowthBook is an open source Feature Flagging and Experimentation platform. Built for high performance and to be completely customizable, we help companies easily launch features and figure out their impact using their own data. Available from our Cloud or self-hosted.
- 自部署，功能要求多的话，可以购买pro或者企业版
