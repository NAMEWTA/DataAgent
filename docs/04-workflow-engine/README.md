# 04 - StateGraph 工作流引擎

> **模块状态**: ⏳ 待填充  
> **上级目录**: [← 返回索引](../00-index.md)

---

## 🔗 工作流节点 (Node)

系统定义了 16 个工作流节点：

| 节点 | 文件 | 阶段 | 职责 |
|------|------|------|------|
| `IntentRecognitionNode` | 3.4KB | 意图理解 | 识别用户查询意图 |
| `QueryEnhanceNode` | 3.9KB | 意图理解 | 查询语句增强 |
| `SchemaRecallNode` | 4.8KB | Schema 检索 | 召回相关表结构 |
| `EvidenceRecallNode` | 14.6KB | Schema 检索 | 召回业务证据与知识 |
| `TableRelationNode` | 11.2KB | Schema 检索 | 推理表之间的关联关系 |
| `SqlGenerateNode` | 7.1KB | SQL 阶段 | 生成 SQL 语句 |
| `SqlExecuteNode` | 12.8KB | SQL 阶段 | 执行 SQL 并处理结果 |
| `SemanticConsistencyNode` | 4.4KB | SQL 阶段 | 校验语义一致性 |
| `FeasibilityAssessmentNode` | 3.2KB | 计划阶段 | 评估任务可行性 |
| `PlannerNode` | 5.2KB | 计划阶段 | 生成执行计划 |
| `PlanExecutorNode` | 7.0KB | 计划阶段 | 执行计划步骤 |
| `HumanFeedbackNode` | 3.0KB | 计划阶段 | 接收人工反馈 |
| `PythonGenerateNode` | 5.6KB | Python 阶段 | 生成 Python 代码 |
| `PythonExecuteNode` | 7.0KB | Python 阶段 | 执行 Python 代码 |
| `PythonAnalyzeNode` | 4.2KB | Python 阶段 | 分析执行结果 |
| `ReportGeneratorNode` | 10.1KB | 报告阶段 | 生成最终报告 |

---

## 🚦 调度器 (Dispatcher)

| 调度器 | 职责 |
|--------|------|
| `IntentRecognitionDispatcher` | 意图识别路由 |
| `QueryEnhanceDispatcher` | 查询增强路由 |
| `SchemaRecallDispatcher` | Schema 召回路由 |
| `TableRelationDispatcher` | 表关系路由 |
| `SqlGenerateDispatcher` | SQL 生成路由 |
| `SQLExecutorDispatcher` | SQL 执行路由 |
| `SemanticConsistenceDispatcher` | 语义一致性路由 |
| `FeasibilityAssessmentDispatcher` | 可行性评估路由 |
| `PlanExecutorDispatcher` | 计划执行路由 |
| `HumanFeedbackDispatcher` | 人工反馈路由 |
| `PythonExecutorDispatcher` | Python 执行路由 |

---

## 📊 工作流图

待后续填充...
