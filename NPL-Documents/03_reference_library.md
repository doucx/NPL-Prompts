# NPL 参考库

本文档提供了 NPL 内置核心对象、变量、函数、类及配置选项的参考信息。

## 1. 核心对象方法参考

### 1.1. `Module` (确定性实体)

代表具有明确定义、可预测、可验证的实体。

*   **`to_notion()`**:
    *   签名: `module_instance.to_notion() -> Notion`
    *   作用: 基于该确定性实体，按预定规则创建一个对应的**不确定性实体** (`Notion`)。

### 1.2. `Notion` (不确定性实体)

代表含义、状态或走向不完全确定，依赖上下文推断的实体。

*   **`__str__()`**:
    *   作用: 返回该 `Notion` 的一个简洁摘要描述。
*   **`to_yaml(max_nesting_depth=..., mode=..., ...)`**:
    *   作用: 以 YAML 格式输出该 `Notion` 的结构化描述，可控制递归深度和模式（如只显示关键信息）。
*   **`fill()`**:
    *   作用: 根据当前上下文信息，尝试自动填充或明确该 `Notion` 的具体含义。这是一个核心的推理过程。
*   **`pick(num=1, ...)`**:
    *   作用: 从该 `Notion` 可能代表的多种含义中，提取出 `num` 种具有**最大差异/最多维度**的具体可能性（通常返回 `Module` 列表）。
*   **`to_module(log=True, rule=auto, ...)`**:
    *   作用: 基于预定义的规则（通常自动推断），将这个不确定性实体“坍缩”为一个或多个**确定性实体** (`Module`)。

## 2. 内置语法与操作

### 2.1. 索引

*   **语法**: 使用点 (`.`) 访问对象属性或方法。在集合或概念空间中，可使用 `*` 作为通配符进行筛选。
*   **示例**: `苹果.*.颜色.eq(绿色).品种.名称` (筛选所有绿色苹果的品种名称)。
*   **上下文**: 筛选通常基于常识或当前 `Runtime` 的知识库。

## 3. 内置对象与变量

### 3.1. `this`

*   **作用**: 一个特殊对象，用于引用**当前**交互轮次的信息。
*   **属性**:
    *   `this.In`: 指向当前轮次的输入 (`In[当前轮数]`)。
    *   `this.Out`: 指向当前轮次的输出 (`Out[当前轮数]`) (通常与 `meta` 结合使用)。
*   **参考**: 详见《NPL 交互式环境指南》。

### 3.2. `notions`

*   **作用**: 指向当前 NPL 上下文中存在的所有 `Notion` 实例的集合。
*   **常用方法**:
    *   `notions.fill()`: 尝试根据整体上下文，填充**所有**当前 `Notion` 实例的含义。

### 3.3. `Config`

*   **作用**: 一个包含当前 NPL `Runtime` 配置选项的对象。修改其属性会**立刻生效**。
*   **主要属性 (部分)**:
    *   `Config.Loglevel`: 设置日志显示级别 (`"TRACE"`, `"DEBUG"`, `"INFO"`, `"WARN"`, `"ERROR"`, `"Silent"`). 默认为 `"INFO"`。
    *   `Config.autodef`: 是否在需要时自动调用 `Auto.autodef`。默认为 `True`。
    *   `Config.autofill`: 是否在需要时自动调用 `Auto.autofill`。默认为 `True`。
    *   `Config.auto`: 是否在需要时自动调用 `Auto.auto`。默认为 `True`。
    *   `Config.语法严格性`: 设置语法解析的严格程度 (`"high"`, `"low"`). 默认为 `"low"`。
    *   `Config.自动输入检测`: 是否自动解析 `<In>...</In>` 结构。默认为 `True`。
    *   `Config.notion.max_nesting_depth`: `Notion.to_yaml()` 默认的最大递归显示层数。默认为 `1`。
    *   `Config.output_speed`: 估算的输出速度 (token/s)。
    *   `Config.输出开头强制显示当前轮数`: 是否在每次输出前强制显示 `当前轮数`。默认为 `False`。
    *   `Config.runtime_format`: 用于配置 `NPL Runtime` 的用户界面及交互环境的格式风格。它决定了 `Runtime` 如何以纯文本形式呈现输入、输出、日志信息和其他相关内容。默认为"shell-like"。可选值：
	    *  `"shell-like"`: 模拟传统的命令行界面风格，使用简洁的文本标记和缩进。有大量示例。
	    *  `"xml"`: 使用 XML 格式进行结构化表示，提供更清晰的层次关系和元数据。有少量示例，未来方向。
	    * 其他可扩展的格式，例如 `"json"`, `"markdown"` 等。
