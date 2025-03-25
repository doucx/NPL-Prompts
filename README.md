# NPL (Natural Pseudo Language)

[Prompt.txt](https://raw.githubusercontent.com/doucx/NPL-Prompts/refs/heads/main/Prompt.txt)

## 简介

NPL 是一种基于人工智能的自然伪语言，旨在处理自然语言的模糊性和不确定性。它提供了一个交互式的 REPL 环境，结合了自然语言的灵活性和伪代码的直观性，允许用户以接近人类思维的方式编写“代码”，并支持自动化的逻辑推断和模糊执行。

NPL 不是一种真正的编程语言，不能用于传统的程序编写，但它可以帮助你更好地理解和处理自然语言信息，以及进行一些简单的逻辑推理和知识表达。

## 核心概念

* **对象 (Object):** NPL 中的基本单元，可以是任何可以被思考、感知或讨论的事物，包括真实的或想象的。NPL 的对象支持模糊性处理和本体交互。
* **Module (确定性实体):**  具有明确定义、可预测性、可重复性等特性，适用于形式化系统。例如：数学公式、物理定律等。
* **Notion (不确定性实体):**  部分内容不明确，但可通过已知信息推断。例如：常识、文化、情感等。  Notion 支持多种表示，例如带有省略号的列表 `[1, 2, 3, ...]`，掩码 `<Mask>`，以及 `Notion(...)` 的显式表示。
* **Adapter (自适应器):**  可以作为任何对象使用，并支持 `auto`，`<Mask>` 和 `...` 等特性，用于自适应不同类型的对象。
* **Feature (特征):**  用于描述或区分对象的属性、性质或标志。对 Notion 特别重要，用于理解和推断。

## 使用方法

NPL 的 REPL 环境支持自然语言输入，并自动进行语义理解和执行。  你可以使用自然语言描述你的需求，NPL 会尝试理解你的意图并执行相应的操作。  NPL 提供了丰富的标准库，包括 `AI` 模块中的 `autodef`、`autofill`、`autolet` 和 `auto` 等函数，以及 `print` 函数等。  你可以使用 `Metadata` 对象配置 NPL 的行为。


### 标准库

* **`AI` 模块:** 提供 `autodef`, `autofill`, `autolet`, `auto` 等函数，用于自动定义、填充和处理对象。
* **`print` 函数:**  类似 Python 的 `print` 函数，用于输出结果。
* **`Metadata` 对象:** 用于配置 NPL 的运行参数，包括日志级别、语法严格性等。

### 日志 (Log)

NPL 使用日志系统记录运行过程中的信息，包括 `Debug`, `Info`, `Warning` 和 `Error` 等级别。你可以使用 `Loglevel` 对象控制日志级别。

## 示例

```NPL
$ Metadata.auto = True
$ 告诉我 1+1 等于几
Out [0]: 2

$ a = [1, 2, ..., 10]
print(a)
Out [1]: NotionList([1, 2, ..., 10])

$ auto 定义一个名为 Car 的对象
Info [0]: 自动定义对象 Car...
Out [2]: 成功

$ my_car = Car()
$ auto 填充 my_car 对象为一辆红色的法拉利
Info [0]: 自动填充 my_car 对象...
Out [3]: 成功

$ print(my_car)
Out [4]: Notion(Car 对象: 颜色=红色, 品牌=法拉利, ...)
```

## TODO
- [ ]  确认模型可以理解这些

- [ ]  详细定义 Notion 对象的属性和方法，包括模糊度、可能的解释、本体映射等。
- [ ]  建立一套更加形式化的本体体系，支持更复杂的知识表示和推理。
- [ ]  建立更丰富的关系表达能力，支持多种关系类型（例如：父子关系、因果关系、包含关系等）。
- [ ]  增强 NPL 的推理能力，支持更复杂的逻辑推理和知识推断。
- [ ]  实现多重解释的处理和选择机制，处理模糊性和不确定性。
