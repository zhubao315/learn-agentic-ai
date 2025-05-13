# 使用 Dapr Agentic Cloud Ascent (DACA) 设计模式学习 Agentic AI：从入门到规模化

该仓库是 [Panaversity 认证 Agentic & Robotic AI 工程师](https://docs.google.com/document/d/15usu1hkrrRLRjcq_3nCTT-0ljEcgiC44iSdvdqrCprk/edit?usp=sharing) 计划的一部分，涵盖 AI-2[...]。

我们有两个假设，巴基斯坦的未来取决于这些假设，让我们确保它们正确无误：

对于巴基斯坦来说，押注即将到来的 Agentic AI 时代的正确技术非常重要。我们将在巴基斯坦及全球范围内在线培训数百万名 Agentic AI 开发者。

### 假设 #1：Dapr
我们认为 Dapr、Dapr Actors、Dapr Workflows 和 Dapr Agents 将是构建下一代多 AI Agentic 系统的核心技术，我的假设正确吗？

### 假设 #2：OpenAI Agents SDK
我们也认为 OpenAI Agents SDK 将是初学者学习 Agentic AI 的首选框架？

让我们看看最好的 AI 对我们的假设有什么看法：

https://chatgpt.com/share/6811b893-82cc-8001-9037-e45bcd91cc64  
https://g.co/gemini/share/1f31c876520b  
https://grok.com/share/bGVnYWN5_4343d342-c7df-4b06-9174-487a64f59d53  

---

## 这个 Panaversity 项目应对的关键挑战：

**“如何设计能够处理 1000 万个并发 AI 代理而不失败的 AI 代理？”**

注：由于训练期间财务资源有限，我们必须指导学生以最小的成本解决这个问题。

<p align="center">
<img src="./img/cover.png" width="600">
</p>

Kubernetes 与 Dapr 理论上可以在 Agentic AI 系统中处理 1000 万个并发代理而不失败，但要实现这一目标需要广泛的优化、显著的基础设施和[...]。

**论点摘要及逻辑证明**：

1. **Kubernetes 可扩展性**：
   - **证据**：Kubernetes 支持每个集群最多 5000 个节点和 15 万个 pod（Kubernetes 文档），真实案例如 PayPal 扩展到 4000 个节点和 20 万个 pod（InfoQ, 2023）[...]
   - **逻辑**：对于 1000 万用户，5000–10000 个节点的集群（例如 AWS g5 实例与 GPU）可以分配工作负载。每个节点可以运行数百个 pod，而 Kubernetes 的水平扩展[...]

2. **Dapr 在 Agentic AI 中的高效性**：
   - **证据**：Dapr 的 Actor 模型支持每个 CPU 核心成千上万个虚拟 Actor，延迟为两位数毫秒（Dapr 文档，2024）。案例研究显示 Dapr 能够处理数百万事件，e[...]
   - **逻辑**：Agentic AI 依赖于状态化、低延迟的代理。基于 Actor 模型的 Dapr Agent 可以将 1000 万用户表示为 Actor，分布在 Kubernetes 集群中。Dapr 的 st[...]

3. **处理 AI 工作负载**：
   - **证据**：LLM 推理框架如 vLLM 和 TGI 每 GPU 每秒可处理数千个请求（vLLM 基准测试，2024）。Kubernetes 有效协调 GPU 工作负载，案例如 Kubernetes[...]
   - **逻辑**：假设每个用户每秒生成 1 个请求，需要 0.01 GPU，则 1000 万用户需要约 10 万个 GPU。通过批处理、缓存和模型并行性可将需求减少到约 1 万–2 万[...]

4. **网络和存储**：
   - **证据**：EMQX 在 Kubernetes 上通过优化处理了 100 万个并发连接（EMQX 博客，2024）。C10M 基准测试（2013）通过优化栈实现了 1000 万连接。Dapr 的 st[...]
   - **逻辑**：1000 万连接需要约 100–1000 Gbps 带宽，现代云支持此需求。高吞吐量数据库（例如 CockroachDB）和缓存（例如 Redis 集群）可处理 10 TB 的[...]

5. **弹性与监控**：
   - **证据**：Dapr 的弹性策略（重试、断路器）和 Kubernetes 的自愈功能（pod 重启）确保了可靠性（Dapr 文档，2024）。Dapr 的 OpenTelemetry 集成扩展[...]
   - **逻辑**：实时指标（例如延迟、错误率）和分布式追踪防止级联故障。Kubernetes 的存活探针和 Dapr 的工作流引擎从崩溃中恢复，确保[...]

**在约束条件下的可行性**：
- **挑战**：没有直接的基准表明在 Agentic AI 环境中使用 Dapr/Kubernetes 处理 1000 万并发用户的能力。基础设施成本（例如 1 万–1 亿美元用于 1 万个节点）对[...]
- **解决方案**：使用开源工具（例如 Minikube、kind）进行本地测试，为学生提供云信用（例如 AWS Educate）。通过工具如 Locust 模拟 1000 万用户的小型集群[...]

**结论**：Kubernetes 与 Dapr 能够在 Agentic AI 系统中处理 1000 万并发用户，其可扩展性已被证明，真实案例研究和逻辑推导也支持这一论点。对于学[...]

---

**2025 年 Agentic AI 的顶级趋势**

<p align="center">
<img src="./img/toptrend.webp" width="200">
</p>

---

## Dapr Agentic Cloud Ascent (DACA) 设计模式解决 1000 万 AI 代理挑战

让我们来了解和学习“Dapr Agentic Cloud Ascent (DACA)”——开发和部署全球规模多代理系统的制胜设计模式。

### 执行摘要：Dapr Agentic Cloud Ascent (DACA)

Dapr Agentic Cloud Ascent (DACA) 指南介绍了一种战略设计模式，用于构建和部署复杂、可扩展且具有弹性的 Agentic AI 系统。解决现代化体系结构的复杂性[...]


**[Dapr Agentic Cloud Ascent (DACA) 设计模式综合指南](https://github.com/panaversity/learn-agentic-ai/blob/main/comprehensive_guide_daca.md)**

<p align="center">
<img src="./img/ascent.png" width="500">
</p>

<p align="center">
<img src="./img/architecture1.png" width="400">
</p>

---

### 目标用户
- **Agentic AI 开发者和 AgentOps 专业人士**

### 为什么 OpenAI Agents SDK 应成为大多数用例的主要开发框架？

**表 1：AI 代理框架抽象级别对比**

| **框架**                | **抽象级别**      | **关键特性**                                                                                 | **学习曲线**   | **控制级别**  | **简洁性**  |
|-----------------------|-----------------|-----------------------------------------------------------------------------------------|--------------|--------------|-----------|
| **OpenAI Agents SDK** | 最小化          | Python 优先，核心原语（代理、交接、护栏），直接控制                                          | 低           | 高           | 高         |
| **CrewAI**            | 中等            | 基于角色的代理、团队、任务，专注于协作                                                     | 低-中         | 中           | 中         |
| **AutoGen**           | 高             | 会话代理、灵活的会话模式、人工干预支持                                                     | 中           | 中           | 中         |
| **Google ADK**        | 中等            | 多代理层级、Google 云集成（Gemini, Vertex AI）、丰富的工具生态系统、双向流式传输                  | 中           | 中-高        [...]
| **LangGraph**         | 低-中           | 基于图的工作流、节点、边、显式状态管理                                                    | 非常高         | 非常高        | 低         |
| **Dapr Agents**       | 中等            | 状态化虚拟 Actor、事件驱动的多代理工作流、Kubernetes 集成、50+ 数据连接器、内置弹性           | 中           | 中           [...]

表格清晰地说明了为什么 OpenAI Agents SDK 应成为大多数用例的主要开发框架：
- 它在**简洁性**和**易用性**方面表现出色，使其成为快速开发和广泛可用性的最佳选择。
- 它提供**高控制**和**最小抽象**，在不增加复杂性的情况下提供了 Agentic 开发所需的灵活性。
- 与大多数替代方案（CrewAI、AutoGen、Google ADK、Dapr Agents）相比，它在可用性和功能之间取得了更好的平衡，而 LangGraph 提供了更多控制，但其复杂性使得它在通用[...]

如果优先考虑易用性、灵活性和 Agentic 开发的快速迭代，基于表格，OpenAI Agents SDK 是明确的赢家。然而，如果您的项目需要企业级功能[...]

---

## 核心 DACA Agentic AI 课程：

### AI-201：Agentic AI 和 DACA AI-First 开发基础（14 周）

- ⁠Agentic & DACA 理论 - 1 周
- UV 和 OpenAI Agents SDK - 5 周
- ⁠Agentic 设计模式 - 2 周
- ⁠内存 [LangMem & mem0] - 1 周
- Postgres/Redis（托管云） - 1 周
- FastAPI（基础） - 2 周
- ⁠容器化（Rancher Desktop） - 1 周
- Hugging Face Docker Spaces - 1 周

**[AI-201 视频播放列表](https://www.youtube.com/playlist?list=PL0vKVrkG4hWovpr0FX6Gs-06hfsPDEUe6)**

注：这些视频用于额外学习，不涵盖所有现场课程内容。

先决条件：[AI-101：现代 AI Python 编程 - 通向智能系统的起点](https://github.com/panaversity/learn-modern-ai-python)

---

### AI-202：DACA 云优先 Agentic AI 开发（14 周）
- 使用本地 Kubernetes 的 Rancher Desktop - 4 周
- 高级 Kubernetes FastAPI - 2 周
- Dapr [工作流，状态，发布订阅，密钥管理] - 3 周
- CockRoachDB 和 RabbitMQ 托管服务 - 2 周
- ⁠模型上下文协议 -  2 周
- ⁠无服务器容器部署（ACA） - 2 周

先决条件：成功完成 AI-201

---

### AI-301：DACA 全球规模分布式 AI 代理（14 周）
- ⁠认证 Kubernetes 应用开发者 (CKAD) - 4 周
- ⁠A2A 协议 - 2 周
- ⁠语音代理 - 2 周
- ⁠Dapr 代理/Google ADK - 2 周
- ⁠自托管 LLMs - 1 周
- 微调 LLMs - 3 周

先决条件：成功完成 AI-201 和 AI-202