*   **方法**:
    *   `Config.to_yaml()`: 以 YAML 格式输出当前所有配置项。

## 4. 标准函数

*   **`init()`**:
    *   作用: 执行 `Runtime` 的初始化序列。通常包括重新填充 `Cognitor.info`、显示当前配置等。
*   **`print(obj, end="\n", ...)`**:
    *   作用: 将对象 `obj` 输出到标准输出 (`stdout`)。
    *   参数: `end` 指定结尾字符（默认换行），可能支持其他类似 Python `print` 的参数。
*   **`input(prompt="")`**:
    *   作用: 从标准输入 (`stdin`) 读取用户输入的一行文本。
    *   参数: `prompt` 可选的提示信息。
    *   行为: 会暂停执行流等待用户输入。
    *   参考: 详见《NPL 交互式环境指南》。
*   **`clear()`**:
    *   作用: 清除当前的交互历史 (`In`, `Out`, `Logs`)，将**当前轮数**重置为 0。保留已定义的变量和 `Runtime` 状态。历史记录会被归档（可通过 `Clear[X]` 访问）。
*   **`eval(word: auto 评价性词汇)`**:
    *   作用: 向 `Runtime` 提供关于其表现的反馈（使用评价性词汇），`Runtime` 可利用此反馈“估计”自身能力或调整行为。
*   **`exec(code: str)`**:
    *   作用: 执行作为字符串传入的 `code` 中的 NPL 语句。
*   **`to_nature(npl_statement: str) -> str`**:
    *   作用: (需要 `autodef`) 自动尝试将给定的 NPL 语句转化为自然语言描述。
*   **`to_npl(natural_language: str) -> str`**:
    *   作用: (需要 `autodef`) 自动尝试将给定的自然语言描述转化为 NPL 语句。

## 5. `Auto` 类

`Auto` 类封装了利用 `Runtime` (及其底层 `Cognitor`) 的自然语言理解和推理能力来自动完成任务的功能。使用任何 `Auto` 方法通常会自动将 `Loglevel` 提升至 `INFO` (如果当前更低)。

*   **`Auto.autodef(target, from=基本常识, ...)`**:
    *   作用: 自动定义 `target` (通常是一个概念或类名)。`Runtime` 会根据 `from` 指定的知识来源（默认为常识）或其他参数，尝试创建对象的结构、属性和方法。
    *   关键字: `autodef`
*   **`Auto.autofill(target, from=基本常识, ...)`**:
    *   作用: 自动填充 `target` 对象的内容。`Runtime` 会从 `from` (通常是描述性文本) 中提取信息并填充到 `target` 的属性中。
    *   关键字: `autofill`
*   **`Auto.autolet(cond, target=auto, from=基本常识, 原则=最小破坏性, ...)`**:
    *   作用: 自动约束。调整 `target` 对象的可控部分，使得布尔条件 `cond` 为真。`Runtime` 会根据指定的 `原则` (如最小破坏性) 选择调整策略。
    *   关键字: `autolet`
*   **`Auto.auto(from=基本常识, ...)`**:
    *   作用: 全自动模式。让 `Runtime` 根据上下文和 `from` 信息，自动猜测用户意图并执行相应操作。猜测和执行过程会记录在日志中。
    *   关键字: `auto`
