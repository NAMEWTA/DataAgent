# 03 - 核心业务模块详解

> **模块状态**: ⏳ 待填充  
> **上级目录**: [← 返回索引](../00-index.md)

---

## 🎮 控制器层 (Controller)

| 控制器 | 端点前缀 | 职责 |
|--------|----------|------|
| `AgentController` | `/api/agent` | 智能体 CRUD |
| `ChatController` | `/api/chat` | 对话会话管理 |
| `DatasourceController` | `/api/datasource` | 数据源管理 |
| `GraphController` | `/api/graph` | 工作流图执行 |
| `ModelConfigController` | `/api/model` | 模型配置 |
| `SemanticModelController` | `/api/semantic` | 语义模型管理 |
| `BusinessKnowledgeController` | `/api/knowledge` | 知识库管理 |
| `PromptConfigController` | `/api/prompt` | Prompt 配置 |
| `FileUploadController` | `/api/file` | 文件上传 |
| ... | ... | ... |

---

## 🔧 服务层 (Service)

### 服务模块概览

| 模块 | 类数量 | 核心职责 |
|------|--------|----------|
| `agent/` | 5 | 智能体生命周期管理 |
| `chat/` | 6 | 对话流程与消息处理 |
| `datasource/` | 11 | 数据源连接与元数据 |
| `knowledge/` | 5 | 知识库存储与检索 |
| `llm/` | 5 | LLM 模型调用封装 |
| `nl2sql/` | 2 | 自然语言转 SQL |
| `code/` | 6 | Python 代码执行 |
| `vectorstore/` | 3 | 向量数据库操作 |
| `hybrid/` | 9 | 混合检索策略 |
| `graph/` | 4 | 工作流图管理 |
| `semantic/` | 3 | 语义模型处理 |
| `prompt/` | 2 | Prompt 模板管理 |
| `mcp/` | 1 | MCP 协议服务 |
| ... | ... | ... |

---

## 🔄 子模块详解

待后续填充...
