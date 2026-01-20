# 02.3 - 数据生命周期与流向

> **模块状态**: ✅ 已完成  
> **上级目录**: [← 返回数据模型总览](./README.md)

---

## 🔄 数据生命周期全景

系统中的数据大体经历三个阶段：**配置生成 → 知识增强 → 交互沉淀**。

```mermaid
flowchart LR
    A[配置生成] --> B[知识增强]
    B --> C[交互沉淀]

    subgraph 配置生成
        A1[创建 Agent]
        A2[配置 Datasource]
        A3[绑定 AgentDatasource]
        A4[维护 SemanticModel]
        A5[维护 LogicalRelation]
        A1 --> A2 --> A3 --> A4 --> A5
    end

    subgraph 知识增强
        B1[上传 AgentKnowledge]
        B2[维护 BusinessKnowledge]
        B3[向量化任务]
        B1 --> B3
        B2 --> B3
    end

    subgraph 交互沉淀
        C1[创建 ChatSession]
        C2[写入 ChatMessage]
        C3[结果归档/复盘]
        C1 --> C2 --> C3
    end
```

---

## 🧭 关键数据流向说明

### 1) 结构化数据流向（以 SQL 为核心）

```mermaid
sequenceDiagram
    participant User as 用户
    participant Agent as Agent
    participant DS as Datasource
    participant SM as SemanticModel
    participant LR as LogicalRelation
    participant SQL as SQL引擎

    User->>Agent: 发起问题
    Agent->>SM: 获取字段语义
    Agent->>LR: 获取表关联逻辑
    Agent->>DS: 获取连接信息
    Agent->>SQL: 生成并执行SQL
    SQL-->>Agent: 返回结果集
    Agent-->>User: 生成自然语言回答
```

**业务意义**：
- `SemanticModel` 与 `LogicalRelation` 是 SQL 生成质量的关键变量，缺失会导致 SQL 结构错误或召回不足。

**二次开发指南**：
- 若引入新的 SQL 生成策略，应在生成前统一聚合语义模型与逻辑关系，避免业务逻辑分散在多个节点中。

---

### 2) 知识增强流向（以向量化为核心）

```mermaid
sequenceDiagram
    participant User as 用户
    participant AK as AgentKnowledge
    participant BK as BusinessKnowledge
    participant Embed as Embedding任务
    participant Store as 向量存储

    User->>AK: 上传文档/QA/FAQ
    User->>BK: 维护业务术语
    AK->>Embed: 进入向量化队列
    BK->>Embed: 进入向量化队列
    Embed->>Store: 写入向量索引
```

**业务意义**：
- `embeddingStatus` 是知识可用性的“状态机”，是前端轮询与后端重试的依据。

**二次开发指南**：
- 若接入新的向量数据库，需保证向量写入与业务表状态更新的事务一致性。

---

### 3) 对话沉淀流向（以会话为核心）

```mermaid
sequenceDiagram
    participant User as 用户
    participant Session as ChatSession
    participant Msg as ChatMessage
    participant Result as 结果/报告

    User->>Session: 创建会话
    User->>Msg: 提交问题
    Msg->>Result: 触发分析/SQL/报告
    Result-->>Msg: 写入assistant回复
```

**业务意义**：
- `ChatMessage` 既是对话记录，也是调试与回溯的审计依据。

**二次开发指南**：
- 若要支持“对话回放”，必须保持 `ChatMessage` 的顺序与角色一致性。
