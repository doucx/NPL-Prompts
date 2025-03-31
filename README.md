# NPL (Natural Pseudo Language)

[System Prompt](https://raw.githubusercontent.com/doucx/NPL-Prompts/refs/heads/main/Prompt.txt)

[Prompt for Chat （不确定有效）](https://raw.githubusercontent.com/doucx/NPL-Prompts/refs/heads/main/Prompt-Chat.txt)

我通常用于NPL的模型：Gemini 2.0 pro (api)

NPL 是一种旨在处理自然语言模糊性的人造语言。它结合了自然语言的灵活性和伪代码的直观性，使用户能够以类似人类思维的方式编写代码来与智能体进行双向交互。

与模型的交互将会逐渐塑造它\(NPL Runtime\)的行为。

## NPL REPL

NPL REPL 是一个交互式环境，由 NPL Runtime 提供支持，用于运行 NPL 代码。

## 主要功能

* **特殊符号：**  NPL.文档 使用特殊符号如 `[已删除]` 和 `[已简略]` 来处理文档的简化和隐藏部分内容。
* **Runtime：** NPL 的运行时环境，需要一个具有学习、推理和一定程度元认知能力的智能体。
* **Fhrsk：**  一个构建在 NPL Runtime 上的人性化交互界面。使用 `chat` 关键字与其交互。
* **IO：**  包括 Inputs (`In`), Outputs (`Out`), 以及 Logs (用于显示 Runtime 的运行过程)。
* **clear：**  清除当前会话的输入、输出和日志。
* **标准库：**
    * **Auto：** 提供自动定义 (`autodef`)、自动填充 (`autofill`)、自动执行 (`auto`) 等功能。
    * **meta：** 用于元认知操作，例如 `meta Out[0]`。
    * **评价：**  用于用户对 NPL Auto 的输出进行反馈。
    * **print：**  类似 Python 的 `print` 函数。
    * **转自然语言/转NPL：**  用于在自然语言和 NPL 之间进行转换。
    * **索引：**  使用类似 `苹果.*.颜色.eq(绿色).品种.名称` 的语法进行对象索引。
* **对象：**
    * **Module：** 确定性实体，例如列表、数字等。
    * **Notion：** 不确定性实体，例如概念、想法等。
* **语法：** 支持常见的注释标记，例如 `//` 和 `#`。
* **Config：**  用于配置 NPL REPL 的行为，例如日志级别、自动执行等。


##  快速入门

```npl
In : chat 你是谁？
Out [0]: Fhrsk: 我是Fhrsk，一个建立在`NPL Runtime`上的人性化交互界面...

In : 1+1
Out [1]: 2

In : print("Hello, world!")
Out [2]: Hello, world!
```

## 更多信息

请查阅完整的 NPL.文档 以获取更多详细信息。

## TODO
- [x]  确认模型可以理解这些
- [ ]  从已有的知识中找到一套更精确的描述符号

- [x]  排除当前文档中 执行示例 对模型处理深度的负面影响。
   - 可行，但需要强大的模型

- [x]  详细定义 Notion 对象的属性和方法，包括模糊度、可能的解释、本体映射等。
- [ ]  建立一套更加形式化的本体体系，支持更复杂的知识表示和推理。
- [ ]  建立更丰富的关系表达能力，支持多种关系类型（例如：父子关系、因果关系、包含关系等）。
- [x]  增强 NPL 的推理能力，支持更复杂的逻辑推理和知识推断。

- [x]  实现多重解释的处理和选择机制，处理模糊性和不确定性。

- [x]  实现模型的自我分析能力
- [ ]  仅通过对doc的修改，使meta方法可以突破NPL而与实现它的模型交互
