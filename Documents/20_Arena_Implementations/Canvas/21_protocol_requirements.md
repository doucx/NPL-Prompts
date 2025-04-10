#  ACP Canvas 协议扩展
## 基本介绍
**ACP Canvas** 中的 **ACP Textual Aren** 扩展规范。

## 核心原则
ACP Canvas 协议设计基于以下核心原则：
*   **类XML格式**:  Arena Context 是 类似XML格式的文本。所有指令、数据和元信息都以XML格式交换。由于Canvas是基于Cognitor运行的，因此Canvas中的XML格式相比于一般的XML格式更加松。

## 核心实体
### Arena
*   **定义**: 在 Canvas 环境下，Arena 代表了遵循 ACP Canvas 协议规范的交互空间。它**必须**通过可审计的文本记录（`<Cell>` 序列和 `<ArenaLog>`）来维护交互上下文和状态。
*   **核心协议要求**:
    1.  **上下文管理**: Arena **必须**能够解析和管理构成交互历史的 `<Cell>` 序列，并维护其间的依赖关系（显式通过 `<depends_on>` 或隐式推断）。
    2.  **Cell 处理**: **必须**定义如何处理不同类型的 `<Cell>` (`EXEC`, `OUTPUT`, `INPUT` 等)，包括何时创建新的 Cell 以及 Cell 之间的状态转换逻辑（例如，`EXEC` 后通常跟随 `OUTPUT`，`input()` 调用需等待 `INPUT`）。
    3.  **指令路由**: 对于 `EXEC` Cell，Arena **必须**有明确的机制来决定是由其内部模拟执行、路由给特定 PersonaCognitor（如 Fhrsk）、还是根据 `target_cognitor` 属性委托给其他指定 Cognitor 执行。
    4.  **过程透明性**: Arena 的关键决策（如路由、信息推断、状态转换）**必须**通过 `<ArenaLog>` 中的结构化日志进行记录，以确保可审计性。
    5.  **纯文本基础**: **必须**确保所有交互状态和历史完全通过 Canvas 的类 XML 文本格式进行表示和存储。
*   **实现说明**: Canvas Arena 的具体行为（如详细的状态机逻辑、路由规则实现）由负责模拟 Arena 的 `Cognitor` 实现，并记录在 `20_Arena_Implementations/Canvas/23_canvas_implementation.md` 中。本文件仅定义协议层面的核心要求。

## 关键协议机制
### Logs (日志系统)
*   **定义** : 在 Canvas 中，`Logs` 嵌入到 `<log>` 节点中。
