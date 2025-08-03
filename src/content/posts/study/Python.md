---
title: Python的学习笔记
published: 2025-08-03
description: "Python的学习笔记，记录了我在学习Python过程中遇到的问题和解决方案。"
image: "./cover.jpg"
tags: ["Python"]
category: 学习笔记
draft: false
---


# Python

## 简介

1989年，为了打发圣诞节假期，Guido van Rossum吉多·范罗苏姆（龟叔）是一名来自荷兰的计算机程序员决心开发一个新的解释程序（Python雏形）

1991年，第一个Python解释器诞生，它是用C语言实现的，并能够调用C语言的库文件

Python（蟒蛇）这个名字，来自龟叔所挚爱的电视剧蒙提·派森的飞行马戏团(Monty Python's Flying Circus)，在Python社区，吉多·范罗苏姆被人们认为是"仁慈的独裁者（BDFL）"，意思是他仍然关注Python的开发进程，并在必要的时刻做出决定。

Python的**官方实现（CPython）** 主要是用 **C 语言** 开发的，同时也包含了一些Python自身：

1. **核心解释器**：
    - 用 C 语言编写（约 60% 代码）
    - 负责字节码编译、执行、内存管理、对象系统等核心功能
2. **标准库**：
    - 大部分用 Python 编写（约 36%）
    - 部分性能关键模块用 C 编写（如 `_json`、`_pickle`）
3. **构建系统**：
    - 用 Python 和 Shell 脚本编写
    - 包含自动化构建和测试工具
4. **文档和工具**：
    - 用 reStructuredText（文档）
    - 用 Python（各种开发工具）

官方源码：[github.com/python/cpython](https://github.com/python/cpython)

开发者指南：[devguide.python.org](https://devguide.python.org/)

```
cpython/
├── Doc/           # 官方文档 (reStructuredText 格式)
├── Grammar/       # Python 语法定义 (PEG 格式)
├── Include/       # C 头文件 (.h)
│   ├── object.h   # 所有Python对象的基类
│   ├── pyport.h   # 跨平台兼容定义
│   └── ...
├── Lib/           # 标准库源码 (.py 文件)
│   ├── os.py      # 操作系统接口
│   ├── re.py      # 正则表达式模块
│   └── ...
├── Modules/       # C 扩展模块
│   ├── _math.c    # 数学模块
│   ├── _io/       # I/O 系统
│   └── ...
├── Objects/       # 核心对象实现
│   ├── listobject.c  # 列表实现
│   ├── dictobject.c  # 字典实现
│   └── ...
├── Parser/        # 语法解析器
│   ├── parser.c   # 语法分析器
│   └── ...
├── Programs/      # 可执行文件入口
│   └── python.c   # main() 函数入口
├── Python/        # 解释器核心
│   ├── ceval.c    # 字节码执行引擎
│   ├── compile.c  # 代码编译
│   └── ...
└── Tools/         # 开发工具
    ├── gdb/       # GDB 调试工具
    └── ...
```

**为什么用C语言开发Python？**

1. **性能**：C语言可直接操作硬件，执行效率高
2. **可移植性**：C语言编译器支持几乎所有平台
3. **扩展性**：易于创建C语言扩展模块
4. **成熟度**：C语言有成熟的开发工具链
5. **历史原因**：Guido van Rossum 最初选择 C语言



## Python的设计目标

1999年，吉多·范罗苏姆向DARPA提交了一条名为"Computer Programming for Everybody"的资金申请，并在后来说明了他对Python的目标：

- 一门简单直观的语言并与主要竞争者一样强大
- 开源，以便任何人都可以为它做贡献
- 代码像纯英语那样容易理解
- 适用于短期开发的日常任务

这些想法中的基本都已经成为现实，Python已经成为一门流行的编程语言

## Python的设计哲学

1.优雅

2.明确

3.简单

- Python开发者的哲学是：用一种方法，最好是只有一种方法来做一件事
- 如果面临多种选择，Python开发者一般会拒绝花俏的语法，而选择明确没有或者很少有歧义的语法

## 为什么选择Python?

代码量少，同一样问题，用不同的语言解决，代码量差距还是很多的，一般情况下Python是Java的1/5，所以说人生苦短，我用Python。

## Python的特点

- Python是完全面向对象的语言
- 函数、模块、数字、字符串都是对象，在Python中一切皆对象
- 完全支持继承、重载、多重继承
- 支持重载运算符，也支持泛型设计
- Python拥有一个强大的标准库，Python语言的核心只包含数字、字符串、列表、字典、文件等常见类型和函数，而由Python标准库提供了系统管理、网络通信、文本处理、数据库接口、图形系统、XML处理等额外的功能
- Python社区提供了大量的第三方模块，使用方式与标准库类似。它们的功能覆盖科学计算、人工智能、机器学习、Web开发、数据库接口、图形系统多个领域

面向对象的思维方式

- 面向对象是一种思维方式，也是一门程序设计技术
- 要解决一个问题前，首先考虑由谁来做，怎么做事情是谁的职责，最后把事情做好就行！对象就是谁。
- 要解决复杂的问题，就可以找多个不同的对象，各司其职，共同实现，最终完成需求

## 什么是Pythonic？

在Python社区里，有一个常被提及的词"Pythonic"。如果你是一名Python程序员，或多或少都会听到这个词，但它究竟是什么意思呢？

## Pythonic的含义

Pythonic（"Python风格"或"符合Python习惯"）指的是以符合Python语言哲学的方式编写代码，使其更简洁、可读、优雅且高效。简单来说，Pythonic代码是符合 Python 语言设计思想的代码。

## Pythonic的哲学基础

要理解Pythonic，我们可以先看看Python语言的核心哲学《Python之禅》（The Zen of Python）。在Python解释器中输入 `import this`，你会看到几条富有哲理的编程建议，例如：

- **优美胜于丑陋（Beautiful is better than ugly.）**
- **明了胜于晦涩（Explicit is better than implicit.）**
- **简单胜于复杂（Simple is better than complex.）**
- **复杂胜于凌乱（Complex is better than complicated.）**
- **可读性很重要（Readability counts.）**

```
C:\Users\mmg>python
Python 3.10.10 (tags/v3.10.10:aad5f6a, Feb  7 2023, 17:20:36) [MSC v.1929 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import this
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!


翻译：
《Python之禅》，作者：Tim Peters
优美比丑陋好。
显式比隐式好。
简单比复杂好。
复杂比错综复杂好。
扁平比嵌套好。
稀疏胜于稠密。
可读性很重要。
特殊情况也不应该违反这些规则。
但现实往往并不那么完美。
异常不应该被静默处理。
除非你希望如此。
遇到模棱两可的地方，不要胡乱猜测。
肯定有一种通常也是唯一一种最佳的解决方案。
虽然这种方案并不是显而易见的，因为你不是那个荷兰人[这里指的是Python之父Guido]。
现在开始做比不做好。
不做比盲目去做好[极限编程中的YAGNI原则]。
如果一个实现方案难于理解，它就不是一个好的方案。
如果一个实现方案易于理解，它很有可能是一个好的方案。
命名空间非常有用，我们应当多加利用!
```

## 什么代码是Pythonic？

- 遵循 Python之禅：代码应优雅、清晰、简洁，Pythonic 代码应尽量优雅直观，而不是冗长复杂。
- 充分利用Python提供的特性：Python提供了许多实用的内置函数，如 `zip()`、`enumerate()`、生成器等。
- 使用标准库，避免重复造轮子：Python提供了强大的标准库，例如 `collections`、`itertools` 等，可以避免编写冗余代码。
- 写可读性高的代码：清晰的变量命名

# 初始

## 安装

官方下载链接：https://www.python.org/downloads/

阿里云下载链接：https://mirrors.aliyun.com/python-release/

## 第一个Python程序

向世界说你好，应该是全世界，所有程序员入门编程语言时，都会选择的第一个程序。让我们也延续这一份来自程序员之间的浪漫，学习如何使用Python，向世界说你好。

```python
print("Hello World!")
```



## Python的解释器

Python解释器，是一个计算机程序，用来翻译Python代码，并提交给计算机执行。

所以，它的功能很简单，就2点：

1. 翻译代码
2. 提交给计算机运行

Python的解释器位于Python安装目录下的python.exe可执行文件。

我们可以将代码，写入一个以".py"结尾的文件中，使用python命令去运行它。
如，在windows系统的D盘，我们新建一个名为：test.py的文件，并通过记事本程序打开它，输入如下内容：

```python
print("Hello World!")
print("我是木芒果!")
```

使用命令运行test.py

```shell
python D:/test.py
```

Python 有多种解释器实现，每种解释器有不同的设计目标和适用场景。以下是主要的 Python 解释器及其特点：

**1. CPython（官方标准解释器）**

- **实现方式**：C 语言编写
- **特点**：
    - Python 的**参考实现**，最广泛使用。
    - 包含全局解释器锁（**GIL**），限制多线程并行。
    - 支持大多数 Python 库和框架。
- **适用场景**：通用 Python 开发，兼容性要求高的项目。
- **官网**：https://www.python.org/

**2. PyPy（高性能 JIT 解释器）**

- **实现方式**：Python 的子集（RPython）编写，带即时编译（JIT）
- **特点**：
    - 比 CPython **更快**（尤其对长时间运行的代码）。
    - 兼容 CPython，但部分 C 扩展可能性能较差。
    - 默认有 GIL，但支持 **STM（软件事务内存）** 实验性移除 GIL。
- **适用场景**：需要高性能的纯 Python 代码（如科学计算、脚本）。
- **官网**：https://www.pypy.org/

**3. Jython（Java 平台集成）**

- **实现方式**：Java 编写
- **特点**：
    - 运行在 **JVM** 上，可直接调用 Java 类库。
    - **无 GIL**，支持真正的多线程。
    - 不支持 CPython 的 C 扩展（如 NumPy）。
- **适用场景**：Java/Python 混合开发，如企业级应用。
- **官网**：http://www.jython.org/

**4. IronPython（.NET 平台集成）**

- **实现方式**：C# 编写
- **特点**：
    - 运行在 **.NET CLR** 上，可调用 .NET 库。
    - 无 GIL，支持多线程。
    - 兼容性低于 CPython（部分库不兼容）。
- **适用场景**：.NET 生态集成（如 Windows 应用）。
- **官网**：http://ironpython.net/

**5. MicroPython（嵌入式优化）**

- **实现方式**：C 编写，高度精简
- **特点**：
    - 专为 **微控制器（MCU）** 设计（如 ESP32、Raspberry Pi Pico）。
    - 支持硬件直接操作（GPIO、I2C 等）。
    - 语法与 CPython 略有差异，标准库精简。
- **适用场景**：物联网（IoT）、嵌入式开发。
- **官网**：https://micropython.org/

**6. Stackless Python（增强并发）**

- **实现方式**：CPython 修改版
- **特点**：
    - 提供 **微线程（tasklets）**，支持高并发（无 GIL 限制）。
    - 被用于游戏引擎（如 EVE Online）。
    - 非官方维护，逐渐被 `asyncio` 替代。
- **适用场景**：高并发、协程密集型应用。
- **官网**：https://github.com/stackless-dev/stackless

**7. Cython（静态编译扩展）**

- **严格来说不是解释器**，而是将 Python 代码编译为 C 的扩展工具。
- **特点**：
    - 允许混合 Python 和 C 语法，提升性能。
    - 常用于加速数值计算（如 Pandas、SciPy 的底层）。
- **官网**：https://cython.org/



## IPython

IPython(全称: Interactive Python)是一个增强型的 Python 交互式解释器，旨在提供更强大的交互式编程体验。它基于 CPython（Python 的标准实现），但扩展了许多功能，特别适合数据科学、科学计算和交互式开发

**IPython 的核心功能**

| 特性               | 说明                                                         |
| :----------------- | :----------------------------------------------------------- |
| **代码补全**       | 按 `Tab` 自动补全变量、函数、模块名（比标准 Python Shell 更智能）。 |
| **内联文档**       | 使用 `?` 或 `??` 快速查看函数/对象的文档（如 `np.array?`）。 |
| **魔法命令**       | 以 `%` 开头的特殊命令（如 `%timeit` 测性能，`%run` 执行脚本）。 |
| **Shell 交互**     | 直接执行系统命令（如 `!ls` 列出当前目录文件）。              |
| **多行编辑**       | 支持粘贴多行代码块并执行，避免标准 REPL 的逐行限制。         |
| **历史记录**       | 保存输入历史，支持 `_`、`__` 访问上一次输出结果。            |
| **内核与 Jupyter** | 作为 Jupyter Notebook 的后端内核，支持交互式笔记本。         |

IPython 不是独立的 Python 解释器实现，而是基于 CPython（或其他 Python 解释器，如 PyPy）的交互式前端。它增强了用户界面和交互功能，但底层仍依赖 CPython 的执行环境。

IPython 是一个功能强大的交互式 Python 解释器，扩展了标准 Python REPL 的功能，提供魔法命令、自动补全、系统命令集成等特性。它是数据科学和交互式开发的首选工具，尤其通过 Jupyter Notebook 广泛应用于科学计算和教学。

**安装与启动**

```shell
# 安装
pip install ipython

# 启动
ipython  # 普通模式
ipython --no-banner  # 隐藏启动信息
```



## Python开发环境

Python程序的开发有许多种方式，一般我们常见的有：

- Python解释器环境内，执行单行代码
- 使用Python解释器程序，执行Python代码文件
- 使用第三方IDE（集成开发工具），如PyCharm软件，开发Python程序

PyCharm集成开发工具（IDE），是当下全球Python开发者，使用最频繁的工具软件。

绝大多数的Python程序，都是在PyCharm工具内完成的开发。

首先，我们先下载并安装它：

下载链接：https://www.jetbrains.com/pycharm/download/#section=windows



# 基础语法

## 字面量

什么是字面量

字面量：在代码中，被写下来的的固定的值，称之为字面量

Python中常用的有6种值（数据）的类型

| 类型               | 描述                                                  | 说明                                                         |
| ------------------ | ----------------------------------------------------- | ------------------------------------------------------------ |
| 数字（Number）     | 整数（int）浮点数（float）复数（complex）布尔（bool） | 整数（int），如10，-10，浮点数（float），如：13.14、-13.14，复数（complex），如4+3j，以j结尾表示复数，布尔（bool）表达现实生活中的逻辑，即真和假，True表示真，Flase表示假。True本质上是一个数字记作1，False记作0。 |
| 字符串（String）   | 描述文本的一种数据类型                                | 字符串（string）由任意数量的字符组成                         |
| 列表（List）       | 有序的可变序列                                        | Python中使用最频繁的数据类型，可有序记录一堆数据             |
| 元组（Tunple）     | 有序的不可变序列                                      | 可有序记录一堆不可变的Python数据集合                         |
| 集合（Set）        | 无序不重复集合                                        | 可无序记录一堆不重复的Python数据集合                         |
| 字典（Dictionary） | 无序Key-Value集合                                     | 可无序记录一堆Key-Value的Python数据集合                      |

字符串（string），又称文本，是由任意数量的字符如中文、英文、各类符号、数字等组成。所以叫做字符的串

如：

- "木芒果"
- "MUMANGGUO木芒果"
- "!@#$%^&"
- "木芒果的Gitee是：https://gitee.com/mumangguo"

Python中，字符串需要用双引号（""）包围起来，被引号包围起来的，都是字符串。

最常用的数据类型：

| 类型           | 程序中的写法 | 说明                             |
| -------------- | ------------ | -------------------------------- |
| 整数           | 666，-88     | 和现实中的写法一致               |
| 浮点数（小数） | 13.14，-5.21 | 和现实中的写法一致               |
| 字符串（文本） | "木芒果"     | 程序中需要加上双引号来表示字符串 |

```python
666
13.14
"木芒果"

print(666)
print(13.14)
print("木芒果")
```



## 注释

注释：在程序代码中对程序代码进行解释说明的文字。例如：物品的使用说明书

作用：注释不是程序，不能被执行，只是对程序代码进行解释说明，让别人可以看懂程序代码的作用，大大增强程序的可读性。

注释的分类：

单行注释：以"#"开头，#右边的所有文字当作说明，而不是真正要执行的程序，起辅助说明作用

```python
# 我是单行注释，注意：#和注释内容一般建议以一个空格隔开
print("Hello World")
```

多行注释：以一对三个双引号引起来(""注释内容"")来解释说明一段代码的作用使用方法

```python
"""
 我是多行注释
 诗名：悯农
 作者：李绅
"""
print("锄禾日当午")
print("汗滴禾下土")
print("谁知盘中餐")
print("粒粒皆辛苦")
```



## 变量

什么是变量？

变量：在程序运行时，能储存计算结果或能表示值的抽象概念。简单的说，变量就是在程序运行时，记录数据用的。

变量的定义格式：变量名称=变量的值

每一个变量都有自己的名称，称之为：变量名，也就是变量本身，并且变量的值是可以动态改变的。

```python
"""
 演示Python中变量的相关操作
"""

# 定义一个变量，用来记录钱包余额
wallet = 1000

# 通过print输出变量的值
print("钱包余额为：", wallet)

# 买了一部手机，花了500元
wallet = wallet - 500

# 通过print输出变量的值
print("买了一部手机，还了500，钱包余额为：", wallet, "元")


"""
  小练习：求钱包余额
"""
money = 50
print("当前钱包余额：", money, "元")
# 冰淇淋10元
ice_cream = 10
money = money - ice_cream
print("购买了冰淇淋，花费：", ice_cream, "元")
# 可乐5元
coke = 5
money = money - coke
print("购买了可乐，花费：", coke, "元")

# 通过print输出变量的值
print("最终，钱包剩余：", money, "元")
```



## 数据类型

变量无类型而数据有类型。

我们可以通过type语句来得到数据的类型：

语法：type(被查看类型的数据）

```python
# 直接通过print打印数据类型
print(type("木芒果")) # 字符串
print(type(666)) # 整数
print(type(13.14)) # 浮点数

# 使用变量存储type的结果
name = "木芒果"
name_type = type(name)
age = 22
age_type = type(age)
money = 1314.14
money_type = type(money)

print(name_type)
print(age_type)
print(money_type)
```



## 数据类型转换

数据类型之间，在特定的场景下，是可以相互转换的，如字符串转数字、数字转字符串等

数据类型转换，将会是我们以后经常使用的功能。如:

- 从文件中读取的数字，默认是字符串，我们需要转换成数字类型
- input()输入语句，默认结果是字符串，若需要数字也需要转换
- 将数字转换成字符串用以写出到外部系统

常见的转换语句

| 语句（函数） | 说明                |
| ------------ | ------------------- |
| int(x)       | 将x转换为一个整数   |
| float(x)     | 将x转换为一个浮点数 |
| str(x)       | 将x转换为字符串     |

同type()语句一样，这三个语句，都是带有结果的（返回值）我们可以用print直接输出，或者使用变量存储结果值。

```python
# 将数字类型转换为字符串类型
number = str(11)
print(type(number), number)

float_str = str(11.11)
print(type(float_str), float_str)

# 将字符串类型转换为数字类型
number2 = int("11")
print(type(number2), number2)

float_str2 = float("11.11")
print(type(float_str2), float_str2)

# 将整数转换为浮点数
number3 = float(11)
print(type(number3), number3)

# 将浮点数转换为整数,小数部分会被舍弃,并不会四舍五入
number4 = int(11.89)
print(type(number4), number4)
```



## 标识符

在Python程序中，我们可以给很多东西起名字，比如：

- 变量的名字
- 方法的名字
- 类的名字

这些名字，我们把它统一的称之为标识符，用来做内容的标识。

标识符是用户在编程的时候所使用的一系列名字，用于给变量、类、方法等命名。

Python中，标识符命名的规则主要有3类：

- 内容限定
- 大小写敏感
- 不可使用关键字

标识符命名中，只允许出现：英文、中文、数字、下划线（_），其余任何内容都不被允许。不推荐使用除英文以外对标识符进行命令，数字不可以在标识符的开头。

以定义变量为例：

- Andy=“安迪1”
- andy=“安迪2”

字母a的大写和小写，是完全能够区分的。

Python中有一系列单词，称之为关键字，关键字在Python中都有特定用途，我们不可以使用它们作为标识符。

```python
False、True、None、break、class、assert、and、as、finally、for、else、def、del、elif、except、from、continue、if、in、lambda、nonlocal、import、global、is、raise、while、with、yield、try、not、or、pass、return
```

```python
# 规则1：内容限定，限定只能使用：中文、英文、数字、下划线，注意：不能以数字开头
# 1_name = "张三" # 错误
# name_! = "张三"  # 错误

name_ = "张三"  # 正确
_name = "张三"  # 正确
name_1 = "张三"  # 正确

# 规则2：大小写敏感
Mumangguo = "木芒果1"
mumangguo = "木芒果2"
print(Mumangguo)
print(mumangguo)

# 规则3：不可使用关键字
# class = "张三"  # 错误
# def = "张三"  # 错误

Class = "张三"  # 正确
Def = "张三"  # 正确
```

标识符的命名规范。

- 变量名
- 类名
- 方法名

不同的标识符，有不同的规范。

变量的命名规范：

- 见名知意，明了：尽量做到，看到名字，就知道是什么意思；简洁：尽量在确保“明了”的前提下，减少名字的长度
- 下划线命名法，多个单词组合变量名，要使用下划线做分隔
- 英文字母全小写



## 运算符

算数（数学）运算符

| 运算符 | 描述   | 实例                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| +      | 加     | 两个对象相加a + b输出结果 30                                 |
| -      | 减     | 得到负数或是一个数减去另一个输a - b输出结果 -10              |
| *      | 乘     | 两个数相乘或是返回一个被重复若干次的字符串a * b 输出结果 200 |
| /      | 除     | b/a 输出结果2                                                |
| //     | 取整除 | 返回尚的整数部分 9//2 输出结果4，9.0//2.0输出结果4.0         |
| %      | 取余   | 返回除法的余数b % a输出结果0                                 |
| **     | 指数   | a**b 为10的20次方，输出结果是10000 0000 0000 0000 00000      |

赋值运算符

| 运算符 | 描述       | 实例                                                         |
| ------ | ---------- | ------------------------------------------------------------ |
| =      | 赋值运算符 | 把=号右边的结果赋给左边的变量，如num = 1+2*3，结果num的值为7 |

复合赋值运算符

| 运算符 | 描述           | 实例                     |
| ------ | -------------- | ------------------------ |
| +=     | 加法赋值运算符 | c += a等效于c = c + a    |
| -=     | 减法赋值运算符 | c -= a等效于c = c - a    |
| *=     | 乘法赋值运算符 | c *= a等效于c = c * a    |
| /=     | 除法赋值运算符 | c /= a等效于c = c / a    |
| %=     | 取模赋值运算符 | c %= a等效于c = c % a    |
| **=    | 幂赋值运算符   | c ** = a等效于c = c ** a |
| //=    | 整除赋值运算符 | c //= a等效于c = c // a  |

```python
"""
    演示Python中的各类运算符
"""

# 算术（数学）运算符
print("1+1=", 1 + 1)  # 加法
print("2-1=", 2 - 1)  # 减法
print("3*3=", 3 * 3)  # 乘法
print("4/2=", 4 / 2)  # 除法
print("11//2=", 11 // 2)  # 整除
print("9%2=", 9 % 2)  # 取余
print("2**2=", 2 ** 2)  # 乘方


# 赋值运算符
num = 1+2*3
print("num=", num)  # 赋值

num += 1  # num = num + 1
print("num=", num)  # 加法赋值

num -= 1  # num = num - 1
print("num=", num)  # 减法赋值

num *= 2  # num = num * 2
print("num=", num)  # 乘法赋值

num /= 2  # num = num / 2
print("num=", num)  # 除法赋值

num //= 2  # num = num // 2
print("num=", num)  # 整除赋值

num %= 2  # num = num % 2
print("num=", num)  # 取余赋值

num **= 2  # num = num ** 2
print("num=", num)  # 乘方赋值
```



## 字符串

### 三种定义方式

单引号定义法：

```python
name = '木芒果'
```

双引号定义法：

```python
name = "木芒果"
```

三引号定义法：

```python
name = """木芒果"""
```

三引号定义法，和多行注释的写法一样，同样支持换行操作。

使用变量接收它，它就是字符串

不使用变量接收它，就可以作为多行注释使用。

```python
"""
    演示字符串的三种定义方式：
    单引号定义法
    双引号定义法
    三引号定义法
"""

name = '木芒果'

name2 = "木芒果"

name3 = """
        木芒果1
        木芒果2
        木芒果3
        """

print(type(name),name)
print(type(name2),name2)
print(type(name3),name3)


# 字符串内 包含双引号
name4 = '"木芒果"'
print(name4)

# 字符串内 包含单引号
name5 = "'木芒果'"
print(name5)

# 使用转义字符\
name6 = "\"木芒果\""
print(name6)
name7 = '\'木芒果\''
print(name7)
```



### 拼接

如果我们有两个字符串（文本）字面量，可以将其拼接成一个字符串，通过+号即可完成，如：

```python
print("木芒果"+"你好")
```


字面量和变量或变量和变量之间会使用拼接，如：

```python
name = "木芒果"
print("我的名字是：" + name + "，我可以教大家IT技能")
```

```python
print("木芒果" + "你好")

name = "木芒果"
print("我的名字是：" + name + "，我可以教大家IT技能")

telephone = 123456789  # TypeError: can only concatenate str (not "int") to str,字符串无法和数字拼接
# print("我的名字是：" + name + "，我可以教大家IT技能，我的电话号码：" + telephone)
```



### 格式化

我们可以通过如下语法，完成字符串和变量的快速拼接。

```python
name="木芒果"
message ="我是 %s" % name
print(message)
```

%表示：我要占位
%s表示：将变量变成字符串放入占位的地方
所以，综合起来的意思就是：我先占个位置，等一会有个变量过来，我把它变成字符串放到占位的位置

```python
"""
    字符串格式化
"""

name = "木芒果"
age = 22
salary = 16781.12
message = "我是%s，我今年%s岁，工资:%s" % (name, age, salary) # 数字类型会自动转换为字符串然后拼接进去
print(message)

# 使用%s %d %f分别对应字符串、整数、浮点数类型进行格式化
message = "我是%s，我今年%d岁，工资:%f" % (name, age, salary)
print(message)
```

Python中，其实支持非常多的数据类型占位，最常用的为以下三种

| 格式符号 | 转化                             |
| -------- | -------------------------------- |
| %s       | 将内容转换成字符串，放入占位位置 |
| %d       | 将内容转换成整数，放入占位位置   |
| %f       | 将内容转换成浮点数，放入占位位置 |



### 数字精度控制

我们可以使用辅助符号"m.n"来控制数据的宽度和精度

- m，控制宽度，要求是数字（很少使用），设置的宽度小于数字自身，不生效
- .n，控制小数点精度，要求是数字，会进行小数的四舍五入

示例：

- %5d：表示将整数的宽度控制在5位，如数字11，被设置为5d，就会变成：【空格】【空格】11，用三个空格补足宽度。
- %5.2f：表示将宽度控制为5，将小数点精度设置为2小数点和小数部分也算入宽度计算。如，对11.345设置了%7.2f后，结果是：【空格】【空格】11.35。2个空格补足宽度，小数部分限制2位精度后，四舍五入为.35
- %.2f：表示不限制宽度，只设置小数点精度为2，如11.345设置%.2f后，结果是11.35

```python
num1 = 11
num2 = 11.345

print("数字11宽度限制5，结果:%5d" % num1)
print("数字11宽度限制1，结果:%1d" % num1)
print("数字11.345宽度限制7，小数精度2，结果：%7.2f" % num2)
print("数字11.345不限制宽度，小数精度2，结果：%.2f" % num2)
```



### 格式化第二种方式

通过语法：f"内容{变量}”的格式来快速格式化，这种方式不理会类型，不做精度控制，适合对精度没有要求的时候快速使用。

```python
"""
    字符串格式化第二种方式
"""

name = "木芒果"
age = 22
salary = 16781.12
message = f"我是{name}，我今年{age}岁，工资:{salary}"
print(message)
```



## 数据输入

input语句(函数)

print语句（函数），可以完成将内容（字面量、变量等）输出到屏幕上。

在Python中，与之对应的还有一个input语句，用来获取键盘输入。

- 数据输出：print
- 数据输入：input

使用上也非常简单：

- 使用input()语句可以从键盘获取输入
- 使用一个变量接收（存储）input语句获取的键盘输入数据即可

input()语句得到的数据都是字符串类型

```python
"""
    获取键盘的输入信息
"""

print("请输入你的姓名：")
name = input()
print("请输入你的年龄：")
age = input()
print("请输入你的工资：")
salary = input()

print("姓名的类型%s,年龄的类型%s,工资的类型%s" % (type(name), type(age), type(salary)))
print("你是%s, 今年%d岁，工资:%.2f" % (name, int(age), float(salary)))

name = input("请输入你的姓名：")
age = input("请输入你的年龄：")
salary = input("请输入你的工资：")
print("你是%s, 今年%d岁，工资:%.2f" % (name, int(age), float(salary)))
```



# 逻辑判断

## 布尔类型和比较运算符

在Python中，可以表示真假的数据类型是布尔（bool）表达现实生活中的逻辑，即真和假，True表示真，Flase表示假。True本质上是一个数字记作1，False记作0。

定义变量存储布尔类型数据：变量名称=布尔类型字面量

布尔类型的数据，不仅可以通过定义得到，也可以通过比较运算符进行内容比较得到。

| 比较运算符 | 描述                                                         | 示例                     |
| ---------- | ------------------------------------------------------------ | ------------------------ |
| ==         | 判断内容是否相等，满足为True，不满足为False                  | 如a=3,b=3,则(a==b)为True |
| !=         | 判断内容是否不相等，满足为True，不满足为False                | 如a=1,b=3,则(a!=b)为True |
| >          | 判断运算符左侧内容是否大于右侧。满足为True，不满足为False    | 如a=7,b=3,则(a>b)为True  |
| <          | 判断运算符左侧内容是否小于右侧。满足为True，不满足为False    | 如a=3,b=7,则(a<b)为True  |
| >=         | 判断运算符左侧内容是否大于等于右侧。满足为True，不满足为False | 如a=3,b=3,则(a>=b)为True |
| <=         | 判断运算符左侧内容是否小于等于右侧。满足为True，不满足为False | 如a=3,b=3,则(a<=b)为True |

```python
"""
    布尔类型和比较运算符
"""
# 定义布尔类型的数据
bool_true = True
bool_false = False
print(f"bool_true的值是{bool_true}，类型是{type(bool_true)}")
print(f"bool_false的值是{bool_false}，类型是{type(bool_false)}")

# 比较运算符 == != > < >= <=
result = 10 == 10
print(f"10 == 10的结果是{result}，类型是{type(result)}")

result = 10 != 5
print(f"10 != 5的结果是{result}，类型是{type(result)}")

result = 10 > 5
print(f"10 > 5的结果是{result}，类型是{type(result)}")

result = 10 < 11
print(f"10 < 11的结果是{result}，类型是{type(result)}")

result = 10 >= 10
print(f"10 >= 10的结果是{result}，类型是{type(result)}")

result = 10 <= 10
print(f"10 <= 10的结果是{result}，类型是{type(result)}")

name1 = "木芒果1"
name2 = "木芒果2"
result = name1 == name2
print(f"{name1} == {name2}的结果是{result}，类型是{type(result)}")
```



## if语句的基本格式

if语句是用来在程序进行逻辑判断的，在Python使用空格缩进来判断代码的归属，判断语句的结果，必须是布尔类型True或False，True会执行if内的代码语句，False则不会执行。

```python
if 要判断的条件:
    条件成立时，要做的事情

# 例如：
age = 20
if age >= 18:
    print(f"我成年了，我今年{age}")
print("这是在if外面的，无论条件是否成立都会执行！")


# 案例
if int(input("欢迎来到儿童游乐园，儿童免费，成人收费。请输入您的年龄：")) >= 18:
    print("您已成年，游玩需要补票10元")
print("祝您游玩愉快！")
```





## if else组合判断语句

if满足条件会执行相应的代码语句，如果不满足呢？有没有不满足的情况下，可供执行的代码呢？if else语句可以实现，else后，不需要判断条件，和if的代码块一样，else的代码块同样需要4个空格作为缩进

```python
if 条件:
    满足条件时要做的事情1
    满足条件时要做的事情2
    满足条件时要做的事情3
    ...
else:
    不满足条件时要做的事情1
    不满足条件时要做的事情2
    不满足条件时要做的事情3
    ...

# 动物园案例
"""
    if else语句的使用
"""

if int(input("欢迎来到儿童游乐园，儿童免费，成人收费。请输入您的年龄：")) >= 18:
    print("您已成年，游玩需要补票10元")
else:
    print("您未成年，可以免费游玩")
print("祝您游玩愉快！")
```



## if elif else组合多条件判断

某些场景下，判断条件不止一个，可能有多个。这种需求能用Python实现吗？可以使用elif语句进行多条件判断，从上到下进行判断，所有条件互斥，有一个条件成立，其他条件均不成立。

```python
if 条件1:
    条件1满足应做的事情
    条件1满足应做的事情
    ...
elif 条件2:
    条件2满足应做的事情
    条件2满足应做的事情
    ...
elif 条件N:
    条件N满足应做的事情
    条件N满足应做的事情
    ...
else:
    所有条件都不满足应做的事情
    所有条件都不满足应做的事情
    ...

# 动物园案例    
"""
    if elif else语句的使用
"""

print("欢迎来到动物园!")
height = int(input("请输入你的身高(cm): "))
vip_level = int(input("请输入你的vip级别(1~5): "))
day = int(input("请告诉我今天是几号: "))
if height < 120:
    print("您的身高小于120CM，可以免费游玩。")
elif vip_level > 3:
    print("您的vip级别大于3，可以免费游玩。")
elif day == 1:
    print("今天是1号，所有人免费游玩。")
else:
    print("不好意思，所有条件都不满足，需要购票10元。")
print("祝您游玩愉快。")
```



## 判断语句的嵌套

基础语法格式如下，第二个if，属于第一个if内，只有第一个if满足条件，才会执行第二个if，嵌套的关键点，在于：空格缩进，通过空格缩进，来决定语句之间的层次关系

```python
if 条件1:
    满足条件1做的事情1
    满足条件1做的事情2
    if 条件2:
        满足条件2做的事情1
        满足条件2做的事情2

# 动物园案例
"""
    判断语句的嵌套
"""

print("欢迎来到动物园。")
if int(input("输入你的身高：")) > 120:
    print("你的身高大于120cm，不可以免费")
    print("不过如果你的vip等级高于3，可以免费游玩")
    if int(input("请告诉我你的vip级别：")) > 3:
        print("恭喜你，你的vip级别大于3，可以免费游玩。")
    else:
        print("Sorry，你需要补票，10元。")
else:
    print("欢迎你小朋友，可以免费游玩。")  
```





# 循环语句

## while循环语句

while循环语句，只要条件满足会无限循环执行。

```python
while 条件：
    条件满足时，做的事情1
    条件满足时，做的事情2
    条件满足时，做的事情3
    ...

# 假如我要输出100次我爱你
print("我爱你")
print("我爱你")
print("我爱你")
...

# 使用while循环
i = 0
while i < 100:
    print("我爱你")
    i += 1

# 使用while循环完成1-100的和
i = 1
sum = 0
while i <= 100:
    sum += i
    i += 1
print(sum)

# 使用while循环完成猜数字游戏
import random
number = random.randint(1, 100)
guess = 0
sum = 0

while guess != number:
    guess = int(input("请输入你猜的数字(1-100)："))
    sum += 1
    if guess < number:
        print("你猜的数字小了")
    elif guess > number:
        print("你猜的数字大了")
    else:
        print("恭喜你，猜对了！")
print(f"你总共猜了{sum}次")
```

注意：

- while的条件需得到布尔类型，True表示继续循环，False表示结束循环
- 需要设置循环终止的条件，如i+=1配合i<100，就能确保100次后停止，否则将无限循环
- 空格缩进和if判断一样，都需要设置



## while循环嵌套

循环内套循环

```python
while 条件1:
    条件1满足时，做的事情1
    条件1满足时，做的事情2
    条件1满足时，做的事情3
    ...
    while 条件2:
        条件2满足时，做的事情1
        条件2满足时，做的事情2
        条件2满足时，做的事情3
        ...

# 表白一百天，每天送10支玫瑰花的案例
"""
    while循环嵌套
"""

i = 1
while i <= 100:
    print(f"今天是第{i}天，准备表白...")
    j = 1
    while j <= 10:
        print(f"送给小美第{j}只玫瑰花")
        j += 1
    print("小美，我喜欢你")
    i += 1
print(f"坚持到第{i - 1}天，表白成功")

# 九九乘法表
i = 1

while i <= 9:
    j = 1
    while j <= i:
        print(f"{j} * {i} = {j * i}", end="\t")
        j += 1
    print("")
    i += 1
```

注意：

- 同判断语句的嵌套一样，循环语句的嵌套，要注意空格缩进。（基于空格缩进来决定层次关系）
- 注意条件的设置，避免出现无限循环（除非真的需要无限循环）



## for循环语句

除了while循环语句外，Python同样提供了for循环语句。两者能完成的功能基本差不多，但仍有一些区别，while循环的循环条件是自定义的，自行控制循环条件，for循环是一种"轮询"机制，是对一批内容进行"逐个处理"

```python
for 临时变量 in 待处理数据集：
	循环满足条件时执行的代码

"""
    for循环的基础语法
"""
# 遍历字符串
name = "木芒果"
count = 0
for x in name:
    print(x)
    count += 1
print("字符串长度为：", count)
```

注意：

同while循环不同，for循环是无法定义循环条件的，只能从被处理的数据集中，依次取出内容进行处理。所以，理论上讲，Python的for循环无法构建无限循环（被处理的数据集不可能无限大）



## range语句

for循环语句，本质上是遍历：序列类型；通过range语句，获得一个简单的数字序列。

```python
# 语法1: 获取一个从0开始，到num结束的数字序列（不含num本身）如range(5)取得的数据是：[0,1,2,3,4]
range(num)

#语法2: 获得一个从num1开始，到num2结束的数字序列（不含num2本身）如range(5,10)取得的数据是：[5,6,7,8,9]
range(num1, num2)

#语法3: 获得一个从num1开始，到num2结束的数字序列（不含num2本身）数字之间的步长，以step为准（step默认为1）如range(5,10,2)取得的数据是：[5,7,9]
range(num1, num2, step)

"""
    range语句的使用
"""
number_list = range(10)
print(f"创建一个从0到9的数字列表：{number_list}")
for i in number_list:
    print(i, end=",")

print()

number_list2 = range(5, 10)
print(f"创建一个从5到9的数字列表：{number_list2}")
for i in number_list2:
    print(i, end=",")

print()

number_list3 = range(1, 10, 2)
print(f"创建一个从1到9的奇数列表：{number_list3}")
for i in number_list3:
    print(i, end=",")
```

注意：

- 语法1从0开始，到num结束（不含num本身）
- 语法2从num1开始，到num2结束（不含num2本身）
- 语法3从num1开始，到num2结束（不含num2本身）步长以step值为准



## for循环的变量作用域

```python
for 临时变量 in 待处理数据集：
	循环满足条件时执行的代码
    
    
"""
    for循环中的临时变量作用域
"""

for i in range(5):
    print(i)

print(f"在for循环外部访问临时变量i的值：{i}") # 会被警告
```

临时变量，在编程规范上，作用范围（作用域），只限定在for循环内部

如果在for循环外部访问临时变量：

- 实际上是可以访问到的
- 在编程规范上，是不允许、不建议这么做的
- 如果需要访问临时变量，可以将临时变量定义在前面，这样就可以将临时变量变为全局变量

```python
"""
    for循环中的临时变量作用域
"""
i = 0 # 定义全局变量i
for i in range(5):
    print(i)

print(f"在for循环外部访问临时变量i的值：{i}")
```



## for循环嵌套

```python
for 临时变量 in 待处理数据集（序列）:
    循环满足条件应做的事情1
    循环满足条件应做的事情2
    循环满足条件应做的事情N
    for 临时变量 in 待处理数据集（序列）:
        循环满足条件应做的事情1
        循环满足条件应做的事情2
        循环满足条件应做的事情N
        
"""
    for循环嵌套使用
"""

# 坚持表白100天，每天送10朵玫瑰花
i = 0  # 定义全局变量i
for i in range(1, 101):
    print(f"第{i}天表白，送10朵玫瑰花")
    for j in range(1, 11):
        print(f"第{i}天送第{j}朵玫瑰花")
    print("小美我喜欢你")
print(f"第{i}天表白成功，和小美在一起了！")

# 九九乘法表
for i in range(1, 10):
   for j in range(1, i + 1):
       print(f"{j} * {i} = {j * i}", end="\t")
   print()
```



## continue和break

思考：无论是while循环或是for循环，都是重复性的执行特定操作。

在这个重复的过程中，会出现一些其它情况让我们不得不：

- 暂时跳过某次循环，直接进行下一次
- 提前退出循环，不在继续

对于这种场景，Python提供continue和break关键字，用以对循环进行临时跳过和直接结束。

continue关键字用于：中断本次循环，直接进入下一次循环

continue可以用于：for循环和while循环，效果一致

```python
for i in range(1,100):
    语句1
    continue/break
    语句2
    
"""
    continue和break
"""

# continue语句的使用
for i in range(1, 10):
    print("语句1")
    continue
    print("语句2")  # 此代码无法到达

# continue在嵌套循环中的使用,作用范围只在当前循环内
for i in range(1, 10):
    print("语句1")
    for j in range(1, 10):
      print("语句2")
      continue
      print("语句3")
    print("语句4")
    
# break语句的使用
for i in range(1, 10):
    print("语句1")
    break # 跳出循环，用于直接退出当前循环
    print("语句2")  # 此代码无法到达
print("语句3")  # 此代码可以到达

# break在嵌套循环中的使用,作用范围只在当前循环内
for i in range(1, 10):
    print("语句1")
    for j in range(1, 10):
        print("语句2")
        break  # 跳出内层循环,用于直接退出当前循环
        print("语句3")  # 此代码无法到达
    print("语句4")  # 此代码可以到达
    

    
# 发工资案例
import random

salary = 10000  # 定义工资
for i in range(1, 21):
    score = random.randint(1, 10)
    if score < 5:
        print(f"员工{i}，绩效分数为{score}，绩效分数小于5不发工资")
        continue
    if salary >= 1000:
        print(f"员工{i}，绩效分数为{score}，发工资1000元")
        salary -= 1000
    else:
        print(f"员工{i}，工资余额不足，跳出循环")
        break
```

continue的作用是：

- 中断所在循环的当次执行，直接进入下一次

break的作用是：

- 直接结束所在的循环

注意事项：

- continue和break，在for和while循环中作用一致
- 在嵌套循环中，只能作用在所在的循环上，无法对上层循环起作用



## else语句

Python 循环中的 `else` 语句提供了一种优雅的方式来处理"循环正常完成"的情况。它：

- 与 `break` 语句配合使用
- 特别适合搜索和验证场景
- 能减少标志变量的使用
- 使代码更简洁、更Pythonic

while循环

```python
attempts = 3
correct_password = "secret123"

while attempts > 0:
    password = input(f"请输入密码（剩余尝试次数: {attempts}）: ")
    if password == correct_password:
        print("登录成功！")
        break
    attempts -= 1
else:
    print("尝试次数过多，账户已锁定！")

# 当三次输入错误密码时输出：尝试次数过多，账户已锁定！
```

for循环

```python
fruits = ["apple", "banana", "cherry"]
target = "mango"

for fruit in fruits:
    if fruit == target:
        print(f"找到 {target}!")
        break
    else:  # 这是if语句的else
         print(f"未找到 {target}!")
else:  # 这是for循环的else
    print(f"未找到 {target}!")
    
"""
	未找到 mango!
    未找到 mango!
    未找到 mango!
    未找到 mango!
"""

# 正确使用循环的else
fruits = ["apple", "banana", "cherry"]
target = "mango"

for fruit in fruits:
    if fruit == target:
        print(f"找到 {target}!")
        break
else:  # 只在循环完成且未break时执行一次
    print(f"未找到 {target}!")
```





## while循环和for循环的对比

while循环和for循环，都是循环语句，但细节不同：

在循环控制上：

- while循环可以自定循环条件 ，并自行控制
- for循环不可以自定循环条件，只可以一个个从容器内取出数据

在无限循环上：

- while循环可以通过条件控制做到无限循环
- for循环理论上不可以，因为被遍历的容器容量不是无限的

在使用场景上：

- while循环适用于任何想要循环的场景
- for循环适用于，遍历数据容器的场景或简单的固定次数循环场景

# 函数

## 初始

函数：是组织好的，可重复使用的，用来实现特定功能的代码段。

```python
"""
    快速函数的开发及应用
    需求：统计字符串的长度
"""
str1 = "mumangguo"
str2 = "zhangsan"
str3 = "lisi"

count = 0
for x in str1:
    count += 1
print(f"字符串{str1}的长度{count}")


count = 0
for x in str2:
    count += 1
print(f"字符串{str2}的长度{count}")


count = 0
for x in str3:
    count += 1
print(f"字符串{str3}的长度{count}")


# 使用函数，对以上代码进行优化,使用关键词def定义函数:def 函数名(参数1,参数2,参数...):
def my_len(data):
    count = 0
    for x in data:
        count += 1
    print(f"字符串{data}的长度{count}")

my_len(str1)
my_len(str2)
my_len(str3)
```

函数的好处：为了得到一个针对特定需求、可供重复利用的代码段提高程序的复用性，减少重复性代码，提高开发效率。



## 基础语法

```python
# 函数的定义
def 函数名(传入参数)
    函数体
    return 返回值

# 函数的调用：
函数名(参数)


"""
    函数的定义
    函数的使用步骤：
    1.先定义函数
    2.后调用函数
"""

# 定义一个函数，输出相关信息
def say_hi():
    print("Hi我是木芒果")

# 调用函数，让定义的函数开始工作
say_hi()
```

使用函数的注意事项：

- 参数如不需要，可以省略
- 返回值如不需要，可以省略
- 函数必须先定义后使用



## 函数的参数

函数的传入参数，传入参数的功能是：在函数进行计算的时候，接受外部（调用时）提供的数据

```python
# 基于函数的定义语法：
def 函数名(传入参数)：
    函数体
    return 返回值

"""
    函数的参数
"""


# 定义函数
def add(x, y):
    result = x + y
    print(f"{x}+{y}的结果是:{result}")


# 调用函数
add(1, 2)
add(3, 4)
add(5, 6)

# 案例：定义函数，接收1个形式参数，数字类型，表示体温
def check_tempture(tempture):
    print("请出示您的健康码以及72小时核酸证明，并配合测量体温！")
    if tempture <= 37.5:
        print(f"体温测量中，您的体温是：{tempture}度，体温正常请进！")
    else:
        print(f"体温测量中，您的体温是：{tempture}度，需要隔离！")

# 调用函数，传入实际参数
check_tempture(36.8)
check_tempture(37.8)
```

注意：

- 函数定义中的参数，称之为形式参数，以表示这个参数只是形式上存在的参数，当函数不被调用时这个参数就不存在，并不像普通变量一样存在于全局或者某个语句中
- 函数调用中的参数，称之为实际参数，以表示这个参数为实际调用函数的传入的参数
- 函数的参数数量不限，使用逗号分隔开
- 传入参数的时候，要和形式参数一一对应，逗号隔开



## 函数的返回值

"返回值"，就是程序中函数完成事情后，最后给调用者的结果，语法就是：通过return关键字，就能向调用者返回数据

```python
# 语法格式
def 函数名(参数...):
    函数体
    return 返回值
变量 = 函数名(参数)

"""
    函数的返回值
"""

"""
    定义两数相加的函数功能。完成功能后，会将相加的结果返回给函数调用者，所以，变量result_add接收到了函数的执行结果。
"""
def add(x, y):
    result = x + y
    # 通过返回值，将相加的结果返回给调用者
    return result
    # 在函数中，return后面的代码不会被执行
    print("这行代码不会被执行")

# 函数的返回值，可以通过变量去接收
result_add = add(1,2)
print(result_add)
```

注意：函数体在遇到return后就结束了，所以写在return后的代码不会执行。



## 返回值None类型

如果函数没有使用return语句返回数据，那么函数有返回值吗？

Python中有一个特殊的字面量：None，其类型是：<class'NoneType'>，无返回值的函数，实际上就是返回了：None这个字面量。

None表示：空的、无实际意义的意思，函数返回的None，就表示，这个函数没有返回什么有意义的内容。也就是返回了空的意思。

```python
"""
    函数的返回值None类型
"""

# 无return语句的函数
def say_hi():
    print("Hi我是木芒果")

# 调用函数
result = say_hi()
print(f"say_hi函数的返回值是：{result}", "类型是：", type(result))

# 有return语句的函数，返回值为None类型
def say_hi2():
    print("Hi我是木芒果")
    # 函数没有返回值，默认返回None,也可以主动地返回None
    return None

# 调用函数
result2 = say_hi2()
print(f"say_hi2函数的返回值是：{result2}", "类型是：", type(result2))
```

None作为一个特殊的字面量，用于表示：空、无意义，其有非常多的应用场景。

- 用在函数无返回值上
- 用在if判断上，在if判断中，None等同于False，一般用于在函数中主动返回None，配合if判断做相关处理
- 用于声明无内容的变量上，定义变量，但暂时不需要变量有具体值，可以用None来代替

```python
# None用于if判断
def check_age(age):
    if age > 18:
        return "SUCCESS"
    else:
        return None


result = check_age(16)
if not result:
    # 进入if表示result是None值也就是False
    print("未成年，不可以进入")

# None用于声明无初始内容的变量，相当于给变量一个初始值
name = None
```



## 函数的说明

函数是纯代码语言，想要理解其含义，就需要一行行的去阅读理解代码，效率比较低。

我们可以给函数添加说明，辅助理解函数的作用。通过多行注释的形式，对函数进行说明解释，内容应写在函数体之前。

```python
# 定义语法
def func(x, y):
    """
    函数说明
    :param x: b参数х的说明
    :param x: 参数у的说明
    :return: 返回值的说明
    """
	函数体
	return 返回值

# :param用于解释参数
# :return用于解释返回值



"""
    函数的说明
"""

# 定义函数，进行文档说明
def add(x, y):
    """
    add函数用于计算两个数的和

    :param x: 形式参数x表示第一个数
    :param y: 形式参数y表示第二个数
    :return: 返回两个数的和
    """
    result = x + y
    return result

print(add(11, 22))
```

函数的说明作用是对函数进行说明解释，帮助更好理解函数的功能



## 函数的嵌套调用

所谓函数嵌套调用指的是一个函数里面又调用了另外一个函数

```python
"""
    函数的嵌套调用
"""

# 定义函数func_b
def func_b():
    print("---2---")

# 定义函数func_a，并在内部调用func_b
def func_a():
    print("---1---")
    # 嵌套调用func_b
    func_b()
    print("---3---")

# 调用函数func_a
func_a()
```

如果函数A中，调用了另外一个函数B，那么先把函数B中的后才会回到上次函数A执行的位置



## 变量在函数中的作用域

变量作用域指的是变量的作用范围（变量在哪里可用，在哪里不可用）

主要分为两类：局部变量和全局变量

所谓局部变量是定义在函数体内部的变量，即只在函数体内部生效

```python
"""
    变量在函数中的作用域
"""

def testA():
    num=100
    print(num)

testA() #100
# print(num) # 报错: name 'num' is not defined. Did you mean: 'sum'?
```

局部变量的作用：在函数体内部，临时保存数据，即函数调用后自动销毁局部变量

全局变量，指的是在函数体内、外都能生效的变量

```python
# 演示全局变量
# 定义全局变量num
num = 100
def testA():
    print(f"testA函数中的num: {num}")

def testB():
    # 将num修改为200，但其实他是局部变量，只在函数内有效
    num = 200
    print(f"testB函数中的num: {num}")

testA() # 100
testB() # 200
print(num) # 100
```

使用global关键字可以在函数内部声明变量为全局变量，在函数内部和外部均可使用

```python
# 语法
global 变量名

# 演示全局变量
# 定义全局变量num
num = 100
def testA():
    print(f"testA函数中的num: {num}")

def testB():
    # 使用global关键字声明num为全局变量
    global num
    # 将num修改为200，但其实他是局部变量，只在函数内有效
    num = 200
    print(f"testB函数中的num: {num}")

testA() # 100
testB() # 200
print(f"全局变量num={num}") # 200
```



## 案例

```python
"""
    函数的综合案例
    ATM机模拟
    定义一个全局变量：money，用来记录银行卡余额（默认5000000）
    定义一个全局变量：name，用来记录客户姓名（启动程序时输入）
    定义如下的函数：
    ·查询余额函数
    ·存款函数
    ·取款函数
    ·主菜单函数
    要求:
    程序启动后要求输入客户姓名
    查询余额、存款、取款后都会返回主菜单
    存款、取款后，都应显示一下当前余额
    客户选择退出或输入错误，程序会退出，否则一直运行
"""

# 定义全局变量
money = 5000000
name = input("请输入客户姓名: ")


def query_balance():
    """查询余额函数"""
    print(f"{name}您好，您当前余额为: {money}元")


def deposit():
    """存款函数"""
    global money
    amount = float(input("请输入存款金额: "))
    if amount > 0:
        money += amount
        print(f"存款成功，当前余额: {money}元")
    else:
        print("存款金额必须大于0")


def withdraw():
    """取款函数"""
    global money
    amount = float(input("请输入取款金额: "))
    if amount > 0:
        if amount <= money:
            money -= amount
            print(f"取款成功，当前余额: {money}元")
        else:
            print("余额不足，取款失败")
    else:
        print("取款金额必须大于0")


def main_menu():
    """主菜单函数"""
    while True:
        print(f"{name}，欢迎使用ATM机")
        print("1. 查询余额")
        print("2. 存款")
        print("3. 取款")
        print("4. 退出")

        choice = input("请选择操作 (1/2/3/4): ")

        if choice == '1':
            query_balance()
        elif choice == '2':
            deposit()
        elif choice == '3':
            withdraw()
        elif choice == '4':
            print("感谢使用ATM机，欢迎下次光临!")
            break
        else:
            print("输入错误，请重新选择操作")

main_menu()
```



# 数据容器

Python中的数据容器：一种可以容纳多份数据的数据类型，容纳的每一份数据称之为1个元素

每一个元素，可以是任意类型的数据，如字符串、数字、布尔等。

数据容器根据特点的不同，如：

- 是否支持重复元素
- 是否可以修改
- 是否有序

分为5类，分别是：列表(list)、元组(tuple）、字符串（str)、集合（set)、字典(dict)



## List列表

列表内的每一个数据，称之为元素，以**[]作为标识**，列表内每一个元素之间用，**逗号隔开**。

```python
#基本语法：

# 字面量
[元素1,元素2,元素3,元素,...]

# 定义变量
变量名称=[元素1,元素2,元素3,元素4,...]

# 定义空列表
变量名称＝[]
变量名称=list()

"""
    演示数据容器之：list列表
    语法：[元素1,元素2,...]
"""

# 定义一个列表list
name_list = ['张三', '李四', '王五', '赵六']
print(name_list)
print(type(name_list))

# 定义一个包含多种数据类型的列表
info_list = ['张三', 18, True]
print(info_list)
print(type(info_list))

# 定义一个嵌套的列表
nested_list = [[1,2,3], ['a', 'b', 'c'], [True, False]]
print(nested_list)
print(type(nested_list))
```

如何从列表中取出特定位置的数据呢？我们可以使用：下标索引，列表中的每一个元素，都有其位置下标索引，从前向后的方向，**从0开始，依次递增**
我们只需要按照下标索引，即可取得对应位置的元素，或者，可以反向索引，也就是从后向前：从-1开始，依次递减（-1、-2、-3、...）如果列表是嵌套的列表，同样支持下标索引。

```python
"""
    演示数据容器之：list列表
    语法：[元素1,元素2,...]
"""

# 定义一个列表list
name_list = ['张三', '李四', '王五', '赵六']
print(name_list)
print(type(name_list))

# 定义一个包含多种数据类型的列表
info_list = ['张三', 18, True]
print(info_list)
print(type(info_list))

# 定义一个嵌套的列表
nested_list = [[1,2,3], ['a', 'b', 'c'], [True, False]]
print(nested_list)
print(type(nested_list))

# 通过下标索引取出对应位置的数据
print(name_list[0])  # 取出第一个元素
print(name_list[1])  # 取出第二个元素
print(name_list[2])  # 取出第三个元素
print(name_list[3])  # 取出第四个元素

# 通过反向索引取出对应位置的数据
print(name_list[-1])  # 取出倒数一个元素
print(name_list[-2])  # 取出倒数二个元素
print(name_list[-3])  # 取出倒数三个元素
print(name_list[-4])  # 取出倒数四个元素


# 通过下标索引取出数据（倒序取出）
# range(3, 0, -1)  # 从3到-1，步长为-1,3是因为列表中的下表是从0开始的
for i in range(len(name_list)-1, 0, -1):
    print(name_list[i])

# 取出嵌套列表的元素
print(nested_list[0][0])  # 取出嵌套列表的第一个列表的第一个元素，即1
print(nested_list[0][1])  # 取出嵌套列表的第一个列表的第二个元素，即2
print(nested_list[0][2])  # 取出嵌套列表的第一个列表的第三个元素，即3
print(nested_list[1][0])  # 取出嵌套列表的第二个列表的第一个元素，即a
print(nested_list[1][1])  # 取出嵌套列表的第二个列表的第二个元素，即b
print(nested_list[1][2])  # 取出嵌套列表的第二个列表的第三个元素，即c
print(nested_list[2][0])  # 取出嵌套列表的第三个列表的第一个元素，即True
print(nested_list[2][1])  # 取出嵌套列表的第三个列表的第二个元素，即False
```



## 列表的常用操作

列表除了可以：

- 定义
- 使用下标索引获取值

以外，列表也提供了一系列功能：

- 插入元素
- 删除元素
- 清空列表
- 修改元素
- 统计元素个数

等等功能，这些功能我们都称之为：列表的方法

| 序号 | 使用方式               | 作用                                     |
| ---- | ---------------------- | ---------------------------------------- |
| 1    | 列表.append(元素)      | 向列表中追加一个元素                     |
| 2    | 列表.extend(容器)      | 将数据容器的内容依次取出，追加到列表尾部 |
| 3    | 列表.insert(下标,元素) | 在指定下标处，插入指定的元素             |
| 4    | del 列表[下标]         | 删除列表指定下标元素                     |
| 5    | 列表.pop(下标)         | 删除列表指定下标元素                     |
| 6    | 列表.remove(元素)      | 从前向后，删除此元素第一个匹配项         |
| 7    | 列表.clear()           | 清空列表                                 |
| 8    | 列表.count(元素)       | 统计目标元素在列表中出现的次数           |
| 9    | 列表.index(元素)       | 查找指定元素在列表的下标                 |
| 10   | len(元素)              | 统计容器内有多少个元素                   |

### 查找某元素的下标

功能：查找指定元素在列表的下标，如果找不到，报错ValueError

语法：列表.index(元素)

index就是列表对象（变量）内置的方法（函数）

```python
"""
    List列表的常用操作
"""
name_list = ['张三', '李四', '王五', '赵六']
# 1.1查找某元素在列表内的下标索引
index_zhangsan = name_list.index("张三")
print(f"张三在列表中的下标索引是：{index_zhangsan}")

# 1.2如果被查找的元素不存在，会报错
# index_lisi = name_list.index("李四2")
# print(f"李四2在列表中的下标索引是：{index_lisi}")  # 会报错：ValueError: '李四2' is not in list
```

### 修改特定位置（索引）的元素值

语法：列表[下标]＝值
可以使用如上语法，直接对指定下标（正向、反向下标均可）的值进行：重新赋值（修改）

```python
"""
    List列表的常用操作
"""
name_list = ['张三', '李四', '王五', '赵六']

# 2.修改特定下标索引的值
name_list[0] = '王小明'  # 修改第一个元素
print(f"修改后的列表：{name_list}")

name_list[-1] = '王小明'  # 修改最后一个元素
print(f"修改最后一个元素后的列表：{name_list}")
```

### 插入元素

语法：列表.insert(下标，元素)，在指定的下标位置，插入指定的元素

```python
"""
    List列表的常用操作
"""
name_list = ['张三', '李四', '王五', '赵六']

# 3.在指定下标位置插入新元素
name_list.insert(2, '刘备')  # 在下标为2的位置插入新元素
print(f"在下标2位置插入刘备后的列表：{name_list}")
```

### 追加元素

语法：列表append(元素)，将指定元素，追加到列表的尾部

```python
"""
    List列表的常用操作
"""
name_list = ['张三', '李四', '王五', '赵六']

# 4.在列表的尾部追加单个新元素
name_list.append('孙尚香')  # 在列表的尾部追加新元素
print(f"在列表尾部追加孙尚香后的列表：{name_list}")
```

### 批量追加元素

语法：列表.extend(其它数据容器)，将其它数据容器的内容取出，依次追加到列表尾部

```python
"""
    List列表的常用操作
"""
name_list = ['张三', '李四', '王五', '赵六']

# 5.在列表的尾部追加一批新元素
name_list.extend(['诸葛亮', '周瑜'])  # 在列表的尾部追加一批新元素
print(f"在列表尾部追加诸葛亮和周瑜后的列表：{name_list}")
```

### 删除元素

语法1：del列表[下标]
语法2：列表.pop(下标)

```python
"""
    List列表的常用操作
"""
name_list = ['张三', '李四', '王五', '赵六']

# 6.删除指定下标索引的元素（2种方式）
# 6.1方式1:del列表[下标]
del name_list[1]  # 删除下标为1的元素
print(name_list)

# 6.2 方式2:列表.pop(下标)
name_list.pop(1)  # 删除下标为1的元素
print(name_list)
```

### 删除某元素在列表中的第一个匹配项

语法：列表.remove(元素)

```python
"""
    List列表的常用操作
"""
name_list = ['张三', '李四', '王五', '赵六']

# 7.删除某元素在列表中的第一个匹配项
name_list.remove('王小明')  # 删除列表中第一个匹配的元素
print(f"删除第一个匹配的王小明后的列表：{name_list}")
```

### 清空列表

语法：列表.clear()

```python
"""
    List列表的常用操作
"""
name_list = ['张三', '李四', '王五', '赵六']

# 8.清空列表
name_list.clear()  # 清空列表
print(f"清空列表后的列表：{name_list}")
```

### 统计某元素在列表内的数量

语法：列表.count(元素)

```python
"""
    List列表的常用操作
"""

# 9.统计到表内某元素的数量
name_list = ['张三', '李四', '王五', '张三', '赵六']
count_zhangsan = name_list.count('张三')  # 统计列表中'张三'的数量
print(f"列表中'张三'的数量是：{count_zhangsan}")

```

### 统计列表元素

语法：len(列表)，可以得到一个int数字，表示列表内的元素数量

```python
"""
    List列表的常用操作
"""
name_list = ['张三', '李四', '王五', '赵六']

# 10.统计列表中全部的元素数量
count_total = len(name_list)  # 统计列表中全部元素的数量
print(f"列表中全部元素的数量是：{count_total}")
```

### 列表排序

语法：列表.sort(key=选择排序依据的函数,reverse=True|False)

- 参数key，是要求传入一个函数，表示将列表的每一个元素都传入函数中，返回排序的依据
- 参数reverse，是否反转排序结果，True表示降序，False表示升序

```python
"""
    列表排序
"""

my_list = [["a", 33], ["b", 55], ["c", 11]]


# 定义排序方法,使用元素的第二个值进行排序
# def choose_sort_key(element):
#     return element[1]

# 使用带名函数进行排序
# 将元素传入choose_sort_key函数中，用来确定按照谁来排序
# my_list.sort(key=choose_sort_key, reverse=True)
# print(my_list)

# 使用lambda表达式简化排序方法
my_list.sort(key=lambda element: element[1], reverse=True)
print(my_list)
```



**列表的特点**

1.可以容纳多个元素（上限为2**63-1、9223372036854775807个）

2.可以容纳不同类型的元素（混装）

3.数据是有序存储的（有下标序号）

4.允许重复数据存在

5.可以修改（增加或删除元素等）



**列表的遍历**

既然数据容器可以存储多个元素，那么，就会有需求从容器内依次取出元素进行操作。
将容器内的元素依次取出进行处理的行为，称之为：遍历、迭代。

使用while循环对列表进行遍历

```python
"""
    列表的循环
"""

def list_while():
    """
        使用while循环对列表进行遍历
        如何在循环中取出列表的元素呢?
        使用列表[下标]的方式取出
        循环条件如何控制？
        定义一个变量表示下标，从0开始
        循环条件为下标值<列表的元素数量
    :return: None
    """
    name_list = ['张三', '李四', '王五', '赵六']
    index = 0  # 初始化下标索引
    while index < len(name_list):  # 当下标索引小于列表长度时，继续循环
        print(name_list[index])  # 打印当前下标索引对应的元素
        index += 1  # 下标索引自增1


list_while()
```

使用for循环对列表进行遍历

```python
"""
    列表的循环
"""


def list_for():
    """
        使用for循环对列表进行遍历
    :return: None
    """
    name_list = ['张三', '李四', '王五', '赵六']
    for name in name_list:
        print(name)

list_for()
```



## 元组

元组同列表一样，都是可以封装多个、不同类型的元素在内。
但最大的不同点在于：**元组一旦定义完成，就不可修改**

元组定义：定义元组使用**小括号**，且**使用逗号**隔开各个数据，数据可以是不同的数据类型。

```python
"""
    元组的定义
    #定义元组字面量
    (元素1,元素2,...元素)

    #定义元组变量
    变量名称=(元素1,元素2,...元素)

    #定义空元组
    变量名称=() # 方式1
    变量名称=tuple() # 方式2
"""

# 定义元组字面量
print(f"{(1, '张三', True)},类型：{type((1, '张三', True))}")

# 定义元组变量
number_tuple = (1, '张三', True)
print(number_tuple)
print(type(number_tuple))

# 定义空元组
empty_tuple = ()  # 方式1
print(empty_tuple)
print(type(empty_tuple))
empty_tuple = tuple()  # 方式2
print(empty_tuple)
print(type(empty_tuple))

# 定义单个元素的元组,需要在元素后添加逗号
single_element_tuple = (1)  # 错误示例，单个元素的元组需要逗号,否则会被当作字面量
print(single_element_tuple)
print(type(single_element_tuple))
single_element_tuple = (1,)  # 注意逗号
print(single_element_tuple)
print(type(single_element_tuple))

# 元组的嵌套
nested_tuple = ((1, 2, 3), (4, 5, 6))
print(nested_tuple)
print(type(nested_tuple))

# 通过下标取出元素
print(nested_tuple[1][2])  # 输出6
```

**元组的操作**

| 序号 | 方法    | 作用                                     |
| ---- | ------- | ---------------------------------------- |
| 1    | index() | 查找某个数据，如果数据存在返回对应的下标 |
| 2    | count() | 统计某个数据在当前元组出现的次数         |
| 3    | len()   | 统计元组内的元素个数                     |

```python
# 元组的操作：index查找方法
name_tuple = ('张三', '李四', '王五', '赵六', '张三')
print(name_tuple.index("李四"))  # 查找元素'李四'在元组中的索引位置

# 元组的操作:count统计方法
print(name_tuple.count("张三"))  # 统计元素'张三'在元组中出现的次数

# 元组的操作：len函数统计元组元素数量
print(len(name_tuple))  # 输出元组中元素的数量

# 元组的遍历：while
name_tuple = ('张三', '李四', '王五', '赵六')
index = 0
while index < len(name_tuple):
    print(name_tuple[index])
    index += 1

# 元组的遍历：for
name_tuple = ('张三', '李四', '王五', '赵六')
for name in name_tuple:
    print(name)

# 尝试修改元组中的元素
name_tuple = ('张三', '李四', '王五', '赵六')
# name_tuple[0] = '小明'  # TypeError: 'tuple' object does not support item assignment

name_tuple = ('张三', '李四', ['王五', '赵六'])
print(name_tuple[2])
name_tuple[2][0] = '小明'  # 修改元组中嵌套的列表元素,是可以的
print(name_tuple[2])
```



**元组的特点**

- 可以容纳多个数据
- 可以容纳不同类型的数据（混装）
- 数据是有序存储的（下标索引）
- 允许重复数据存在
- 不可以修改（增加或删除元素等）
- 支持for循环



## 字符串

字符串是字符的容器，一个字符串可以存放任意数量的字符。如，字符串："mumangguo"

和其它容器如：列表、元组一样，字符串也可以通过下标进行访问

- 从前向后，下标从0开始
- 从后向前，下标从-1开始

同元组一样，字符串是一个：无法修改的数据容器。
修改指定下标的字符如：字符串[0]="A"、移除特定下标的字符如：del字符串[o]、字符串.remove()、字符串.pop()等、追加字符等如：字符串.append()都是无法完成，如果必须要修改，只能得到一个新的字符串，旧的字符串是无法修改的。

| 序号 | 操作                                | 说明                                                         |
| ---- | ----------------------------------- | ------------------------------------------------------------ |
| 1    | 字符串[下标]                        | 根据下标索引取出特定位置字符                                 |
| 2    | 字符串.index(字符串)                | 查找给定字符的第一个匹配项的下标                             |
| 3    | 字符串.replace(字符串1,字符串2)     | 将字符串内的全部字符串1，替换为字符串2，不会修改原字符串，而是得到一个新的字符串 |
| 4    | 字符串.split(字符串)                | 按照给定字符串，对字符串进行分割不会修改原字符串，而是得到一个新的列表 |
| 5    | 字符串.strip()/字符串.strip(字符串) | 移出首尾的空格和换行符或指定字符串                           |
| 6    | 字符串.count()                      | 统计字符串内某个字符串出现的次数                             |
| 7    | len(字符串)                         | 统计字符串的字符个数                                         |

```python
"""
    演示字符串作为数据容器的相关操作
"""

my_str = "Hello,World!"

# 通过下标索引取值
print(my_str[0])  # 输出: H
print(my_str[-1])  # 输出: !

#my_str[0] = "A" # TypeError: 'str' object does not support item assignment

# index方法
print(my_str.index("Hello"))  # 输出: 0

# replace方法 语法：字符串.replace(字符串1,字符串2)
# 功能：将字符串内的全部：字符串1替换为字符串2
# 注意：不是修改字符串本身，而是得到了一个新字符串哦
new_str = my_str.replace("World", "Python")
print(new_str)  # 输出: Hello, Python!

# split方法 语法：字符串.split(分隔符字符串）
# 功能：按照指定的分隔符字符串，将字符串划分为多个字符串，并存人列表对象中
# 注意：字符串本身不变，而是得到了一个列表对象
split_str = my_str.split(",")
print(split_str,type(split_str))  # 输出: ['Hello', 'World!'] <class 'list'>
print(split_str[0])  # 输出: Hello
print(split_str[1])  # 输出: World!

# strip方法 字符串的规整操作默认去前后空格,也可以去前后指定字符串
# 语法：字符串strip()
# 语法：字符串.strip(字符串)
strip_str = "   Hello,World!   "
print(strip_str.strip())  # 输出: Hello,World!
strip_str = "12Hello,World!21"
print(strip_str.strip("12"))  # 输出: Hello,World!

# 统计字符串中某字符串的出现次数
print(my_str.count("l"))  # 输出: 3

# 统计字符串的长度
print(len(my_str))  # 输出: 12

# 使用while循环遍历字符串
index = 0
while index < len(my_str):
    print(my_str[index])
    index += 1

# 使用for循环遍历字符串
for i in my_str:
    print(i)
```



**字符串的特点**

- 只可以存储字符串
- 长度任意（取决于内存大小）
- 支持下标索引
- 允许重复字符串存在
- 不可以修改（增加或删除元素等）
- 支持for循环



## 序列切片

序列是指：内容连续、有序，可使用下标索引的一类数据容器
列表、元组、字符串，均可以可以视为序列。

序列支持切片，即：列表、元组、字符串，均支持进行切片操作
切片：从一个序列中，取出一个子序列

语法：序列[起始下标:结束下标:步长]

表示从序列中，从指定位置开始，依次取出元素，到指定位置结束，得到一个新序列：

- 起始下标表示从何处开始，可以留空，留空视作从头开始
- 结束下标（不含）表示何处结束，可以留空，留空视作截取到结尾
- 步长表示，依次取元素的间隔
- 步长1表示，一个个取元素
- 步长2表示，每次跳过1个元素取
- 步长N表示，每次跳过N-1个元素取
- 步长为负数表示，反向取（注意，起始下标和结束下标也要反向标记)
- 起始可以省略，省略从头开始，序列[:结束下标:步长]
- 结束可以省略，省略到尾结束，序列[起始下标::步长]
- 步长可以省略，省略步长为1（可以为负数，表示倒序执行），序列[起始下标:结束下标]

```python
"""
    演示对序列进行切片操作
"""

# 对list进行切片，从1开始，4结束，步长1
my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(my_list[1:4])  # 输出: [2, 3, 4]

# 对tuple进行切片，从头开始，到最后结束，步长1
my_tuple = (10, 20, 30, 40, 50)
print(my_tuple[:])  # 起始和结束不写表示从头到尾，步长为可以省略，则输出: (10, 20, 30, 40, 50)

# 对str进行切片，从头开始，到最后结束，步长2
my_str = "123456789"
print(my_str[::2])  # 输出: 13579

# 对str进行切片，从头开始，到最后结束，步长-1
my_str = "123456789"
print(my_str[::-1])  # 输出: 987654321

# 对列表进行切片，从3开始，到1结束，步长-1
my_list = [1, 2, 3, 4, 5, 6, 7, 8, 9]
print(my_list[3:1:-1])  # 输出: [4, 3]

# 对元组进行切片，从头开始，到尾结束，步长-2
my_tuple = (10, 20, 30, 40, 50)
print(my_tuple[::-2])  # 输出: (50, 30, 10)

# 案例，在以下字符串中提取木芒果
str = "你爱我，果芒木跟，nohtyP习学"
# 方式一：倒序字符串，切片取出
print(str[::-1][10:13])

# 方式二：切片取出，然后倒序
print(str[4:7][::-1])

# 方式三：使用split方法分割字符串，取出第二个元素后倒序
print(str.split("，")[1][::-1][1:])
```



## 集合

集合，最主要的特点就是：不支持元素的重复（自带去重功能）、并且内容无序；列表可修改、支持重复元素且有序；元组、字符串不可修改、支持重复元素且有序，它们都支持重复元素。和列表、元组、字符串等定义基本相同：列表使用：[ ]、元组使用：( )、字符串使用：" "、集合使用：{ }。

```python
# 基本语法：
# 定义集合字面量
{元素,元素,元素...}

# 定义集合变量
变量名称={元素,元素,...元素}

# 定义空集合
变量名称=set()

"""
    集合的使用
"""

# 定义集合
fruit_set = {"apple", "banana", "cherry", "apple", "apple", "cherry"}
print(fruit_set, type(fruit_set))
empty_set = set()  # 定义一个空集合
print(empty_set, type(empty_set))
```

集合是无序的，所以集合不支持：下标索引访问，但是集合和列表一样，是允许修改的。

| 序号 | 操作                           | 说明                                                        |
| ---- | ------------------------------ | ----------------------------------------------------------- |
| 1    | 集合.add(元素)                 | 集合内添加一个元素                                          |
| 2    | 集合.remove(元素)              | 移出集合内指定的元素                                        |
| 3    | 集合.pop()                     | 从集合中随机取出一个元素                                    |
| 4    | 集合.clear()                   | 将集合清空                                                  |
| 5    | 集合1.difference(集合2)        | 得到一个新集合，内含2个集合的差集原有的2个集合内容不变      |
| 6    | 集合1.difference_update(集合2) | 在集合1中，删除集合2中存在的元素，集合1被修改，集合2不变    |
| 7    | 集合1.union(集合2)             | 得到1个新集合，内含2个集合的全部元素，原有的2个集合内容不变 |
| 8    | len(集合)                      | 得到一个整合，记录了集合的元素数量                          |

```python
"""
    集合的使用
"""

# 定义集合
fruit_set = {"apple", "banana", "cherry", "apple", "apple", "cherry"}
print(fruit_set, type(fruit_set))
empty_set = set()  # 定义一个空集合
print(empty_set, type(empty_set))

# 添加新元素 语法：集合.add(元素)。将指定元素，添加到集合内
# 结果：集合本身被修改，添加了新元素
fruit_set.add("orange")
print(fruit_set)

# 移除元素
# 语法：集合.remove(元素)。将指定元素，从集合内删除
# 结果：集合本身被修改，移除了元素
fruit_set.remove("banana")
print(fruit_set)

# 随机取出一个元素 语法：集合.pop()功能，从集合中随机取出一个元素
# 结果：会得到一个元素的结果。同时集合本身被修改，元素被移除
random_fruit = fruit_set.pop()
print(random_fruit)

# 清空集合
fruit_set.clear()
print(fruit_set)

# 取2个集合的差集 语法：集合1.difference(集合2)
# 功能：取出集合1和集合2的差集（集合1有而集合2没有的）
# 结果：得到一个新集合，集合1和集合2不变
set1 = {1, 2, 3}
set2 = {1, 5, 6}
difference_set = set1.difference(set2)
print(difference_set)  # 输出: {2, 3}
print(set1)  # 输出: {1, 2, 3}
print(set2)  # 输出: {1, 5, 6}

# 消除2个集合的差集 语法：集合1.difference_update(集合2)
# 功能：对比集合1和集合2，在集合1内，删除和集合2相同的元素。
# 结果：集合1被修改，集合2不变
set1 = {1, 2, 3}
set2 = {1, 5, 6}
set1.difference_update(set2)
print(set1)  # 输出: {2, 3}
print(set2)  # 输出: {1, 5, 6}

# 2个集合合并为1个 语法：集合1.union(集合2)
# 功能：将集合1和集合2组合成新集合
# 结果：得到新集合，集合1和集合2不变
set1 = {1, 2, 3}
set2 = {1, 5, 6}
union_set = set1.union(set2)
print(union_set)  # 输出: {1, 2, 3, 5, 6}
print(set1)  # 输出: {1, 2, 3}
print(set2)  # 输出: {1, 5, 6}

# 统计集合元素数量
set1 = {1, 2, 3, 4, 5, 1, 2, 3, 4, 5}
print(len(set1))

# 集合的遍历,集合不支持下标索引，不能用while循环,只能用for循环遍历
fruit_set = {"apple", "banana", "cherry", "apple", "apple", "cherry"}
for fruit in fruit_set:
    print(fruit)
```



**集合的特点**

- 可以容纳多个数据
- 可以容纳不同类型的数据（混装）
- 数据是无序存储的（不支持下标索引）
- 不允许重复数据存在
- 可以修改（增加或删除元素等）
- 支持for循环



## 字典

Python中的字典，是一组包含键值对(key-value)的数据。

老师有一份名单，记录了学生的姓名和考试总成绩。

| 姓名 | 成绩 |
| ---- | ---- |
| 张三 | 88   |
| 李四 | 90   |
| 王五 | 91   |

现在需要将其通过Python录入至程序中，并可以**通过学生姓名检索学生的成绩**。

使用字典最为合适：可以通过Key（学生姓名），取到对应的Value（考试成绩）

字典的定义，同样使用{}，不过存储的元素是一个个的：键值对。字典同集合一样，不可以使用下标索引，但是字典可以通过Key值来取得对应的Value。
```python
# 定义字典字面量
{key: value,key: value,key: value}

#定义字典变量
my_dict = {key: value,key: value,key: value}

#定义空字典
my_dict = {} #空字典定义方式1
my_dict = dict() #空字典定义方式2

"""
    字典的使用
"""

# 定义字典
students = {"张三": 88, "李四": 90, "王五": 91}
print(students,type(students))

# 定义空字典
empty_dict = {}
print(empty_dict,type(empty_dict))
empty_dict = dict()
print(empty_dict,type(empty_dict))

# 定义重复Key的字典
students = {"张三": 88, "李四": 90, "王五": 91, "张三": 95}
print(students, type(students))

# 从字典中基于Key获取Value
print(students["张三"])  # 输出：95
print(students.get("李四"))  # 输出：95

# 定义嵌套字典
students = {
    "张三": {"语文": 88, "数学": 20, "英语": 30},
    "李四": {"语文": 90, "数学": 30, "英语": 60},
    "王五": {"语文": 91, "数学": 40, "英语": 80}
}
print(students)

# 从嵌套字典中获取数据
print(students["张三"].get("语文"))
print(students["王五"].get("数学"))
```



**字典的常用操作**

| 序号 | 操作              | 说明                                          |
| ---- | ----------------- | --------------------------------------------- |
| 1    | 字典[key]         | 获取指定Key对饮的Value值                      |
| 2    | 字典[key] = value | 添加或更新键值对                              |
| 3    | 字典.pop(key)     | 取出Key对应的Value并在字典内删除此Key的键值对 |
| 4    | 字典.clear()      | 清空字典                                      |
| 5    | 字典.keys()       | 获取字典的全部Key，可用于for循环遍历字典      |
| 6    | len(字典)         | 计算字典内的元素数量                          |

```python
"""
    字典的常用操作
"""

# 新增元素,语法：字典[Key]=Value
# 结果：字典被修改，新增了元素
students = {"张三": 88, "李四": 90, "王五": 91}
students["赵六"] = 85
print(students)

# 更新元素,语法：字典[Key]=Value
# 结果：字典被修改，元素被更新
# 注意：字典Key不可以重复，所以对已存在的Key执行上述操作，就是更新value值
students["张三"] = 95
print(students)

# 删除元素 语法：字典pop(Key)，结果：获得指定Key的Value，同时字典被修改，指定Key的数据被删除
students.pop("李四")
print(students)

# 清空元素 语法：字典.clear()，结果：字典被修改，元素被清空
# students.clear()
# print(students)

# 获取全部的key 语法：字典.keys() 结果：得到字典中的全部Key
keys = students.keys()
print(keys)

# 遍历字典,通过keys()方法获取所有的Key，然后遍历Key来获取对应的Value
for key in students.keys():
    print(key, students[key])

# 遍历字典,直接遍历字典，默认遍历Key
for key in students:
    print(key, students[key])

# 统计字典内的元素数量
# 语法：len(字典)，结果：返回字典内的元素数量
count = len(students)
print(f"字典内的元素数量为: {count}")

# 案例
employee_dict = {
    "张三": {
        "部门": "科技部",
        "工资": 3000,
        "级别": 1
    },
    "李四": {
        "部门": "市场部",
        "工资": 5000,
        "级别": 2
    },
    "王五": {
        "部门": "市场部",
        "工资": 7000,
        "级别": 3
    },
    "赵六": {
        "部门": "科技部",
        "工资": 4000,
        "级别": 1
    },
    "陈七": {
        "部门": "市场部",
        "工资": 6000,
        "级别": 2
    },
}
print(employee_dict)
for employee in employee_dict:
    # 给所有级别为1的员工，级别上升1级，薪水增加1000
    if employee_dict[employee]["级别"] == 1:
        employee_dict[employee]["级别"] = 2
        employee_dict[employee]["工资"] += 1000

print(employee_dict)
```

**字典的特点**

- 可以容纳多个数据
- 可以容纳不同类型的数据
- 每一份数据是Key/Value键值对
- 可以通过Key获取到Value，Key不可重复（重复会覆盖）
- 不支持下标索引
- 可以修改（增加或删除更新元素等）
- 支持for循环，不支持while循环



## 数据容器分类

数据容器可以从以下视角进行简单的分类：

1.是否支持下标索引

- 支持：列表、元组、字符串一序列类型
- 不支持：集合、字典一非序列类型

2.是否支持重复元素

- 支持：列表、元组、字符串一序列类型
- 不支持：集合、字典一非序列类型

3.是否可以修改

- 支持：列表、集合、字典
- 不支持：元组、字符串

|          | 列表                             | 元组                               | 字符串             | 集合                   | 字典                                                |
| -------- | -------------------------------- | ---------------------------------- | ------------------ | ---------------------- | --------------------------------------------------- |
| 元素数量 | 支持多个                         | 支持多个                           | 支持多个           | 支持多个               | 支持多个                                            |
| 元素类型 | 任意                             | 任意                               | **仅字符**         | 任意                   | **Key:Value，key除字典外任意类型，Value：任意类型** |
| 下标索引 | 支持                             | 支持                               | 支持               | **不支持**             | **不支持**                                          |
| 重复元素 | 支持                             | 支持                               | 支持               | **不支持**             | **不支持**                                          |
| 可修改性 | 支持                             | **不支持**                         | **不支持**         | 支持                   | 支持                                                |
| 数据有序 | 是                               | 是                                 | 是                 | **否**                 | **否**                                              |
| 使用场景 | 可修改、可重复的一批数据记录场景 | 不可修改、可重复的一批数据记录场景 | 一串字符的记录场景 | 不可重复的数据记录场景 | 以Key检索Value的数据记录场景                        |



## 数据容器的通用操作

| 功能                        | 描述                                                 |
| --------------------------- | ---------------------------------------------------- |
| 通用for循环                 | 遍历容器（字典是遍历Key）                            |
| max()                       | 容器内最大元素                                       |
| min()                       | 容器内最小元素                                       |
| len()                       | 容器元素个数                                         |
| list()                      | 转换为列表                                           |
| tuple()                     | 转换为元组                                           |
| str()                       | 转换为字符串                                         |
| set()                       | 转换为集合                                           |
| sorted(序列,[reverse=True]) | 排序，reverse=True表示降序，返回一个排好序的**列表** |

```python
"""
    数据容器的通用操作
"""

my_list = [1, 2, 3, 4, 5]
my_tuple = (1, 2, 3, 4, 5)
my_str = "abcdefg"
my_set = {1, 2, 3, 4, 5}
my_dict = {"key1": 1, "key2": 2, "key3": 3, "key4": 4, "key5": 5}

# len元素个数
print(f"列表元素个数有:{len(my_list)}")
print(f"元组元素个数有:{len(my_tuple)}")
print(f"字符串元素个数有：{len(my_str)}")
print(f"集合元素个数有:{len(my_set)}")
print(f"字典元素个数有:{len(my_dict)}")

# max最大元素
print(f"列表最大元素是:{max(my_list)}")
print(f"元组最大元素是:{max(my_tuple)}")
print(f"字符串最大元素是：{max(my_str)}")
print(f"集合最大元素是:{max(my_set)}")
print(f"字典最大元素是:{max(my_dict)}")

# min最小元素
print(f"列表最小元素是:{min(my_list)}")
print(f"元组最小元素是:{min(my_tuple)}")
print(f"字符串最小元素是：{min(my_str)}")
print(f"集合最小元素是:{min(my_set)}")
print(f"字典最小元素是:{min(my_dict)}")

# 类型转换：容器转列表
my_list_from_list = list(my_list)
my_list_from_tuple = list(my_tuple)
my_list_from_str = list(my_str)
my_list_from_set = list(my_set)
my_list_from_dict = list(my_dict)
print(f"列表转列表：{my_list_from_list}", f"类型：{type(my_list_from_list)}")
print(f"元组转列表：{my_list_from_tuple}", f"类型：{type(my_list_from_tuple)}")
print(f"字符串转列表：{my_list_from_str}", f"类型：{type(my_list_from_str)}")
print(f"集合转列表：{my_list_from_set}", f"类型：{type(my_list_from_set)}")
print(f"字典转列表：{my_list_from_dict}", f"类型：{type(my_list_from_dict)}")

# 类型转换：容器转元组
my_tuple_from_list = tuple(my_list)
my_tuple_from_tuple = tuple(my_tuple)
my_tuple_from_str = tuple(my_str)
my_tuple_from_set = tuple(my_set)
my_tuple_from_dict = tuple(my_dict)
print(f"列表转元组：{my_tuple_from_list}", f"类型：{type(my_tuple_from_list)}")
print(f"元组转元组：{my_tuple_from_tuple}", f"类型：{type(my_tuple_from_tuple)}")
print(f"字符串转元组：{my_tuple_from_str}", f"类型：{type(my_tuple_from_str)}")
print(f"集合转元组：{my_tuple_from_set}", f"类型：{type(my_tuple_from_set)}")
print(f"字典转元组：{my_tuple_from_dict}", f"类型：{type(my_tuple_from_dict)}")

# 类型转换：容器转字符串
my_str_from_list = str(my_list)
my_str_from_tuple = str(my_tuple)
my_str_from_str = str(my_str)
my_str_from_set = str(my_set)
my_str_from_dict = str(my_dict)
print(f"列表转字符串：{my_str_from_list}", f"类型：{type(my_str_from_list)}")
print(f"元组转字符串：{my_str_from_tuple}", f"类型：{type(my_str_from_tuple)}")
print(f"字符串转字符串：{my_str_from_str}", f"类型：{type(my_str_from_str)}")
print(f"集合转字符串：{my_str_from_set}", f"类型：{type(my_str_from_set)}")
print(f"字典转字符串：{my_str_from_dict}", f"类型：{type(my_str_from_dict)}")

# 类型转换：容器转集合
my_set_from_list = set(my_list)
my_set_from_tuple = set(my_tuple)
my_set_from_str = set(my_str)
my_set_from_set = set(my_set)
my_set_from_dict = set(my_dict)
print(f"列表转集合：{my_set_from_list}", f"类型：{type(my_set_from_list)}")
print(f"元组转集合：{my_set_from_tuple}", f"类型：{type(my_set_from_tuple)}")
print(f"字符串转集合：{my_set_from_str}", f"类型：{type(my_set_from_str)}")
print(f"集合转集合：{my_set_from_set}", f"类型：{type(my_set_from_set)}")
print(f"字典转集合：{my_set_from_dict}", f"类型：{type(my_set_from_dict)}")

# sorted排序
my_list = [3, 4, 1, 2, 5]
my_tuple = (3, 4, 1, 2, 5)
my_str = "cddbefg"
my_set = {3, 4, 1, 2, 5}
my_dict = {"key3": 3, "key4": 4, "key1": 1, "key2": 2, "key5": 5}
print(f"列表排序：{sorted(my_list)}")
print(f"元组排序：{sorted(my_tuple)}")
print(f"字符串排序：{sorted(my_str)}")
print(f"集合排序：{sorted(my_set)}")
print(f"字典排序：{sorted(my_dict)}")

# reversed反转
print(f"列表排序：{sorted(my_list, reverse=True)}")
print(f"元组排序：{sorted(my_tuple, reverse=True)}")
print(f"字符串排序：{sorted(my_str, reverse=True)}")
print(f"集合排序：{sorted(my_set, reverse=True)}")
print(f"字典排序：{sorted(my_dict, reverse=True)}")
```



## 字符串大小比较

ASCII码表

在程序中，字符串所用的所有字符如：

- 大小写英文单词
- 数字
- 特殊符号(!、\、/、@、#、空格等)

都有其对应的ASCII码表值
每一个字符都能对应上一个：数字的码值
字符串进行比较就是基于数字的码值大小进行比较的

| Bin(二进制) | Oct(八进制) | Dec(十进制) | Hex(十六进制) |          缩写/字符          |     解释     |
| :---------: | :---------: | :---------: | :-----------: | :-------------------------: | :----------: |
|  0000 0000  |     00      |      0      |     0x00      |          NUL(null)          |    空字符    |
|  0000 0001  |     01      |      1      |     0x01      |   SOH(start of headline)    |   标题开始   |
|  0000 0010  |     02      |      2      |     0x02      |     STX (start of text)     |   正文开始   |
|  0000 0011  |     03      |      3      |     0x03      |      ETX (end of text)      |   正文结束   |
|  0000 0100  |     04      |      4      |     0x04      |  EOT (end of transmission)  |   传输结束   |
|  0000 0101  |     05      |      5      |     0x05      |        ENQ (enquiry)        |     请求     |
|  0000 0110  |     06      |      6      |     0x06      |      ACK (acknowledge)      |   收到通知   |
|  0000 0111  |     07      |      7      |     0x07      |         BEL (bell)          |     响铃     |
|  0000 1000  |     010     |      8      |     0x08      |       BS (backspace)        |     退格     |
|  0000 1001  |     011     |      9      |     0x09      |     HT (horizontal tab)     |  水平制表符  |
|  0000 1010  |     012     |     10      |     0x0A      | LF (NL line feed, new line) |    换行键    |
|  0000 1011  |     013     |     11      |     0x0B      |      VT (vertical tab)      |  垂直制表符  |
|  0000 1100  |     014     |     12      |     0x0C      | FF (NP form feed, new page) |    换页键    |
|  0000 1101  |     015     |     13      |     0x0D      |    CR (carriage return)     |    回车键    |
|  0000 1110  |     016     |     14      |     0x0E      |       SO (shift out)        |   不用切换   |
|  0000 1111  |     017     |     15      |     0x0F      |        SI (shift in)        |   启用切换   |
|  0001 0000  |     020     |     16      |     0x10      |   DLE (data link escape)    | 数据链路转义 |
|  0001 0001  |     021     |     17      |     0x11      |   DC1 (device control 1)    |  设备控制1   |
|  0001 0010  |     022     |     18      |     0x12      |   DC2 (device control 2)    |  设备控制2   |
|  0001 0011  |     023     |     19      |     0x13      |   DC3 (device control 3)    |  设备控制3   |
|  0001 0100  |     024     |     20      |     0x14      |   DC4 (device control 4)    |  设备控制4   |
|  0001 0101  |     025     |     21      |     0x15      | NAK (negative acknowledge)  |   拒绝接收   |
|  0001 0110  |     026     |     22      |     0x16      |   SYN (synchronous idle)    |   同步空闲   |
|  0001 0111  |     027     |     23      |     0x17      |  ETB (end of trans. block)  |  结束传输块  |
|  0001 1000  |     030     |     24      |     0x18      |        CAN (cancel)         |     取消     |
|  0001 1001  |     031     |     25      |     0x19      |     EM (end of medium)      |   媒介结束   |
|  0001 1010  |     032     |     26      |     0x1A      |      SUB (substitute)       |     代替     |
|  0001 1011  |     033     |     27      |     0x1B      |        ESC (escape)         |  换码(溢出)  |
|  0001 1100  |     034     |     28      |     0x1C      |     FS (file separator)     |  文件分隔符  |
|  0001 1101  |     035     |     29      |     0x1D      |    GS (group separator)     |    分组符    |
|  0001 1110  |     036     |     30      |     0x1E      |    RS (record separator)    |  记录分隔符  |
|  0001 1111  |     037     |     31      |     0x1F      |     US (unit separator)     |  单元分隔符  |
|  0010 0000  |     040     |     32      |     0x20      |           (space)           |     空格     |
|  0010 0001  |     041     |     33      |     0x21      |              !              |     叹号     |
|  0010 0010  |     042     |     34      |     0x22      |              "              |    双引号    |
|  0010 0011  |     043     |     35      |     0x23      |              #              |     井号     |
|  0010 0100  |     044     |     36      |     0x24      |              $              |    美元符    |
|  0010 0101  |     045     |     37      |     0x25      |              %              |    百分号    |
|  0010 0110  |     046     |     38      |     0x26      |              &              |     和号     |
|  0010 0111  |     047     |     39      |     0x27      |              '              |   闭单引号   |
|  0010 1000  |     050     |     40      |     0x28      |              (              |    开括号    |
|  0010 1001  |     051     |     41      |     0x29      |              )              |    闭括号    |
|  0010 1010  |     052     |     42      |     0x2A      |              *              |     星号     |
|  0010 1011  |     053     |     43      |     0x2B      |              +              |     加号     |
|  0010 1100  |     054     |     44      |     0x2C      |              ,              |     逗号     |
|  0010 1101  |     055     |     45      |     0x2D      |              -              | 减号/破折号  |
|  0010 1110  |     056     |     46      |     0x2E      |              .              |     句号     |
|  0010 1111  |     057     |     47      |     0x2F      |              /              |     斜杠     |
|  0011 0000  |     060     |     48      |     0x30      |              0              |    字符0     |
|  0011 0001  |     061     |     49      |     0x31      |              1              |    字符1     |
|  0011 0010  |     062     |     50      |     0x32      |              2              |    字符2     |
|  0011 0011  |     063     |     51      |     0x33      |              3              |    字符3     |
|  0011 0100  |     064     |     52      |     0x34      |              4              |    字符4     |
|  0011 0101  |     065     |     53      |     0x35      |              5              |    字符5     |
|  0011 0110  |     066     |     54      |     0x36      |              6              |    字符6     |
|  0011 0111  |     067     |     55      |     0x37      |              7              |    字符7     |
|  0011 1000  |     070     |     56      |     0x38      |              8              |    字符8     |
|  0011 1001  |     071     |     57      |     0x39      |              9              |    字符9     |
|  0011 1010  |     072     |     58      |     0x3A      |              :              |     冒号     |
|  0011 1011  |     073     |     59      |     0x3B      |              ;              |     分号     |
|  0011 1100  |     074     |     60      |     0x3C      |              <              |     小于     |
|  0011 1101  |     075     |     61      |     0x3D      |              =              |     等号     |
|  0011 1110  |     076     |     62      |     0x3E      |              >              |     大于     |
|  0011 1111  |     077     |     63      |     0x3F      |              ?              |     问号     |
|  0100 0000  |    0100     |     64      |     0x40      |              @              | 电子邮件符号 |
|  0100 0001  |    0101     |     65      |     0x41      |              A              |  大写字母A   |
|  0100 0010  |    0102     |     66      |     0x42      |              B              |  大写字母B   |
|  0100 0011  |    0103     |     67      |     0x43      |              C              |  大写字母C   |
|  0100 0100  |    0104     |     68      |     0x44      |              D              |  大写字母D   |
|  0100 0101  |    0105     |     69      |     0x45      |              E              |  大写字母E   |
|  0100 0110  |    0106     |     70      |     0x46      |              F              |  大写字母F   |
|  0100 0111  |    0107     |     71      |     0x47      |              G              |  大写字母G   |
|  0100 1000  |    0110     |     72      |     0x48      |              H              |  大写字母H   |
|  0100 1001  |    0111     |     73      |     0x49      |              I              |  大写字母I   |
|  01001010   |    0112     |     74      |     0x4A      |              J              |  大写字母J   |
|  0100 1011  |    0113     |     75      |     0x4B      |              K              |  大写字母K   |
|  0100 1100  |    0114     |     76      |     0x4C      |              L              |  大写字母L   |
|  0100 1101  |    0115     |     77      |     0x4D      |              M              |  大写字母M   |
|  0100 1110  |    0116     |     78      |     0x4E      |              N              |  大写字母N   |
|  0100 1111  |    0117     |     79      |     0x4F      |              O              |  大写字母O   |
|  0101 0000  |    0120     |     80      |     0x50      |              P              |  大写字母P   |
|  0101 0001  |    0121     |     81      |     0x51      |              Q              |  大写字母Q   |
|  0101 0010  |    0122     |     82      |     0x52      |              R              |  大写字母R   |
|  0101 0011  |    0123     |     83      |     0x53      |              S              |  大写字母S   |
|  0101 0100  |    0124     |     84      |     0x54      |              T              |  大写字母T   |
|  0101 0101  |    0125     |     85      |     0x55      |              U              |  大写字母U   |
|  0101 0110  |    0126     |     86      |     0x56      |              V              |  大写字母V   |
|  0101 0111  |    0127     |     87      |     0x57      |              W              |  大写字母W   |
|  0101 1000  |    0130     |     88      |     0x58      |              X              |  大写字母X   |
|  0101 1001  |    0131     |     89      |     0x59      |              Y              |  大写字母Y   |
|  0101 1010  |    0132     |     90      |     0x5A      |              Z              |  大写字母Z   |
|  0101 1011  |    0133     |     91      |     0x5B      |              [              |   开方括号   |
|  0101 1100  |    0134     |     92      |     0x5C      |              \              |    反斜杠    |
|  0101 1101  |    0135     |     93      |     0x5D      |              ]              |   闭方括号   |
|  0101 1110  |    0136     |     94      |     0x5E      |              ^              |    脱字符    |
|  0101 1111  |    0137     |     95      |     0x5F      |              _              |    下划线    |
|  0110 0000  |    0140     |     96      |     0x60      |              `              |   开单引号   |
|  0110 0001  |    0141     |     97      |     0x61      |              a              |  小写字母a   |
|  0110 0010  |    0142     |     98      |     0x62      |              b              |  小写字母b   |
|  0110 0011  |    0143     |     99      |     0x63      |              c              |  小写字母c   |
|  0110 0100  |    0144     |     100     |     0x64      |              d              |  小写字母d   |
|  0110 0101  |    0145     |     101     |     0x65      |              e              |  小写字母e   |
|  0110 0110  |    0146     |     102     |     0x66      |              f              |  小写字母f   |
|  0110 0111  |    0147     |     103     |     0x67      |              g              |  小写字母g   |
|  0110 1000  |    0150     |     104     |     0x68      |              h              |  小写字母h   |
|  0110 1001  |    0151     |     105     |     0x69      |              i              |  小写字母i   |
|  0110 1010  |    0152     |     106     |     0x6A      |              j              |  小写字母j   |
|  0110 1011  |    0153     |     107     |     0x6B      |              k              |  小写字母k   |
|  0110 1100  |    0154     |     108     |     0x6C      |              l              |  小写字母l   |
|  0110 1101  |    0155     |     109     |     0x6D      |              m              |  小写字母m   |
|  0110 1110  |    0156     |     110     |     0x6E      |              n              |  小写字母n   |
|  0110 1111  |    0157     |     111     |     0x6F      |              o              |  小写字母o   |
|  0111 0000  |    0160     |     112     |     0x70      |              p              |  小写字母p   |
|  0111 0001  |    0161     |     113     |     0x71      |              q              |  小写字母q   |
|  0111 0010  |    0162     |     114     |     0x72      |              r              |  小写字母r   |
|  0111 0011  |    0163     |     115     |     0x73      |              s              |  小写字母s   |
|  0111 0100  |    0164     |     116     |     0x74      |              t              |  小写字母t   |
|  0111 0101  |    0165     |     117     |     0x75      |              u              |  小写字母u   |
|  0111 0110  |    0166     |     118     |     0x76      |              v              |  小写字母v   |
|  0111 0111  |    0167     |     119     |     0x77      |              w              |  小写字母w   |
|  0111 1000  |    0170     |     120     |     0x78      |              x              |  小写字母x   |
|  0111 1001  |    0171     |     121     |     0x79      |              y              |  小写字母y   |
|  0111 1010  |    0172     |     122     |     0x7A      |              z              |  小写字母z   |
|  0111 1011  |    0173     |     123     |     0x7B      |              {              |   开花括号   |
|  0111 1100  |    0174     |     124     |     0x7C      |             \|              |     垂线     |
|  0111 1101  |    0175     |     125     |     0x7D      |              }              |   闭花括号   |
|  0111 1110  |    0176     |     126     |     0x7E      |              ~              |    波浪号    |
|  0111 1111  |    0177     |     127     |     0x7F      |        DEL (delete)         |     删除     |

字符串是按位比较，也就是一位位进行对比，只要有一位大，那么整体就大。

```python
"""
    字符串大小比较
"""

# abc比较 abd
print("abc" < "abd")  # True

# a 比较 ab
print("a" < "ab")  # True

# a 比较 A
print("a" < "A")  # False

# key1比较key2
print("key1" < "key2")  # True
```



## 迭代器

### iter()函数

**iter()** 函数用来生成迭代器，实现了 `__iter__()` 和 `__next__()` 方法的对象，用于遍历可迭代对象（如列表、字典、文件等）。迭代器会记住当前遍历的位置，每次调用 `next()` 返回下一个值，直到结束（抛出 `StopIteration` 异常）。

```python
iter(object[, sentinel])
```

- object -- 支持迭代的集合对象。
- sentinel -- 如果传递了第二个参数，则参数 object 必须是一个可调用的对象（如，函数），此时，iter 创建了一个迭代器对象，每次调用这个迭代器对象的__next__()方法时，都会调用 object。

```python
my_list = [1, 2, 3]
my_iter = iter(my_list)  # 创建迭代器

print(next(my_iter))  # 输出: 1
print(next(my_iter))  # 输出: 2
print(next(my_iter))  # 输出: 3
print(next(my_iter))  # 抛出 StopIteration 异常

# 循环迭代器
for i in my_iter:
     print(i)
```

自定义一个返回平方数的迭代器

迭代器需要实现两个核心方法：

- `__iter__()`：返回迭代器自身。
- `__next__()`：返回下一个元素，若结束则抛出 `StopIteration`

```python
class SquareIterator:
    def __init__(self, max_num):
        self.max_num = max_num
        self.current = 0

    def __iter__(self):
        return self  # 返回迭代器自身

    def __next__(self):
        if self.current >= self.max_num:
            raise StopIteration
        result = self.current ** 2
        self.current += 1
        return result

# 使用自定义迭代器
squares = SquareIterator(3)
print(next(squares))  # 输出: 0 (0²)
print(next(squares))  # 输出: 1 (1²)
print(next(squares))  # 输出: 4 (2²)
```

### itertools模块

Python的itertools模块是标准库的一部分，提供了一组高效的迭代器工具函数，用于处理可迭代对象。这些函数专为迭代操作设计，支持函数式编程，适用于生成序列、组合数据、过滤元素等场景。itertools的实现基于C语言，性能高且内存效率优异，尤其适合处理大型数据集或需要复杂迭代逻辑的任务。

- **官方文档**：https://docs.python.org/3/library/itertools.html
- **Python 标准库**：`itertools` 模块的源代码可在 Python 源码中查看。

**itertools 模块的作用**

- **高效迭代**：提供快速、内存高效的工具，替代手动循环或列表推导式。
- **序列生成**：生成无穷序列、笛卡尔积、排列组合等。
- **数据处理**：支持过滤、分组、合并、切片等操作。
- **函数式编程**：与高阶函数（如 `map`、`filter`）结合，简化代码。

**核心功能与分类**

`itertools` 的函数可分为以下几类：

1. **无穷迭代器**：生成无限序列。
2. **有限迭代器**：处理有限序列的组合、排列等。
3. **组合工具**：生成笛卡尔积、排列、组合等。
4. **其他工具**：分组、切片、合并等。

**无穷迭代器**

这些函数生成无限序列，适合与 `break` 或其他终止条件结合使用。

| 函数                         | 描述                                          | 示例                                             |
| ---------------------------- | --------------------------------------------- | ------------------------------------------------ |
| `count(start=0, step=1)`     | 从 `start` 开始，按 `step` 递增，生成无穷序列 | `itertools.count(10, 2)` → 10, 12, 14, ...       |
| `cycle(iterable)`            | 循环重复可迭代对象中的元素                    | `itertools.cycle('ABC')` → A, B, C, A, B, C, ... |
| `repeat(object, times=None)` | 重复指定对象，无限次或指定次数                | `itertools.repeat(5, 3)` → 5, 5, 5               |

**示例**：

```python
import itertools

# count：生成偶数
for num in itertools.count(0, 2):
    if num > 6:
        break
    print(num)  # 输出: 0, 2, 4, 6

# cycle：循环输出
counter = 0
for char in itertools.cycle('ABC'):
    if counter >= 6:
        break
    print(char, end=' ')  # 输出: A B C A B C
    counter += 1

# repeat：重复元素
print(list(itertools.repeat(5, 3)))  # 输出: [5, 5, 5]
```

**有限迭代器**

这些函数从可迭代对象生成有限序列，常用于数据处理。

| 函数                                                    | 描述                                       | 示例                                                         |
| ------------------------------------------------------- | ------------------------------------------ | ------------------------------------------------------------ |
| `accumulate(iterable, func=operator.add, initial=None)` | 计算累计结果（Python 3.8+ 支持 `initial`） | `itertools.accumulate([1, 2, 3])` → 1, 3, 6                  |
| `chain(*iterables)`                                     | 将多个可迭代对象连接为单个迭代器           | `itertools.chain([1, 2], [3, 4])` → 1, 2, 3, 4               |
| `chain.from_iterable(iterable)`                         | 从可迭代对象中逐一解包并连接               | `itertools.chain.from_iterable([[1, 2], [3, 4]])` → 1, 2, 3, 4 |
| `compress(data, selectors)`                             | 根据布尔选择器过滤元素                     | `itertools.compress('ABC', [1, 0, 1])` → A, C                |
| `dropwhile(predicate, iterable)`                        | 丢弃满足条件的开头元素，之后保留所有       | `itertools.dropwhile(lambda x: x < 3, [1, 2, 3, 4])` → 3, 4  |
| `takewhile(predicate, iterable)`                        | 保留满足条件的开头元素，之后丢弃           | `itertools.takewhile(lambda x: x < 3, [1, 2, 3, 4])` → 1, 2  |
| `filterfalse(predicate, iterable)`                      | 保留不满足条件的元素                       | `itertools.filterfalse(lambda x: x % 2, [1, 2, 3, 4])` → 2, 4 |
| `groupby(iterable, key=None)`                           | 按键函数分组（需预排序）                   | `itertools.groupby('AABBC')` → (A, AA), (B, BB), (C, C)      |
| `islice(iterable, start, stop, step)`                   | 对可迭代对象切片                           | `itertools.islice('ABCDEFG', 2, 5)` → C, D, E                |
| `starmap(function, iterable)`                           | 类似 `map`，但输入为元组                   | `itertools.starmap(pow, [(2, 3), (3, 2)])` → 8, 9            |
| `tee(iterable, n=2)`                                    | 创建 n 个独立迭代器副本                    | `itertools.tee([1, 2, 3], 2)` → iter1, iter2                 |
| `zip_longest(*iterables, fillvalue=None)`               | 按最长可迭代对象配对，填充缺失值           |                                                              |

**示例**：

```python
import itertools
import operator

# accumulate：累加
print(list(itertools.accumulate([1, 2, 3, 4])))  # 输出: [1, 3, 6, 10]
print(list(itertools.accumulate([1, 2, 3, 4], operator.mul)))  # 输出: [1, 2, 6, 24]

# chain：连接
print(list(itertools.chain([1, 2], [3, 4])))  # 输出: [1, 2, 3, 4]

# compress：选择
print(list(itertools.compress('ABCDE', [1, 0, 1, 0, 1])))  # 输出: ['A', 'C', 'E']

# groupby：分组
data = sorted('AABBCC')
for key, group in itertools.groupby(data):
    print(key, list(group))  # 输出: A ['A', 'A'], B ['B', 'B'], C ['C', 'C']
```

**组合工具**

这些函数生成排列、组合或笛卡尔积，常用于数学或算法问题。

| 函数                                         | 描述                   | 示例                                                         |
| -------------------------------------------- | ---------------------- | ------------------------------------------------------------ |
| `product(*iterables, repeat=1)`              | 笛卡尔积，替代嵌套循环 | `itertools.product('AB', [1, 2])` → (A, 1), (A, 2), (B, 1), (B, 2)` |
| `permutations(iterable, r=None)`             | 有序排列（长度 r ）    | `itertools.permutations('ABC', 2)` → (A, B), (A, C), (B, A), (B, C), (C, A), (C, B)` |
| `combinations(iterable, r)`                  | 无序组合（长度 r ）    | `itertools.combinations('ABC', 2)` → (A, B), (A, C), (B, C)` |
| `combinations_with_replacement(iterable, r)` | 无序组合，允许重复     | `itertools.combinations_with_replacement('ABC', 2)` → (A, A), (A, B), (A, C), (B, B), (B, C), (C, C)` |

**示例**：

```python
import itertools

# product：笛卡尔积
print(list(itertools.product('AB', [1, 2])))  # 输出: [('A', 1), ('A', 2), ('B', 1), ('B', 2)]

# permutations：排列
print(list(itertools.permutations('ABC', 2)))  # 输出: [('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'C'), ('C', 'A'), ('C', 'B')]

# combinations：组合
print(list(itertools.combinations('ABC', 2)))  # 输出: [('A', 'B'), ('A', 'C'), ('B', 'C')]
```

**性能与特点**

- 惰性求值：itertools 函数返回迭代器，仅在需要时计算，节省内存。
- 高效实现：C 语言实现，性能优于 Python 循环或列表推导式。
- 内存效率：避免创建中间列表，适合处理大型数据集。
- 灵活性：可与其他高阶函数（如 map、filter）或 operator 模块结合。



## 枚举

**enumerate()**函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。

```python
enumerate(sequence, [start=0])
```

- sequence -- 一个序列、迭代器或其他支持迭代对象。
- start -- 下标起始位置。

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print(list(enumerate(seasons)))
print(list(enumerate(seasons, start=1))) # 下标从 1 开始
```

枚举在for循环中的应用

```python
fruits = ['apple', 'banana', 'cherry']

# 传统方式（需手动维护索引）
index = 0
for fruit in fruits:
    print(f"索引 {index}: {fruit}")
    index += 1

# 枚举方式（更简洁）
for index, fruit in enumerate(fruits):
    print(f"索引 {index}: {fruit}")
```

**总结对比**

| **特性**     | **迭代器（Iterator）**                 | **枚举（Enumerate）**                     |
| ------------ | -------------------------------------- | ----------------------------------------- |
| **核心作用** | 遍历可迭代对象，逐个返回元素           | 遍历可迭代对象，同时返回索引和元素        |
| **实现方式** | 实现 `__iter__()` 和 `__next__()` 方法 | 内置函数 `enumerate(iterable, start)`     |
| **适用场景** | 大数据集、惰性计算、自定义遍历逻辑     | 需要同时获取索引和元素的场景              |
| **示例**     | `iter([1, 2])` → 迭代器对象            | `enumerate(['a', 'b'])` → (0,'a'),(1,'b') |



## 推导式

在Python里，推导式是一种可以从一个数据序列构建另一个新的数据序列的语法结构。

Python 中有四种常见的推导式：

- 列表推导式
- 字典推导式
- 集合推导式
- 生成器表达式

列表推导式的作用是生成新的列表。其基本语法为：`[表达式 for 变量 in 可迭代对象 if 条件]`。

```python
# 生成一个包含 0 到 9 的平方的列表
squares = [x**2 for x in range(10)]
print(squares)  # 输出: [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
# 过滤出偶数的平方
squares_of_evens = [x**2 for x in range(10) if x % 2 == 0]
print(squares_of_evens) # 输出: [4 16, 36 64]
# 嵌套的列表推导式
nested_list = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
flattened_list = [x for sublist in nested_list for x in sublist]
print(flattened_list) # 输出: [1, 2, 3, 4, 5, 6, 7, 8, 9]
# 使用多个if子句,1-10中既是偶数又能被3整除的数字列表
multi_if = [x for x in range(1, 11) if x % 2 == 0 if x % 3 == 0]
print(multi_if) # 输出: [6, 10]
# 使用if-else条件,1-10中偶数位置的字符串为"Even"，奇数位置的字符串为"Odd"
if_else = ["Even" if x % 2 == 0 else "Odd" for x in range(1, 11)]
print(if_else) # 输出: ["Odd", "Even", "Odd", "Even", "Odd", "Even", "Odd", "Even", "Odd", "Even"]
# 多层for循环嵌套
pairs = [(x, y) for x in range(1, 4) for y in range(5, 8)]
print(pairs) # 输出: [(1, 5), (1, 6), (1, 7), (2, 5), (2, 6), (2, 7), (3, 5), (3, 6), (3, 7)]
# 同时使用多个for循环和if条件
pairs = [(x, y) for x in range(1, 4) if x % 2 == 1 for y in range(5, 8) if y % 2 == 0]
print(pairs) # 输出: [(1, 6), (3, 6)]
```

字典推导式能够创建新的字典。它的基本语法是：`{键表达式: 值表达式 for 变量 in 可迭代对象 if 条件}`。

```python
# 生成一个键为 0 到 4，值为其平方的字典
squares_dict = {x: x**2 for x in range(5)}
print(squares_dict)  # 输出: {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

集合推导式用于生成新的集合。基本语法为：`{表达式 for 变量 in 可迭代对象 if 条件}`。

```python
# 生成一个包含 0 到 4 的平方的集合（集合会自动去重）
squares_set = {x**2 for x in range(-2, 3)}
print(squares_set)  # 输出: {0, 1, 4}
```

生成器表达式会返回一个生成器对象。它的基本语法是：`(表达式 for 变量 in 可迭代对象 if 条件)`。

```python
# 创建一个生成器对象，生成 0 到 4 的平方
squares_generator = (x**2 for x in range(5))
print(squares_generator)  # 输出: <generator object <genexpr> at 0x...>
# 使用 next() 或循环来获取生成器中的值
print(next(squares_generator))  # 输出: 0
for num in squares_generator:
    print(num)  # 输出: 1, 4, 9, 16
```



# 函数进阶

## 函数的多返回值

如果一个函数有多个返回值，按照返回值的顺序，写对应顺序的多个变量接收即可，变量之间用逗号隔开，支持不同类型的数据return。

```python
"""
    函数的多返回值
"""

# 定义一个函数，返回多个值
def test_return():
    """
    函数的多返回值
    """
    return 1, "a", True

# 调用函数并接收多个返回值
a, b, c = test_return()
print(a)
print(b)
print(c)
```



## 函数的多种传参方式

使用方式上的不同，函数有4中常见参数使用方式：

- 位置参数
- 关键字参数
- 缺省参数
- 不定长参数

位置参数：调用函数时根据函数定义的参数位置来传递参数，传递的参数和定义的参数的顺序及个数必须一致

```python
# 位置参数,默认使用形式
def user_info(name, age, gender):
    print(f'您的名字是{name},年龄是{age},性别是{gender}')


user_info('TOM', 20, '男')
```

关键字参数：函数调用时通过"键=值"形式传递参数
作用：可以让函数更加清晰、容易使用，同时也清除了参数的顺序需求
函数调用时，如果有位置参数时，位置参数必须在关键字参数的前面，但关键字参数之间不存在先后顺序

```python
def user_info(name, age, gender):
	print(f'您的名字是{name},年龄是{age},性别是{gender}')
    
# 关键字参数
user_info(name="小明", age=20, gender="男")
# 可以不按照固定顺序
user_info(age=20, gender="男", name="小明")
# 可以和位置参数混用，位置参数必须在前，且匹配参数顺序
user_info("小明", age=20, gender="男")
```

缺省参数：缺省参数也叫默认参数，用于定义函数，为参数提供默认值，调用函数时可不传该默认参数的值（注意：所有位置参数必须出现在默认参数前，包括函数定义和调用）
作用：当调用函数时没有传递参数，就会使用默认是用缺省参数对应的值

```python
# 缺省参数(默认值)必须是最后一个参数才能设置，也可以都设置默认值
def user_info(name, age, gender='男'):
    print(f'您的名字是{name},年龄是{age},性别是{gender}')


user_info("小明", 20)
user_info("小美", 20, '女')
```

不定长参数：不定长参数也叫可变参数，用于不确定调用的时候会传递多少个参数（不传参也可以)的场景，
作用：当调用函数时不确定参数个数时，可以使用不定长参数

不定长参数的类型：

- 位置传递，传进的所有参数都会被args变量收集，它会根据传进参数的位置合并为一个元组（tuple)，args是元组类型，这就是位置传递
- 关键字传递，参数是"键=值"形式的形式的情况下，所有的"键=值"都会被kwargs接受，同时会根据"键=值"组成字典

```python
# 不定长-位置不定长，*号 传进的所有参数都会被args变量收集，它会根据传进参数的位置合并为一个元组（tuple)，args是元组类型，这就是位置传递,args是形式参数，可以由任意字符组成
def user_info(*args):
    """
    不定长-位置不定长，*号
    :param args: 可变参数
    """
    print(args, type(args))


user_info('小明')
user_info('小明', 20)
user_info('小明', 20, '男')


# 不定长-关键字不定长，**号 参数是"键=值"形式的形式的情况下，所有的"键=值"都会被kwargs接受，同时会根据"键=值"组成字典,kwargs是形式参数，可以由任意字符组成
def user_info(**kwargs):
    """
    不定长-关键字不定长，**号
    :param kwargs: 可变参数
    """
    print(kwargs, type(kwargs))


user_info(name="小明")
user_info(name="小明", age=20)
user_info(name="小明", age=20, gender="男")
```



## 匿名函数

### 函数作为参数传递

1.函数本身是可以作为参数，传入另一个函数中进行使用的。
2.将函数传入的作用在于：传入计算逻辑，而非传入数据。

```python
"""
    函数作为参数传递
"""

def add(x, y):
    """返回两个数的和"""
    return x + y

def subtract(x, y):
    """返回两个数的差"""
    return x - y

def calculate(func, x, y):
    """使用传入的函数计算结果"""
    return func(x, y)

# 测试函数作为参数传递
result1 = calculate(add, 5, 3)
result2 = calculate(subtract, 5, 3)
print(f"5 + 3 = {result1}")
print(f"5 - 3 = {result2}")
```

### lambda匿名函数

函数的定义中

- def关键字，可以定义带有名称的函数
- lambda关键字，可以定义匿名函数（无名称）

有名称的函数，可以基于名称**重复使用**。
无名称的匿名函数，只可**临时使用一次**。

匿名函数定义语法：

```python
lambda 参数列表:函数体(只能写一行代码)
```

- lambda是关键字，表示定义匿名函数
- 参数列表表示匿名函数的形式参数，如：x，y表示接收2个形式参数
- 函数体，就是函数的执行逻辑，要注意：只能写一行，无法写多行代码

```python
"""
    lambda匿名函数
"""


def calculate(func, x, y):
    """使用传入的函数计算结果"""
    return func(x, y)


# 测试lambda匿名函数 lambda 参数列表:函数体
result1 = calculate(lambda x, y: x + y, 5, 3)
result2 = calculate(lambda x, y: x - y, 5, 3)
print(f"5 + 3 = {result1}")
print(f"5 - 3 = {result2}")
```

## zip函数

`zip`函数能够把多个可迭代对象（像列表、元组）中的元素组合成一个个元组，最终返回一个迭代器。

```python
names = ['Alice', 'Bob', 'Charlie']
ages = [25, 30, 35]

zipped = zip(names, ages)
print(list(zipped))  # 输出：[('Alice', 25), ('Bob', 30), ('Charlie', 35)]
```

**常用场景**：同时遍历多个列表。

```python
for name, age in zip(names, ages):
    print(f"{name} is {age} years old.")
```

构建字典

```python
person_dict = dict(zip(names, ages))
print(person_dict)  # 输出：{'Alice': 25, 'Bob': 30, 'Charlie': 35}
```



## map函数

`map`函数会将指定的函数应用到可迭代对象的每一个元素上，然后返回一个迭代器。其语法格式为：`map(函数, 可迭代对象)`。

```python
def square(x):
    return x**2

numbers = [1, 2, 3, 4]
squared = map(square, numbers)
print(list(squared))  # 输出：[1, 4, 9, 16]
```

**常用场景**：结合`lambda`函数使用。

```python
names = ['Alice', 'Bob', 'Charlie']
upper_names = map(lambda x: x.upper(), names)
print(list(upper_names))  # 输出：['ALICE', 'BOB', 'CHARLIE']
```

对多个可迭代对象进行操作

```python
a = [1, 2, 3]
b = [4, 5, 6]
summed = map(lambda x, y: x + y, a, b)
print(list(summed))  # 输出：[5, 7, 9]
```

**总结**

- `zip`函数：用于组合多个可迭代对象。
- `lambda`函数：用于创建轻量级的匿名函数。
- `map`函数：用于对可迭代对象中的元素进行批量处理



## 内置函数

在Python中，内置函数是可以直接使用的工具，无需额外导入模块。

完整的内置函数列表可参考 Python 官方文档：https://docs.python.org/3/library/functions.html

### 基础数据类型转换

- **`int(x)`**：将 `x` 转换为整数。
- **`float(x)`**：将 `x` 转换为浮点数。
- **`str(x)`**：将 `x` 转换为字符串。
- **`bool(x)`**：将 `x` 转换为布尔值（`True` 或 `False`）。
- **`list(x)`**：将 `x` 转换为列表。
- **`tuple(x)`**：将 `x` 转换为元组。
- **`dict(x)`**：将 `x` 转换为字典。
- **`set(x)`**：将 `x` 转换为集合。

### 数学运算

- **`abs(x)`**：返回 `x` 的绝对值。
- **`round(x, n)`**：将 `x` 四舍五入到 `n` 位小数（默认 `n=0`）。
- **`max(iterable)`**：返回可迭代对象中的最大值。
- **`min(iterable)`**：返回可迭代对象中的最小值。
- **`sum(iterable)`**：返回可迭代对象中所有元素的和。
- **`pow(x, y)`**：返回 `x` 的 `y` 次幂（等价于 `x**y`）。

### 序列操作

- **`len(iterable)`**：返回可迭代对象的长度。
- **`sorted(iterable, key=None, reverse=False)`**：返回一个新的已排序列表。
- **`reversed(seq)`**：返回一个反向迭代器。
- **`range(start, stop, step)`**：生成一个不可变的整数序列。
- **`enumerate(iterable, start=0)`**：返回一个枚举对象（索引 - 值对）。
- **`zip(\*iterables)`**：将多个可迭代对象的元素打包成元组。

###  输入输出

- **`print(\*objects, sep=' ', end='\n')`**：打印对象到标准输出。
- **`input(prompt)`**：从标准输入读取一行文本。
- **`open(file, mode='r')`**：打开文件并返回文件对象。

### 类型检查与帮助

- **`type(x)`**：返回 `x` 的类型。
- **`isinstance(obj, classinfo)`**：检查 `obj` 是否是 `classinfo` 的实例。
- **`help([obj])`**：启动交互式帮助系统（或显示对象的文档）。
- **`dir([obj])`**：返回对象的所有属性和方法名称列表。

### 高阶函数

- **`map(func, iterable)`**：对可迭代对象的每个元素应用函数 `func`。
- **`filter(func, iterable)`**：过滤可迭代对象中满足条件的元素。
- **`reduce(func, iterable[, initial])`**：（需从 `functools` 导入）累积计算可迭代对象的元素。

### 其他常用函数

- **`id(obj)`**：返回对象的唯一标识符（内存地址）。
- **`hash(obj)`**：返回对象的哈希值（如果可哈希）。
- **`chr(i)`**：返回 Unicode 码点为 `i` 的字符。
- **`ord(c)`**：返回字符 `c` 的 Unicode 码点。
- **`bin(x)`**：返回整数 `x` 的二进制字符串表示。
- **`hex(x)`**：返回整数 `x` 的十六进制字符串表示。
- **`oct(x)`**：返回整数 `x` 的八进制字符串表示。







# 文件操作

## 文件编码

编码技术即：翻译的规则，记录了如何将内容翻译成二进制，以及如何将二进制翻译回可识别内容。

计算机中有许多可用编码：UTF-8、GBK、Big5等，不同的编码，将内容翻译成二进制也是不同的。

计算机只认识0和1，所以需要将内容翻译成0和1才能保存在计算机中。

同时也需要编码，将计算机保存的0和1，反向翻译回可以识别的内容。



## 文件读取

对文件的基本操作，大概可以分为三个步骤（简称文件操作三步走）：

- 打开文件
- 读写文件
- 关闭文件

在Python，使用open函数，可以打开一个已经存在的文件，或者创建一个新文件，语法如下

```python
file = open(name, mode, encoding)
```

name：是要打开的目标文件名的字符串（可以包含文件所在的具体路径)
mode：设置打开文件的模式（访问模式）：只读、写入、追加等
encoding：编码格式（推荐使用UTF-8）

文件打开模式：

| 模式 | 描述                                                         |
| ---- | ------------------------------------------------------------ |
| r    | 以只读方式打开文件。文件的指针将会放在文件的开头。文件必须存在，否则会抛出 `FileNotFoundError` 错误 |
| w    | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，原有内容会被删除，如果该文件不存在，创建新文件 |
| a    | 打开一个文件用于追加。如果该文件已存在，新的内容将会被写入到已有内容之后，如果该文件不存在，创建新文件进行写入 |
| x    | 创建新文件并打开。如果文件已存在，则抛出 `FileExistsError` 错误 |
| b    | 二进制模式。这是与其他模式配合使用的，用于读取或写入二进制文件，如图片、音频等 |
| t    | 文本模式（默认模式）。用于文本文件的读取或写入。可以与其他模式（如 `r`、`w` 等）配合使用，但通常不需要显式指定，因为它是默认的 |
| rb   | 只读二进制模式，适用于读取二进制文件（例如图片、音频文件等） |
| wb   | 写入二进制模式，适用于将数据写入二进制文件                   |
| ab   | 追加二进制模式，适用于将数据以二进制格式追加到文件末尾       |
| r+   | 读写模式。文件必须存在，可以同时读取和写入文件。             |
| w+   | 读写模式。文件存在时覆盖内容，不存在时创建新文件。           |
| a+   | 追加读写模式。可以在文件末尾添加内容，也可以读取文件内容。如果文件不存在，创建新文件 |
| x+   | 创建并打开文件进行读写。文件已存在时，抛出 `FileExistsError` 错误 |
| b+   | 结合二进制和读写模式使用。适用于需要二进制读写操作的文件     |
| rb+  | 以二进制模式读写文件。适用于需要同时读取和写入二进制文件     |
| wt+  | 以文本模式读写文件。适用于需要同时读取和写入文本文件         |

常用操作：

| 操作                                | 功能                                    |
| ----------------------------------- | --------------------------------------- |
| 文件对象 = open(file,mode.encoding) | 打开文件获取文件对象                    |
| 文件对象.read(num)                  | 读取指定长度字节，默认读取文件全部内容  |
| 文件对象.readline()                 | 读取一行                                |
| 文件对象.readlines()                | 读取全部行，返回内容列表                |
| for line in 文件对象                | for循环文件行，一次循环得到一行数据     |
| 文件对象.close()                    | 关闭文件对象                            |
| with open as file                   | 通过with open语法打开文件，可以自动关闭 |

```python
"""
    文件的读取
"""

# 打开文件
file = open("1.txt", "r", encoding="utf-8")
print(type(file))

# 读取文件-read()
# print(file.read(5))
# print(file.read())

# 读取文件-readLines(),读取文件并返回一个列表
# print(file.readlines(), type(file.readlines()))

# 读取文件-readline(O),一次读取一行,逐行读取
# print(f"第一行的数据：{file.readline()}")
# print(f"第二行的数据：{file.readline()}")

# for循环读取文件行
for i in file:
    print(i)

# 文件的关闭
# 最后通过close，关闭文件对象，也就是关闭对文件的占用
# 如果不调用close，同时程序没有停止运行，那么这个文件将一直被Python程序占用。
file.close()

# with open语法操作文件
# 通过在with open的语句块中对文件进行操作
# 可以在操作完成后自动关闭close文件，避免遗忘掉close方法
with open("1.txt", "r", encoding="utf-8") as file:
    for i in file:
        print(i)


# 案例：统计文本中的字数
with open("1.txt", "r", encoding="utf-8") as file:
    content = file.read()
    count = 0
    for i in content.strip():
        count += 1
    print(f"文本中的字数为：{count}")
    print(f"文本中hello出现的次数为：{content.count('hello')}")
```



## 文件写入

对文件的基本操作，大概可以分为三个步骤（简称文件操作三步走）：

- 打开文件
- 读写文件
- 关闭文件

1. 写入文件使用open函数的"w"模式进行写入
2. 写入的方法有：
   wirte()，写入内容
   flush()，刷新内容到硬盘中
3. 注意事项：
   w模式，文件不存在，会创建新文件
   w模式，文件存在，会清空原有内容
   close()方法，带有flush()方法的功能

```python
"""
    文件的写入
"""

# 打开文件，不存在的文件
# f = open("2.txt", "w", encoding="utf-8")
# write写入
# f.write("Hello, World!")

# flush刷新
# f.flush()

# close关闭,内置了flush功能，如果调用了close方法，可以不调用flush方法
# f.close()

# 打开一个存在的文件
f = open("2.txt", "w", encoding="utf-8")

# write写入、flush刷新
f.write("Hello, 木芒果!")
f.flush()

# close关闭
f.close()
```



## 文件追加写入

1. 追加写入文件使用open函数的"a"模式进行写入
2. 追加写入的方法有（和w模式一致）：
   wirte()，写入内容
   flush()，刷新内容到硬盘中
3. 注意事项：
   a模式，文件不存在，会创建新文件
   a模式，文件存在，会在原有内容后面继续写入
   可以使用"\n"来写出换行符

```python
"""
    文件的追加写入
"""

# 打开文件，不存在的文件
# f = open("3.txt", "a", encoding="utf-8")  # 'a'模式表示追加写入

# write写入
# f.write("Hello, World!")

# flush刷新
# f.flush()

# close关闭
# f.close()

# 打开一个存在的文件
f = open("3.txt", "a", encoding="utf-8")  # 'a'模式表示追加写入

# write写入、flush刷新
f.write("Hello, 木芒果!\n")
f.flush()

# close关闭
f.close()
```



## 案例

```py
"""
    需求：有一份账单文件，记录了消费收入的具体记录bill.txt
    name,date,money,type,remarks
    周杰轮,2022-01-01,100000,消费,正式
    周杰轮,2022-01-02,300000,收入,正式
    周杰轮,2022-01-03,100000,消费,测试
    林俊节,2022-01-01,300000,收入,正式
    林俊节,2022-01-02,100000,消费,测试
    林俊节,2022-01-03,100000,消费,正式
    林俊节,2022-01-04,100000,消费,测试
    林俊节,2022-01-05,500000,收入,正式
    张学油,2022-01-01,100000,消费,正式
    张学油,2022-01-02,500000,收入,正式
    张学油,2022-01-03,900000,收入,测试
    王力鸿,2022-01-01,500000,消费,正式
    王力鸿,2022-01-02,300000,消费,测试
    王力鸿,2022-01-03,950000,收入,正式
    刘德滑,2022-01-01,300000,消费,测试
    刘德滑,2022-01-02,100000,消费,正式
    刘德滑,2022-01-03,300000,消费,正式
    读取文件
    将文件写出到bill.txt.bak文件作为备份
    同时，将文件内标记为测试的数据行丢弃
"""

with open("bill.txt", "r", encoding="utf-8") as f:
    for bill in f:
        # if bill.split(",")[4] =="测试":
        if bill.count("测试") > 0:
            continue
        with open("bill.txt.bak", "a", encoding="utf-8") as f_bak:
            f_bak.write(bill)
```



# 异常

## 什么是异常？

当检测到一个错误时，Python解释器就无法继续执行了，反而出现了一些错误的提示，这就是所谓的"异常"，也就是我们常说的BUG

BUG单词的诞生：

早期计算机采用大量继电器工作，马克二型计算机就是这样的。
1945年9月9日，下午三点，马克二型计算机无法正常工作了，技术人员试了很多办法，最后定位到第70号继电器出错。负责人哈珀观察这个出错的继电器，
发现一只飞蛾躺在中间，已经被继电器打死。她小心地用摄子将蛾子夹出来，用透明胶布帖到“事件记录本”中，并注明“第一个发现虫子的实例。”自此之
后，引发软件失效的缺陷，便被称为Bug。



## 捕获异常

捕获异常的作用在于：提前假设某处会出现异常，做好提前准备，当真的出现异常的时候，可以有后续手段。

```python
"""
    捕获异常
    基础语法：
    try:
		可能发生错误的代码
	except[异常 as 别名]:
		如果出现异常执行的代码
	[else]:
	    没有异常发生执行的代码
	[finally]:
	    不管是否发生异常，都会执行的代码
"""

# 基本捕获语法
try:
    file = open("abc.txt", "r", encoding="utf-8")
except:
    print("出现异常了，因为文件不存在，我将open的模式，改为w模式去打开")
    file = open("abc.txt", "w", encoding="utf-8")

# 捕获指定异常
try:
    print(name)
except NameError as e:
    print(e)
    print("出现了变量未定义的异常，异常信息：", e)

# 捕获多个异常
try:
    # print(name)
    print(10 / 0)
except (NameError, ZeroDivisionError) as e:
    print(e)
    print("出现了变量未定义或除以零的异常，异常信息：", e)

# 捕获所有异常 Exception
try:
    # print(name)
    # print(10 / 0)
    print("hello")
except Exception as e:
    print(e)
    print("出现了未知异常，异常信息：", e)


# else、finally语句块
try:
    file = open("abc123.txt", "r", encoding="utf-8")
except:
    print("出现异常了，因为文件不存在，我将open的模式，改为w模式去打开")
    file = open("abc123.txt", "w", encoding="utf-8")
else:
    print("没有异常发生，执行else语句块")
finally:
    print("无论是否发生异常，都会执行finally语句块")
    file.close()
```



## 抛出异常

手动抛出异常可以使用raise可以抛出各种预定异常，即使程序在运行时根本不会引发该异常。

```python
"""
    手动抛出异常
    基础语法：
    raise 异常名("异常信息")
"""


try:
    if len(input("请输入名字(小于10个字符)：")) > 10:
        # 使用raise关键词手动抛出异常
        raise Exception("名字不能超过10个字符")
    else:
        print("名字合法")
except Exception as e:
    print(f"发生异常：{e}")
```

手动抛出异常还可以使用assert语句是简化的raise语句，它引发异常的前提是其后面的条件测试为假，assert语句一般用于在程序开发时测试代码的有效性

```python
"""
    assert语句
    基础语法：
    assert 条件, "异常信息"
"""
name = input("请输入名字(小于10个字符)：")
# len(name) < 10会返回True/False，如果是False，则抛出异常，如果是True，则继续执行后面的代码
assert len(name) < 10, "名字不能超过10个字符"
print("名字合法")
```



## 异常的传递

异常是具有传递性的

```python
"""
    异常的传递
    当函数func01中发生异常，并且没有捕获处理这个异常的时候，异常会传递到函数func02，当func02也没有捕获处理这个异常的时候main函数会捕获这个异常，这就是异常的传递性
    当所有函数都没有捕获异常的时候，程序就会报错
"""


def func01():
    # 异常在func()1中没有被捕获
    print("这是func()1开始")
    num = 1 / 0
    print("这是func()1结束")


# 异常在funco2中没有被捕获
def func02():
    print("这是func02开始")
    func01()
    print("这是func02结束")


# 异常在mian中被捕获
def main():
    try:
        func02()
    except Exception as e:
        print(e)

# 程序入口
main()
```



## 自定义异常类

在Python中定义异常类不用从基础完全自己定义，只要通过继承Exception类来创建自己的异常类。

如果需要异常类带有一定的提示信息，也可以重载`__str__和__init__`这两个方法。

```python
"""
    自定义异常
    1. 自定义异常类需要继承Exception类
    2. 自定义异常类可以添加自己的属性和方法
    3. 在需要抛出异常的地方，使用raise关键词手动抛出自定义异常类
"""


# 自定义字符串长度异常类
class StringLengthException(Exception):
    def __init__(self):
        self.msg = "字符串长度异常"

    def __str__(self):
        return self.msg


name = input("请输入名字(小于10个字符)：")
# 使用自定义异常类进行异常处理
try:
    if len(name) > 10:
        raise StringLengthException()
    else:
        print("名字合法")
except Exception as e:
    print(f"发生异常：{e}")
```



# Python的模块

## 什么是模块？

Python模块(Module)，是一个Python文件，以.py结尾，模块能定义函数，类和变量，模块里也能包含可执行的代码

模块的作用：
python中有很多各种不同的模块，每一个模块都可以帮助我们快速的实现一些功能，比如实现和时间相关的功能就可以使用time模块我们可以认为一个模块就是一个工具包，每一个工具包中都有各种不同的工具供我们使用进而实现各种不同的功能。

大白话：模块就是一个Python文件，里面有类、函数、变量等，我们可以拿过来用（导入模块去使用）

模块的导入一般写在代码文件的开头位置

## 导入模块

模块在使用前需要先导入导入的语法如下：

```python
[from 模块名] import [模块 | 类 | 变量 | 函数 | *] [as别名]
```

常用的组合形式如：

- import 模块名
- from 模块名 import 类、变量、方法等
- from 模块名 import *
- import 模块名 as 别名
- from 模块名 import 功能名 as 别名

```python
"""
    导入模块
"""

# 使用import导入time模块使用sleep功能（函数）
# import time # 导入Python内置的time模块(time.py这个代码文件)
# print("你好")
# time.sleep(1) # 调用time模块中的sleep函数，暂停1秒
# print("我是木芒果")

# 使用from导入time的sleep功能（函数）
# from time import sleep # 从time模块中导入sleep函数
# print("你好")
# sleep(1) # 调用time模块中的sleep函数，暂停1秒
# print("我是木芒果")

# 使用 * 导入time模块的全部功能
# from time import *  # 从time模块中导入全部功能
# print("你好")
# sleep(1)  # 调用time模块中的sleep函数，暂停1秒
# print("我是木芒果")

# 使用as给特定功能加上别名
# import time as t # 导入time模块，并给它起一个别名t
# print("你好")
# t.sleep(1)
# print("我是木芒果")

from time import sleep as s  # 从time模块中导入sleep函数，并给它起一个别名s
print("你好")
s(1)  # 调用time模块中的sleep函数，暂停1秒
print("我是木芒果")
```



## 自定义模块

Python中已经帮我们实现了很多的模块，不过有时候我们需要一些个性化的模块，这里就可以通过自定义模块实现，也就是自己制作一个模块

新建一个Python文件，命名为my_module.py，并定义test函数

my_module.py

```python
__all__ = ['testA'] # 用于控制从模块中导入的内容,例如通过 * 的方式导入，只能导入被__all__声明的方法：from my_module import *


def test(a, b):
    return a + b


def testA():
    print("testA")


def testB():
    print("testB")


print(__name__)
if __name__ == '__main__':
    print(test(1, 2))
```

main.py

```python
"""
    自定义模块
"""

# 导入自定义模块使用
# import my_module
#
# result = my_module.test(1, 2)
# print(result)

# from my_module import test
#
# result = test(1, 2)
# print(result)

# 导入不同模块的同名功能
# from my_module import test
# from my_module2 import test
#
# result = test(1, 2)  # 来自 my_module2
# print(result)

# __main__变量
# from my_module import test
#
# result = test(1, 2)
# print(result)

# __all__变量
from my_module import *
result = testA()  # 只能访问被__all__声明的方法
print(result)
testB() # 不能访问被__all__声明之外的方法
```

1.如何自定义模块并导入?
在Python代码文件中正常写代码即可，通过import、from关键字和导入Python内置模块一样导入即可使用。

2._main_变量的功能是?
if __name__ == '__main__'表示，只有当程序是直接执行的才会进入
if内部，如果是被导入的，则if无法进入

3.注意事项
不同模块，同名的功能，如果都被导入，那么后导入的会覆盖先导入的



# Python的包

基于Python模块，我们可以在编写代码的时候，导入许多外部代码来丰富功能。
但是，如果Python的模块太多了，就可能造成一定的混乱，那么如何管理呢？
通过Python包的功能来管理。

## 什么是Python包？

从物理上看，包就是一个文件夹，在该文件夹下包含了一个_init_.py文件，该文件夹可用于包含多个模块文件，__init__.py存在这个文件夹内才能代表这是一个包
从逻辑上看，包的本质依然是模块

## 自定义Python包

1.通过Pycharm创建，右键项目名->New->Python Package->输入包名`my_package`，Pycharm就会自动创建my_package文件夹以及__init__文件用于标识包

__init__.py

```python
__all__ = ['my_module1']
```

2.可以在包内创建各种模块，在`my_package`包上右键新建Python File并命名为`my_module1`和`my_module2`，这样就创建好两个模块，并属于`my_package`包

my_module1

```python
"""
    演示自定义模块1
"""


def info_print1():
    print("我是my_module1.py中的info_print1函数")
```

my_module2

```python
"""
    演示自定义模块2
"""


def info_print2():
    print("我是my_module2.py中的info_print2函数")
```

main.py

```python
"""
    导入自定义包
"""

# 导入自定义包中的模块
# import my_package.my_module1
# import my_package.my_module2

# 调用模块中的函数
# my_package.my_module1.info_print1()
# my_package.my_module2.info_print2()

# 使用 from ... import ... 的方式导入模块
# from my_package import my_module1
# from my_package import my_module2
#
# my_module1.info_print1()
# my_module2.info_print2()

# 使用 from ... import ... 的方式导入指定函数
# from my_package.my_module1 import info_print1
# from my_package.my_module2 import info_print2

# 调用导入的函数
# info_print1()
# info_print2()

# 通过 __all___ 变量，控制import *
# from my_package import *
# 调用导入的函数
# my_module1.info_print1()
# my_module2.info_print2() # 注意：my_module2没有被导入，因为在my_package的__init__.py中没有声明 NameError: name 'my_module2' is not defined. Did you mean: 'my_module1'?

# 这样不使用 * 导入是可以的
from my_package import my_module1
from my_package import my_module2

my_module1.info_print1()
my_module2.info_print2()
```



## 安装第三方包

什么是第三方包？

包可以包含一堆的Python模块，而每个模块又内含许多的功能。一个包，就是一堆同类型功能的集合体。

在Python程序的生态中，有许多非常多的第三方包（非Python官方），可以极大的帮助我们提高开发效率，如：

- 科学计算中常用的：numpy包
- 数据分析中常用的：pandas包
- 大数据计算中常用的：pyspark、apache-flink包
- 图形可视化常用的：matplotlib、pyecharts
- 人工智能常用的：tensorflow

这些第三方的包，极大的丰富了Python的生态，提高了开发效率

但是由于是第三方，所以Python没有内置，所以需要安装它们才可以导入使用

第三方包的安装非常简单，需要使用Python内置的pip程序，通过输入pip install 第三方包名，即可完成包的安装

```shell
# 在cmd命令中通过pip安装numpy包
pip install numpy
```

由于pip是连接的国外的网站进行包的下载，所以有的时候会速度很慢。
我们可以通过如下命令，让其连接国内的网站进行包的安装：

```shell
pip install 包名称 -i https://pypi.tuna.tsinghua.edu.cn/simple
```

https://pypi.tuna.tsinghua.edu.cn/simple是清华大学提供的一个网站，可供pip程序下载第三方包



## 配置第三方包下载源

查看当前源

```shell
pip config get global.index-url
```

临时变更源

```shell
pip install 包名称 -i https://pypi.tuna.tsinghua.edu.cn/simple
```

永久变更源(任选一个即可)

```shell
# 清华
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

# 百度
pip config set global.index-url https://mirror.baidu.com/pypi/simple

# 腾讯
pip config set global.index-url https://mirrors.cloud.tencent.com/pypi/simple

# 中国科学技术大学开源软件镜像站
pip config set global.index-url https://mirrors.ustc.edu.cn/pypi/web/simple

# 官方镜像源
pip config set global.index-url https://pypi.org/simple
```

# 面向对象

## 初始对象

在程序中简单使用变量来记录学生信息

```python
# 使用字典
student_1 = {
    "姓名"："周杰轮",
    "性别"："男",
    "国籍"："中国",
    "籍贯"："台湾省",
    "年龄"：33
}

# 使用简单的字符串
student_2 = "我叫林军杰，今年31岁，男的，来自中国山东省"

# 使用列表
student_3 = [
    "邓紫旗"，
    "中国"，
    "北京市"，
    26，
    "女"
]
```

在程序中是可以做到和生活中那样，设计表格、生产表格、填写表格的组织形式的。

1.在程序中设计表格，称之为：设计类（class）

```python
class Student:
	name = None #记录学生姓名
```

2.在程序中打印生产表格，称之为：创建对象

```python
# 基于类创建对象
stu_1 = Student()
stu_2 = Student()
```

3.在程序中填写表格，称之为：对象属性赋值

```python
stu_1.name="周杰轮" # 为学生1对象赋予名称属性值
stu_2.name="林军杰" # 为学生2对象赋予名称属性值
```

```python
"""
    初始对象
"""


# 1.设计一个类（类比生活中：设计一张登记表）
class Student:
    name = None,  # 姓名
    gender = None,  # 性别
    nationality = None,  # 国籍
    native_place = None,  # 籍贯
    age = None,  # 年龄


# 2.创建一个对象（类比生活中：打印一张登记表）
student1 = Student()

# 3.对象属性进行赋值（类比生活中：填写表单）
student1.name = "张三"
student1.gender = "男"
student1.nationality = "中国"
student1.native_place = "北京"
student1.age = 20

# 4.获取对象中记录的信息
print(f"姓名:{student1.name}")
print(f"性别:{student1.gender}")
print(f"国籍:{student1.nationality}")
print(f"籍贯:{student1.native_place}")
print(f"年龄:{student1.age}")
```



## 成员方法

一个完整的类包括：类名、属性、行为

类的使用语法：

```python
class 类名称: #class是关键字，表示要定义类了
	类的属性 # 类的属性，即定义在类中的变量（成员变量）
	类的行为 # 类的行为，即定义在类中的函数（成员方法）
# 创建类对象的语法：
对象 = 类名称()
```

写在类中定义的属性（变量），我们称之为：成员变量

写在类中定义的行为（函数），我们称之为：成员方法

在类中定义成员方法和定义函数基本一致，但仍有细微区别：

```python
def 方法名(self,形参1,·····,形参N):
	方法体
```

在方法定义的参数列表中，有一个：self关键字

**self关键字是成员方法定义的时候，必须填写的。**

- 它用来表示类对象自身的意思
- 当我们使用类对象调用方法的是，self会自动被python传入
- **在方法内部，想要访问类的成员变量，必须使用self**

```python
"""
    成员方法
"""


class Student:
    name = None

    # 定义成员方法必须要有self参数，这个参数指向调用该方法的实例对象
    def say_hello(self):
        # 通过self访问实例对象的name属性
        print(f"大家好，我是{self.name}，很高兴认识大家！")

    # 定义另一个成员方法，带有参数
    def say_hello2(self, msg):
        print(f"大家好，我是{self.name}，{msg}")


# 创建类对象
student1 = Student()
# 给对象的属性赋值
student1.name = "木芒果"
# 调用成员方法
student1.say_hello()

# 创建另一个类对象
student2 = Student()
# 给对象的属性赋值
student2.name = "张三"
# 实际调用带有参数成员方法时，可以不用管self参数，直接传入其他参数
student2.say_hello2("很高兴认识你们！")
```



## 类和对象

基于类创建对象的语法：对象名 = 类名称()

类只是一种程序内的"设计图纸"，需要基于图纸生产实体（对象），才能正常工作这种套路，称之为：**面向对象编程**

面向对象编程就是设计类，基于类创建对象，由对象做具体的工作

```python
"""
    类和对象
"""


# 设计一个闹钟类
class Clock:
    id = None
    price = None

    def run(self):
        print(f"闹钟响铃了！ID: {self.id}, 价格: {self.price}")
        import winsound
        # 通过winsound模块发出响铃声音,2000(hz)表示频率，3000(ms)表示持续时间
        winsound.Beep(2000,3000)

# 基于类创建对象
c1 = Clock()
c1.id = 1
c1.price = 100
# 调用响铃方法
c1.run()

# 通过类创建对象
c2 = Clock()
c2.id = 2
c2.price = 200
# 调用响铃方法
c2.run()
```



## 构造方法

如何在类创建时将成员变量赋值呢？需要使用构造方法： `__init__()`

Python类可以使用：`__init__()`方法，称之为构造方法。

- 在创建类对象的时候，**会自动执行**。
- 在创建类对象的时候，**将传入参数自动传递给init方法使用**。

```python
"""
    构造方法
    使用构造方法对成员变量进行赋值
"""

class Student:
    name = None
    age = None
    tel = None

    # __init__方法，即构造方法，在创建对象时自动调用，它也是需要self参数的,并且需要通过self来访问类的成员变量
    def __init__(self, name, age, tel):
        """
        构造方法，通过构造方法对成员变量进行赋值
        :param name: 姓名
        :param age: 年龄
        :param tel: 电话
        """
        self.name = name
        self.age = age
        self.tel = tel
        print("构造方法被调用,类创建成功!")


student = Student("张三", 18, "12345678901")
print(f"学生姓名：{student.name}")
print(f"学生年龄：{student.age}")
print(f"学生电话：{student.tel}")
```



## 魔术方法

__init__构造方法，是Python类内置的方法之一。内置的类方法，各自有各自特殊的功能，这些内置方法称之为：魔术方法，在Python通过`__方法名__`，都属于魔术方法。

常用魔术方法：

- `__init__`：构造方法
- `__call__`：实例化构造方法（让**实例对象可以像函数一样被调用**）
- `__str__`：字符串方法
- `__lt__`：小于、大于符号比较
- `__le__`：小于等于、大于等于符号比较
- `__eq__`：==符号比较

```python
"""
    常用魔术方法
"""

class Student:
    def __init__(self, name, age):
        self.name = name # 学生姓名
        self.age = age # 学生年龄

    #__call__魔术方法，自带一个参数self，表示当前对象
    def __call__(self, year):
        return f"出生年份：{year - self.age}" # 实例化调用时执行此操作

    # __str__魔术方法，自带一个参数self，表示当前对象
    def __str__(self):
        return f"姓名: {self.name}, 年龄: {self.age}"

    # _lt__魔术方法，自带两个参数self以及other，其中self表示当前对象，other表示要比较的对象
    def __lt__(self, other):
        return self.age < other.age

    # __le__魔术方法，自带两个参数self以及other，其中self表示当前对象，other表示要比较的对象
    def __le__(self, other):
        return self.age <= other.age

    # __eq__魔术方法，自带两个参数self以及other，其中self表示当前对象，other表示要比较的对象
    def __eq__(self, other):
        return self.age == other.age


student1 = Student("张三", 20)
print(student1) # <__main__.Student object at 0x00000189EA09BFD0>在没有编写__str__方法时打印的内容，其实是对象的内存地址

# 让实例对象可以像函数一样被调用，当实例对象被创建时自动调用__call__函数
birth_year = student1("2025")
print(birth_year) # 2005

student2 = Student("李四", 22) # TypeError: '<' not supported between instances of 'Student' and 'Student'在没有编写__lt__方法时比较两个学生对象会报错
# 比较两个学生对象,谁年龄大
print(student1 < student2)
print(student1 > student2)

# 在没有编写__le__方法时，TypeError: '<=' not supported between instances of 'Student' and 'Student'
print(student1 <= student2)
print(student1 >= student2)

# 不编写__eq__方法，对象之间可以比较，但是比较的是内存地址，也即是：就算两个对象所有的属性和方法都一样时比较结果也一定是False，因为他们在内存中是两个不同的对象，所以内存地址不同
# 编写__eq__方法后，就可以自行定义两个对象是否相等的规则
print(student1 == student2)
```



## 封装

面向对象编程，是许多编程语言都支持的一种编程思想。
简单理解是：基于模板（类）去创建实体（对象），使用对象完成功能开发。

面向对象包含3大主要特性：

- 封装
- 继承
- 多态

封装表示的是，将现实世界事物的属性和行为，封装到类中，描述为成员变量、成员方法，从而完成程序对现实世界事物的描述

现实世界中的事物，有属性和行为。但是不代表这些属性和行为都是开放给用户使用的。

例如：苹果越狱、安卓root，也是为了突破权限使用这些对用户隐藏的属性和行为

类中提供了私有成员的形式来支持。

- 私有成员变量
- 私有成员方法

定义私有成员的方式非常简单，只需要：

- 私有成员变量：变量名以_开头（2个下划线）
- 私有成员方法：方法名以_开头（2个下划线）

```python
"""
    封装
"""

# 定义一个类，内含私有成员变量和私有成员方法
class Phone:
    # 定义一个私有的成员变量，运行电压
    __current_voltage = None

    # 定义一个私有的成员方法
    def __keep_single_core(self):
        print("让CPU保持单核运行")


iphone = Phone()
print(iphone.__current_voltage) # AttributeError: 'Phone' object has no attribute '__current_voltage'. Did you mean: '_Phone__current_voltage'?
print(iphone.__keep_single_core()) # AttributeError: 'Phone' object has no attribute '__keep_single_core'. Did you mean: '_Phone__keep_single_core'?
```

私有成员无法被类对象使用，但是可以被类中其它的成员使用。

```python
"""
    封装
"""

# 定义一个类，内含私有成员变量和私有成员方法
class Phone:
    # 定义一个私有的成员变量，运行电压
    __current_voltage = 0.5

    # 定义一个私有的成员方法
    def __keep_single_core(self):
        print("让CPU保持单核运行")

    # 通过公有方法来访问私有成员变量和私有成员方法
    def call_by_5g(self):
        if self.__current_voltage >= 1:
            print("使用5G网络打电话")
        else:
            self.__keep_single_core()
            print("电压不足，无法使用5G网络打电话")


iphone = Phone()
# print(iphone.__current_voltage) # AttributeError: 'Phone' object has no attribute '__current_voltage'. Did you mean: '_Phone__current_voltage'?
# print(iphone.__keep_single_core()) # AttributeError: 'Phone' object has no attribute '__keep_single_core'. Did you mean: '_Phone__keep_single_core'?
iphone.call_by_5g()
```



## 继承

继承就是一个类，继承另外一个类的成员变量和成员方法

```python
# 基础语法
class 类(父类1,父类2,...父类N):
	类内容体
```

单继承：一个类继承另一个类

```python
"""
    继承
"""

# 父类
class Phone:
    IMEI = None
    producer = "Apple"

    def call_by_4g(self):
        print("4g通话")


# 子类继承Phone类，创建一个新的类Iphone16
class Iphone16(Phone):
    face_id = "10001"

    def call_by_5g(self):
        print("5g通话")


my_phone = Iphone16()
print(my_phone.producer)
my_phone.call_by_4g()
my_phone.call_by_5g()
```

多继承：一个类继承多个类，按照顺序从左向右依次继承；多继承中，如果父类有同名方法或属性，先继承的优先级高于后继承

```python
"""
    继承
"""

# 多继承
# 父类
class Phone:
    IMEI = None
    producer = "Apple"

    def call_by_4g(self):
        print("4g通话")


# 父类
class NFCReader:
    ntf_type = "第五代"
    producer = "Xiaomi"

    def read_card(self):
        print("读卡")

    def write_card(self):
        print("写卡")


# 父类
class RemoteControl:
    rc_type = "红外遥控"

    def control(self):
        print("红外遥控开启了")

# 子类继承Phone、NFCReader和RemoteControl类，创建一个新的类MyPhone
class MyPhone(Phone, NFCReader, RemoteControl):
    # pass是占位语句用来保证函数（方法）或类定义的完整性，表示无内容，空的意思
    pass

my_phone = MyPhone()
# 在多继承中访问同名属性和方法时，按照继承顺序查找
print(my_phone.producer) # Apple
my_phone.call_by_4g()
my_phone.read_card()
my_phone.write_card()
my_phone.control()
```

复写：子类继承父类的成员属性和成员"不满意"，那么可以进行复写。即：在子类中重新定义同名的属性或方法即可。

```python
"""
    继承的复写和使用父类成员
"""


# 父类
class Phone:
    IMEI = None
    producer = "Apple"

    def call_by_5g(self):
        print("Phone的5g通话")

# 子类
class MyPhone(Phone):
    # 复写父类的成员变量
    producer = "Xiaomi"

    # 复写父类的方法
    def call_by_5g(self):
        print("MyPhone的5g通话")
        print("使用5G网络通话")
        print("关闭CPU单核模式")


my_phone = MyPhone()
print(my_phone.producer)
my_phone.call_by_5g()
```

调用父类同名成员，一旦复写父类成员，那么类对象调用成员的时候，就会调用复写后的新成员
如果需要使用被复写的父类的成员，需要特殊的调用方式：

调用父类成员

- 使用成员变量：父类名成员变量
- 使用成员方法：父类名.成员方法(self)

使用super()调用父类成员

- 使用成员变量：super().成员变量
- 使用成员方法：super().成员方法()

```python
"""
    继承的复写和使用父类成员
"""


# 父类
class Phone:
    IMEI = None
    producer = "Apple"

    def call_by_5g(self):
        print("Phone的5g通话")

# 子类
class MyPhone(Phone):
    # 复写父类的成员变量
    producer = "Xiaomi"

    # 复写父类的方法
    def call_by_5g(self):
        print("MyPhone的5g通话")
        print("使用5G网络通话")
        print("关闭CPU单核模式")

        # 方式一：通过父类名调用父类的成员变量和方法
        print(f"父类的品牌是：{Phone.producer}")
        Phone.call_by_5g(self)

        # 方式二：通过super()调用父类的成员变量和方法
        print(f"父类的品牌是：{super().producer}")
        super().call_by_5g()



my_phone = MyPhone()
print(my_phone.producer)
my_phone.call_by_5g()
```



## 变量的类型注解

Python在3.5版本的时候引入了类型注解，以方便静态类型检查工具，IDE等第三方工具。

类型注解：在代码中涉及数据交互的地方，提供数据类型的注解（显式的说明）。

主要功能：

- 帮助第三方IDE工具（如PyCharm）对代码进行类型推断，协助做代码提示
- 帮助开发者自身对变量进行类型注释

支持：

- 变量的类型注解
- 函数（方法）形参列表和返回值的类型注解

为变量设置类型注解

```python
# 基础语法：变量:类型
var_1:int= 10
var_2:float = 3.1415926
var_3:bool = True
var_4:str = "mumangguo"
```

类对象类型注解

```python
class Student:
	pass
stu:Student = Student()
```

基础容器类型注解

```python
my_list:list = [1,2，3]
my_tuple:tuple = (1,2,3)
my_set:set = {1,2,3}
my_dict:dict = {"mumangguo":888}
my_str:str = "mumangguo"
```

容器类型详细注解

```python
my_list:list[int]=[1, 2, 3]
my_tuple:tuple[str, int, bool] = ("mumangguo", 666, True) # 元组类型设置类型详细注解，需要将每一个元素都标记出来
my_set:set[int] = {1, 2, 3}
my_dict:dict[str, int]= {"mumangguo": 666} # 字典类型设置类型详细注解，需要2个类型，第一个是key第二个是value
```

在注释中进行类型注解 # type:类型

```python
var_1 = random.randint(1,10) # type:int
var_2 = json.loads('{"key1": 1, "key2": 2, "key3": 3}') # type:dict[str,int]
def func():
    return 10
var_3 = func() # type:int
```

类型注解只是提示性的，并非决定性的。数据类型和注解类型无法对应也不会导致错误



## 函数和方法的类型注解

形参注解，在编写函数（方法），使用形参的时候，工具没有任何提示；在调用函数（方法），传入参数的时候，工具无法提示参数类型，这些都是因为，我们在定义函数（方法）的时候，没有给形参进行注解

函数和方法的形参类型注解语法：

```python
def 函数方法名(形参名:类型,形参名:类型,...):
	pass

# 例如：
def add(x: int, y: int):
	return x + y

def func(data: list):
	pass
```

函数（方法）的返回值也是可以添加类型注解的，语法如下：

```python
def 函数方法名(形参名:类型,形参名:类型,...) -> 返回值类型:
	pass

# 例如：
def add_with_return(x: int, y: int) -> int:
    return x + y
```



## Union联合类型注解

使用Union[类型,...类型]，可以定义联合类型注解

```python
"""
    Union联合类型注解
"""

# 使用Union类型，必须要导入Union
from typing import Union

my_list: list[Union[int, str]] = [1, "hello", 2, "world"]  # 表示列表中可以包含int和str类型的元素


def func(data: Union[int, str]) -> Union[int, str]:
    """
        函数的参数和返回值都可以是int或str类型
    :param data:
    :return:
    """
    pass
```



## 多态

多态，指的是：多种状态，即完成某个行为时，使用不同的对象会得到不同的状态。**同样的行为（函数），传入不同的对象，得到不同的状态**

多态常需要作用在继承关系上。函数(方法)形参声明接收父类对象，实际传入父类的子类对象进行工作，即以父类做定义声明，以子类做实际工作，用以获得同一行为，不同状态。

```python
"""
    多态
"""

# 父类
class Animal:
    def speak(self):
        pass

# 子类
class Dog(Animal):
    def speak(self):
        print("汪汪汪")

# 子类
class Cat(Animal):
    def speak(self):
        print("喵喵喵")


def make_noise(animal: Animal):
    """
    接受一个Animal类型的参数，并调用其speak方法
    :param animal: Animal类型的实例
    """
    animal.speak()


dog = Dog()
make_noise(dog)

cat = Cat()
make_noise(cat)
```

父类Animal的speak方法，是空实现，这种设计的含义是父类用来确定有哪些方法，具体的方法实现，由子类自行决定，这种写法，就叫做抽象类（也可以称之为接口）

抽象类：含有抽象方法的类称之为抽象类

抽象方法：方法体是空实现的（pass）称之为抽象方法

抽象类就好比定义一个标准，包含了一些抽象的方法，要求子类必须实现。多用于做顶层设计（设计标准），以便子类做具体实现。也是对子类的一种软性约束，要求子类必须复写（实现）父类的一些方法，并配合多态使用，获得不同的工作状态。

```python
# 演示抽象类
class AC:
    def cool_wind(self):
        # 制冷
        pass

    def hot_wind(self):
        # 制热
        pass

    def swing_l_r(self):
        # 左右摆风
        pass


class Midea_AC(AC):
    def cool_wind(self):
        print("美的空调制冷")

    def hot_wind(self):
        print("美的空调制热")

    def swing_l_r(self):
        print("美的空调左右摆风")


class GREE_AC(AC):
    def cool_wind(self):
        print("格力空调制冷")

    def hot_wind(self):
        print("格力空调制热")

    def swing_l_r(self):
        print("格力空调左右摆风")


def make_cool(ac: AC):
    """
    接受一个AC类型的参数，并调用其cool_wind方法
    :param ac: AC类型的实例
    """
    ac.cool_wind()

make_cool(Midea_AC())
make_cool(GREE_AC())
```



## 浅拷贝和深拷贝

在 Python 里，`copy`（浅拷贝）和`deepcopy`（深拷贝）是用于复制对象的两种不同方式，它们的主要区别在于复制的深度以及对象引用的处理方式。

### 赋值操作

赋值操作只是创建一个新的变量，该变量指向的是同一个对象，并非复制对象本身。

```python
original = [1, 2, [3, 4]]
copy = original  # 赋值操作
copy[0] = 99     # 修改复制后的对象
print(original)  # 输出：[99, 2, [3, 4]]
```

**关键点**：赋值操作不会创建新的对象，原对象和复制对象共享同一块内存空间。

### 浅拷贝

浅拷贝会创建一个新的对象，不过对于对象中的嵌套对象，仍然使用原始的引用。

```python
import copy

original = [1, 2, [3, 4]]
shallow_copy = copy.copy(original)  # 浅拷贝
shallow_copy[0] = 99                # 修改顶层元素
shallow_copy[2][0] = 33             # 修改嵌套元素
print(original)  # 输出：[1, 2, [33, 4]]
```

**关键点**：

- 浅拷贝会生成一个新的容器对象（如列表）。
- 嵌套对象（如内部列表）不会被复制，原对象和浅拷贝对象共享这些嵌套对象。

### 深拷贝

深拷贝会递归地复制对象及其所有嵌套对象，创建出一个完全独立的对象。

```python
import copy

original = [1, 2, [3, 4]]
deep_copy = copy.deepcopy(original)  # 深拷贝
deep_copy[0] = 99                    # 修改顶层元素
deep_copy[2][0] = 33                 # 修改嵌套元素
print(original)  # 输出：[1, 2, [3, 4]]
```

**关键点**：

- 深拷贝会创建一个完全独立的对象，包括所有的嵌套对象。
- 原对象和深拷贝对象没有任何共享的引用。

###  自定义对象的复制

对于自定义类的对象，浅拷贝和深拷贝的行为取决于类的实现：

```python
import copy

class Person:
    def __init__(self, name, hobbies):
        self.name = name
        self.hobbies = hobbies

# 创建一个Person对象
p1 = Person("Alice", ["reading", "swimming"])

# 浅拷贝
p2 = copy.copy(p1)
p2.hobbies.append("running")
print(p1.hobbies)  # 输出：['reading', 'swimming', 'running']

# 深拷贝
p3 = copy.deepcopy(p1)
p3.hobbies.append("dancing")
print(p1.hobbies)  # 输出：['reading', 'swimming', 'running']
```

### 总结

| 操作类型  | 是否创建新对象 | 是否复制嵌套对象 |
| --------- | -------------- | ---------------- |
| 赋值（=） | 否             | 否               |
| 浅拷贝    | 是             | 否               |
| 深拷贝    | 是             | 是               |



# Python的标准库

Python的标准库非常庞大，所提供的组件涉及范围十分广泛，使用标准库我们可以让您轻松地完成各种任务。

以下是一些Python常用标准库中的模块：

- os模块：提供与操作系统交互的功能，如文件路径操作（`os.path`子模块）、目录创建（`os.mkdir()`）、删除（`os.rmdir()`）、获取环境变量（`os.environ`）、执行系统命令（`os.system()`）等。例如，`os.listdir('.')`可列出当前目录下的所有文件和文件夹
- sys模块：用于访问与 Python 解释器相关的变量和函数，如命令行参数（`sys.argv`）、退出程序（`sys.exit()`）、获取 Python 版本信息（`sys.version`）、标准输入输出流（`sys.stdin`/`sys.stdout`）等。例如，`sys.argv`可获取运行脚本时传入的参数列表
- time模块：提供处理时间的基本功能，如获取当前时间戳（`time.time()`）、格式化时间（`time.strftime()`）、程序暂停（`time.sleep(secs)`）等。时间戳是从 1970 年 1 月 1 日 00:00:00 UTC 开始到现在的秒数
- datetime模块：提供更高级的日期和时间处理功能，包含`datetime`（日期时间）、`date`（日期）、`time`（时间）等类。例如，`datetime.datetime.now()`可获取当前本地日期时间，支持日期加减等操作
- random模块：用于生成随机数，如随机整数（`random.randint(a, b)`）、随机浮点数（`random.random()`）、打乱列表顺序（`random.shuffle(list)`）、从序列中随机选择元素（`random.choice(seq)`）等
- math模块：提供基本的数学运算函数，如三角函数（`math.sin()`、`math.cos()`）、对数（`math.log()`）、开方（`math.sqrt()`）、取整（`math.floor()`、`math.ceil()`）等，适用于浮点数运算
- re模块：提供正则表达式操作功能，用于字符串的匹配、查找、替换等。例如，`re.search(pattern, string)`可在字符串中搜索匹配正则表达式的内容，`re.sub(pattern, repl, string)`可替换匹配的子串
- json模块：用于处理 JSON 格式数据，提供`json.dumps()`（将 Python 对象转为 JSON 字符串）和`json.loads()`（将 JSON 字符串转为 Python 对象）函数，常用于数据序列化和反序列化
- urllib模块：用于处理 URL 相关操作，包含`urllib.request`（发送 HTTP 请求）、`urllib.parse`（解析 URL）等子模块。例如，`urllib.request.urlopen(url)`可打开一个 URL 并读取其内容。
- hashlib模块：提供多种加密算法，如 MD5、SHA1、SHA256 等，用于生成数据的哈希值。哈希值是不可逆的，常用于密码存储、数据校验等。例如，`hashlib.md5(b'hello').hexdigest()`可生成 “hello” 的 MD5 哈希值。
- logging模块：用于记录程序运行时的日志信息，支持设置日志级别（DEBUG、INFO、WARNING、ERROR、CRITICAL）、输出到文件或控制台、格式化日志内容等。相比`print`，更适合在大型项目中跟踪程序状态。
- pickle模块：用于 Python 对象的序列化与反序列化，允许将对象转换为字节流（序列化）并在需要时恢复（反序列化）。



# Pickle

`pickle`是 Python 标准库中的一个模块，主要功能是实现 Python 对象的序列化与反序列化。简单来说，就是可以把对象转换为字节流，也能把字节流再恢复成原来的对象。

## 序列化

序列化是指将 Python 对象（像列表、字典、类实例等）转化为字节流的过程，这个过程也被叫做 "pickling"。

```python
import pickle

data = {
    'name': 'Alice',
    'age': 30,
    'hobbies': ['reading', 'swimming']
}

# 将对象序列化为字节流
with open('data.pkl', 'wb') as f:
    pickle.dump(data, f)
```

## 反序列化

反序列化则是把字节流重新转换为 Python 对象的过程，也称为"unpickling"。

```python
import pickle

# 从文件中读取字节流并反序列化为对象
with open('data.pkl', 'rb') as f:
    loaded_data = pickle.load(f)

print(loaded_data)  # 输出：{'name': 'Alice', 'age': 30, 'hobbies': ['reading', 'swimming']}
```

## 主要方法

- **`pickle.dump(obj, file)`**：将对象`obj`序列化后写入文件对象`file`中。
- **`pickle.load(file)`**：从文件对象`file`中读取字节流，并反序列化为对象。
- **`pickle.dumps(obj)`**：将对象`obj`序列化为字节对象（bytes）。
- **`pickle.loads(bytes_obj)`**：把字节对象`bytes_obj`反序列化为对象。

## 支持的对象类型

`pickle`能够处理大多数 Python 对象，包括：

- 基本数据类型，如整数、浮点数、字符串、布尔值等。
- 容器类型，如列表、元组、字典、集合等。
- 函数（仅限模块级别的函数）。
- 类（仅限模块级别的类）。
- 类实例（前提是类在反序列化时是可导入的）。

## 使用场景

1. **数据持久化**：把复杂的数据结构保存到文件或者数据库中，例如缓存、会话数据等。
2. **跨进程通信**：在进程间传递对象，比如使用`multiprocessing`模块时。
3. **远程调用**：在分布式系统中传输对象，不过这种情况下更推荐使用 JSON 或 Protocol Buffers 等标准格式。



# JSON

## 什么是JSON?

JSON是一种轻量级的数据交互格式。可以按照JSON指定的格式去组织和封装数据，JSON本质上是一个带有特定格式的字符串，Python语言使用JSON有很大优势，因为：JSON无非就是一个单独的字典或一个内部元素都是字典的列表
主要功能：json就是一种在各个编程语言中流通的数据格式，负责不同编程语言中的数据传递和交互

## JSON有什么用?

各种编程语言存储数据的容器不尽相同，在Python中有字典dict这样的数据类型，而其它语言可能没有对应的字典。为了让不同的语言都能够相互通用的互相传递数据，JSON就是一种非常良好的中转数据格式。

## Python中的应用

json格式数据转化

```json
# json数据的格式可以是：
("name":"admin","age":18}
# 也可以是：
[("name":"admin","age":18},("name":"root","age":16),("name":"张=","age":20}]
```

Python数据和Json数据的相互转化

```python
"""
    JSON数据转换
"""

# 导入json模块
import json

# 准备符合格式json格式要求的python数据
data = [{"name": "老王", "age": 16}, {"name": "张三", "age": 20}]

# 通过json.dumps(data)方法把python数据转化为了json数据，如果有中文数据需要将ensure_ascii设置为False
data = json.dumps(data, ensure_ascii=False)
print(data, type(data))

# 通过json.loads(data)方法把json数据转化为了python数据
data = json.loads(data)
print(data, type(data))

# 将字典转换为JSON
data = {"name": "老王", "age": 16}
data = json.dumps(data, ensure_ascii=False)
print(data, type(data))
data = json.loads(data)
print(data, type(data))
```

## Pickle与JSON的区别

在 Python 里，Pickle 和 JSON 都能用于对象的序列化与反序列化，不过它们的应用场景、数据类型支持以及兼容性存在差异。

**JSON（JavaScript Object Notation）**

JSON 属于文本格式，具备跨语言的特性，在 Web 应用的数据交换场景中较为常见。

- **支持的数据类型**：包含字典、列表、字符串、数字、布尔值以及 null。
- **应用场景**：常用于不同编程语言的系统之间进行数据交换，像 API 数据传输、配置文件存储等。
- **优势**：采用文本格式，便于人类阅读，并且拥有广泛的跨语言支持。
- **局限**：仅能处理基础数据类型，无法对自定义类的实例进行序列化。

**Pickle**

Pickle 是 Python 专有的二进制格式，能够对更丰富的对象类型进行序列化。

- **支持的数据类型**：可以处理几乎所有的 Python 对象，其中包括自定义类的实例、函数等。
- **应用场景**：主要用于 Python 程序内部的数据存储，例如缓存、对象持久化等。
- **优势**：无需额外配置，就能支持复杂对象的序列化。
- **局限**：只能在 Python 环境中使用，并且存在安全风险（如果加载来自不可信来源的数据，可能会执行恶意代码）。

**主要区别对比**

| **特性**       | **JSON**                   | **Pickle**                 |
| -------------- | -------------------------- | -------------------------- |
| 数据格式       | 文本格式                   | 二进制格式                 |
| 跨语言支持     | 支持多种语言               | 仅支持 Python              |
| 安全性         | 安全（仅处理简单数据类型） | 不安全（可能执行恶意代码） |
| 支持的对象类型 | 基础数据类型               | 几乎所有 Python 对象       |
| 可读性         | 人类可读                   | 人类不可读                 |
| 性能           | 较慢（文本解析）           | 较快（二进制处理）         |



# Python操作MySQL

## 介绍

MySQL数据库管理系统由瑞典的DataKonsultAB公司研发，该公司被Sun公司收购，现在Sun公司又被Oracle公司收购，因此MySQL目前属于Oracle旗下产品。

MySQL软件采用了双授权政策，分为社区版和商业版，由于其体积小、速度快、总体拥有成本低，一般开发都选择MySQL作为数据库。

简单来说，MySQL是一个中小型的数据库，简单易用性能不错，在企业中频繁出现。
大多数开发人员都会和MySQL打交道，可以说是开发人员必须会使用的一款数据库软件。

针对不同的用户，MySQL分为两种不同的版本：

- MySQL Community Server：社区版本，免费，但是Mysql不提供官方技术支持
- MySQL Cluster：集群版，开源免费，可将几个MySQLServer封装成一个Server
- MySQL Enterprise Edition：商业版，该版本是收费版本，可以试用30天，官方提供技术支持
- MySQL Cluster CGE：高级集群版，需付费

下载地址：https://downloads.mysql.com/archives/installer

SQL全称：Structured Query Language，结构化查询语言，用于访问和处理数据库的标准的计算机语言。

SQL语言1974年由Boyce和Chamberlin提出，并首先在IBM公司研制的关系数据库系统SystemR上实现。

经过多年发展，SQL以成为数据库领域统一的数据操作标准语言，可以说几乎市面上所有的数据库系统都支持使用SQL语言来操作

由于数据库管理系统（数据库软件）功能非常多，不仅仅是存储数据，还要包含：数据的管理、表的管理、库的管理、账户管理、权限管理等等。
所以，操作数据库的SQL语言，也基于功能，可以划分为4类：

- 数据定义：DDL(Data Definition Language)，库的创建删除、表的创建删除等
- 数据操纵：DML (Data Manipulation Language)，新增数据、删除数据、修改数据等
- 数据控制：DCL（Data Control Language)，新增用户、删除用户、密码修改、权限管理等
- 数据查询：DQL(Data Query Language)，基于需求查询和计算数据

SQL语言，大小写不敏感

SQL可以单行或多行书写，最后以;号结束

SQL支持注释：

- 单行注释：--注释内容（--后面一定要有一个空格）
- 单行注释：#注释内容（#后面可以不加空格，推荐加上）
- 多行注释：/*注释内容*/

DDL数据定义常用SQL：

```sql
# 查看数据库
SHOW DATABASES;
# 使用数据库
USE 数据库名称;
# 创建数据库
CREATE DATABASE 数据库名称 [CHARSET UTF8];
# 删除数据库
DROP DATABASE 数据库名称;
# 查看当前使用的数据库
SELECT DATABASE();
# 查看有哪些表 注意：需要先选择数据库哦
SHOW TABLES;
# 删除表
DROP TABLE 表名称;
DROP TABLE IF EXISTS 表名称;
# 创建表
CREATE TABLE 表名称(
列名称 列类型,
列名称 列类型,
);
# 列类型有
int -- 整数
float -- 浮点数
varchar(长度) -- 文本，长度为数字，做最大长度限制
date -- 日期类型
timestamp -- 时间戳类型
```

DML数据操纵常用SQL：

```sql
# 数据插入 INSERT，一个列对应一个值
INSERT INTO 表(列1,列2,...) VALUES(值1,值2,...);
# 数据删除 DELETE
DELETE FROM 表名称 [WHERE 条件判断];
# 数据更新 UPDATE，一个列对应一个值
UPDATE 表名 SET 列=值 [WHERE 条件判断];
```

DQL数据查询常用SQL：

```sql
# 查询单个字段或者所有字段
SELECT 字段列表|* FROM 表;
# 根据条件查询
SELECT 字段列表|* FROM 表 WHERE 条件判断;
# 分组聚合查询
SELECT 字段|聚合函数 FROM 表 [WHERE条件] GROUP BY 列;
聚合函数有：
SUM(列) 求和
AVG(列) 求平均值
MIN(列) 求最小值
MAX(列) 求最大值
COUNT(列|*) 求数量
# 排序查询，ASC表示升序，DESC表示降序
SELECT 列|聚合函数|* FROM 表
WHERE ...
GROUP BY ...
ORDER BY ... [ASC | DESC]
# 分页查询
SELECT 列|聚合函数|* FROM 表
WHERE ...
GROUP BY ...
ORDER BY ... [ASC | DESC]
LIMIT n[,m]
```



## pymysql

在Python中，使用第三方库：pymysql来完成对MySQL数据库的操作。

安装：

```shell
pip install pymysql
```

入门：

```python
"""
    pymysql库的基本操作
"""
from pymysql import Connection

# 构建到MySQL数据库的链接
connection = Connection(host="localhost",  # MySQL服务器地址
                        port=3306,  # MySQL服务器端口
                        user="root",  # MySQL用户名
                        password="admin")  # MySQL密码
server_info = connection.get_server_info()
print(f"连接到MySQL服务器成功，版本信息：{server_info}")

# 执行非查询性质SQL
# 选择数据库
connection.select_db("mumangguo")
# 获取游标对象
cursor = connection.cursor()
# 执行创建数据库的SQL语句
# cursor.execute("CREATE TABLE test_pymysql (id int);")

# 执行查询性质SQL
# 通过游标对象执行SQL语句
cursor.execute("select * from t_student;")
# 获取查询结果
result = cursor.fetchall()
for i in result:
    print(i)

# 关闭链接
connection.close()
```

数据插入（pymysql库在执行对数据库有修改操作的行为时，是需要通过链接对象的commit成员方法来进行确认的。只有确认的修改，才能生效）：

```python
"""
    mysql数据插入
"""
from pymysql import Connection

connection = Connection(host="localhost",  # MySQL服务器地址
                        port=3306,  # MySQL服务器端口
                        user="root",  # MySQL用户名
                        password="admin",  # MySQL密码
                        database="mumangguo",  # 选择数据库
                        autocommit=True  # 设置自动提交事务为True
                        )

# 获取游标对象
cursor = connection.cursor()

# 执行插入数据的SQL语句
cursor.execute("INSERT INTO t_student (name, age) VALUES ('小明', 18);")

# 提交事务，在没有设置autocommit的情况下，必须手动交事务才能使插入生效
# connection.commit()

# 关闭连接
connection.close()
```

## 综合案例

数据库表创建SQL语句：

```sql
CREATE DATABASE py_sql;
use py_sql;

CREATE TABLE `orders`  (
  `id` bigint NOT NULL AUTO_INCREMENT,
  `order_date` date NULL DEFAULT NULL,
  `order_id` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NULL DEFAULT NULL,
  `money` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NULL DEFAULT NULL,
  `province` varchar(10) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NULL DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
)
```

main.py

```python
"""
    1．创建数据对象
    2．将数据存入MySQL数据库
"""

import json
from datetime import date
from pymysql import Connection

# 1. 手动创建数据示例
text_orders = [
    [date(2011, 1, 1), "001", 200.0, "Beijing"],
    [date(2011, 1, 2), "002", 150.0, "Shanghai"],
    [date(2011, 1, 3), "003", 120.0, "Guangzhou"],
    [date(2011, 1, 4), "004", 350.0, "Shenzhen"],
    [date(2011, 1, 5), "005", 180.0, "Hangzhou"],
    [date(2011, 1, 6), "006", 220.0, "Chengdu"],
    [date(2011, 1, 7), "007", 160.0, "Xi'an"],
    [date(2011, 1, 8), "008", 310.0, "Wuhan"],
    [date(2011, 1, 9), "009", 270.0, "Tianjin"],
    [date(2011, 1, 10), "010", 300.0, "Nanjing"],
    [date(2011, 1, 11), "011", 210.0, "Suzhou"],
    [date(2011, 1, 12), "012", 330.0, "Shenzhen"],
    [date(2011, 1, 13), "013", 200.0, "Beijing"],
    [date(2011, 1, 14), "014", 190.0, "Shanghai"],
    [date(2011, 1, 15), "015", 170.0, "Guangzhou"],
    [date(2011, 1, 16), "016", 380.0, "Shenzhen"],
    [date(2011, 1, 17), "017", 250.0, "Hangzhou"],
    [date(2011, 1, 18), "018", 230.0, "Chengdu"],
    [date(2011, 1, 19), "019", 180.0, "Xi'an"],
    [date(2011, 1, 20), "020", 290.0, "Wuhan"],
]

json_orders = [
    [date(2011, 2, 1), "021", 210.0, "Beijing"],
    [date(2011, 2, 2), "022", 240.0, "Shanghai"],
    [date(2011, 2, 3), "023", 160.0, "Guangzhou"],
    [date(2011, 2, 4), "024", 370.0, "Shenzhen"],
    [date(2011, 2, 5), "025", 190.0, "Hangzhou"],
    [date(2011, 2, 6), "026", 250.0, "Chengdu"],
    [date(2011, 2, 7), "027", 300.0, "Xi'an"],
    [date(2011, 2, 8), "028", 220.0, "Wuhan"],
    [date(2011, 2, 9), "029", 270.0, "Tianjin"],
    [date(2011, 2, 10), "030", 320.0, "Nanjing"],
]

# 合并
all_orders = text_orders + json_orders

# 构建MySQL链接对象
connection = Connection(
    host="localhost",  # MySQL服务器地址
    port=3306,  # MySQL服务器端口
    user="root",  # MySQL用户名
    password="admin",  # MySQL密码
    database="py_sql",  # 选择数据库
    autocommit=True  # 设置自动提交事务为True
)

# 获得游标对象
cursor = connection.cursor()

# 执行SQL语句
# for order in all_orders:
#     sql = "INSERT INTO orders (order_date, order_id, money, province) VALUES (%s, %s, %s, %s)"
#     cursor.execute(sql, (order[0], order[1], order[2], order[3]))

# 查询数据并以json格式保存到文件中
sql = "SELECT * FROM orders"
cursor.execute(sql)
results = cursor.fetchall()
with open("orders.json", "w", encoding="utf-8") as f:
    for row in results:
        # 将数据转换为字典
        order_dict = {
            "date": row[0].strftime('%Y-%m-%d') if isinstance(row[0], date) else row[0],  # 确保日期格式正确
            "order_id": row[1],
            "money": row[2],
            "province": row[3]
        }
        # 将字典写入JSON文件
        f.write(json.dumps(order_dict, ensure_ascii=False) + ",\n")

# 关闭连接
connection.close()
```

# 闭包

定义双层嵌套函数，内层函数可以访问外层函数的变量，将内层函数作为外层函数的返回，此内层函数就是闭包函数

```python
"""
    闭包
"""


# 演示简单的闭包方法
def outer(logo):
    def inner(msg):
        print(f"{logo}|{msg}|{logo}")

    return inner


# 使用闭包
fn1 = outer("木芒果")
fn1("你好")
fn1("我也好")

fn2 = outer("mumangguo")
fn2("你好")
fn2("我也好")


# 使用nonlocal关键字修改外部函数的值
def outer2(num1):
    def inner(num2):
        nonlocal num1
        num1 += num2
        print(f"num1={num1}")

    return inner


# 使用闭包
fn3 = outer2(10)
fn3(1)
fn3(2)


# 使用闭包实现ATM取款案例
def bank(initial_amount=0):
    def atm(num, deposit=True):
        nonlocal initial_amount
        if deposit:
            initial_amount += num
            print(f"存款成功，当前余额：{initial_amount}")
        else:
            if num > initial_amount:
                print("余额不足，取款失败")
            else:
                initial_amount -= num
                print(f"取款成功，当前余额：{initial_amount}")
    return atm

# 使用闭包
atm = bank(1000)
atm(500, False)  # 取款500
atm(200)   # 存款200
```

优点，使用闭包可以让我们得到：

- 无需定义全局变量即可实现通过函数，持续的访问、修改某个值
- 闭包使用的变量的所用于在函数内，难以被错误的调用修改

缺点：

- 由于内部函数持续引用外部函数的值，所以会导致这一部分内存空间不被释放，一直占用内存



# 装饰器

装饰器（Decorators）是Python中一种强大而灵活的功能，用于修改或增强函数或类的行为。装饰器本质上是一个函数，它接受另一个函数或类作为参数，并返回一个新的函数或类。它们通常用于在不修改原始代码的情况下添加额外的功能或功能。装饰器是Python中一个非常强大和常用的特性，它可以用于许多不同的情况，例如缓存、日志记录、权限控制等。通过在项目中使用的我们介绍的这些Python装饰器，可以简化我们的开发流程或者让我们的代码更加健壮。

装饰器的语法使用`@`符号，将装饰器应用于目标函数或类。

装饰器其实也是一种闭包，其功能就是在不破坏目标函数原有的代码和功能的前提下，为目标函数增加新功能。

## 常用装饰器

### @staticmethod

`@staticmethod`装饰器是Python中用于定义静态方法的装饰器。静态方法是与类相关联但不依赖于实例的方法。它们可以直接通过类名调用，而无需创建类的实例

```python
# 示例1：静态方法通常被用于处理和类相关的计算逻辑，而与类实例的状态无关。例如，我们可以在一个日期类中定义一个静态方法，用于判断某一年是否为闰年。因为判断闰年与具体的日期实例无关，所以这个方法可以被定义为静态方法
class Date:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day

    @staticmethod
    def is_leap_year(year):
        if year % 4 == 0 and year % 100 != 0 or year % 400 == 0:
            return True
        else:
            return False

    def display_date(self):
        print(f"Date: {self.year}-{self.month}-{self.day}")

# 创建日期实例
my_date = Date(2022, 10, 1)

# 调用静态方法判断是否为闰年
if Date.is_leap_year(my_date.year):
    print(f"{my_date.year} is a leap year.")
else:
    print(f"{my_date.year} is not a leap year.")
    
# 示例2：类中的静态方法可以被类方法和实例方法访问
class MyClass:
    @staticmethod
    def static_method():
        print("This is a static method.")
    
    @classmethod
    def class_method(cls):
        cls.static_method()
        print("This is a class method.")
    
    def instance_method(self):
        self.static_method()
        print("This is an instance method.")

# 通过类名调用静态方法
MyClass.static_method()
# 输出: This is a static method.

# 通过类方法调用静态方法
MyClass.class_method()
# 输出:
# This is a static method.
# This is a class method.

# 创建类的实例
obj = MyClass()
# 通过实例调用静态方法
obj.static_method()
# 输出: This is a static method.

# 通过实例方法调用静态方法
obj.instance_method()
# 输出:
# This is a static method.
# This is an instance method.
```

### @classmethod

`@classmethod`装饰器用于定义类方法。类方法与普通方法不同，它在类层级上操作，而不是在实例层级上。通过类方法，我们可以直接通过类名调用方法，而无需创建类的实例。并且第一个参数通常被命名为 cls，代表类本身，而不是常见的self。类方法可以访问类的属性和其他类方法（不包括实例方法），但不能直接访问实例的属性。

```python
# 示例1：访问类的属性搭配使用，注意不是实例的属性self.xxx。示例中统计创建了多少个对象。
class MyClass:
    count = 0 # 类的属性 而不是实例属性

    def __init__(self):
        MyClass.count += 1

    @classmethod
    def get_count(cls):
        return cls.count

obj1 = MyClass()
obj2 = MyClass()
obj3 = MyClass()
print(MyClass.get_count())  # 输出：3

# 示例2：从字符串中创建对象，类方法可以提供一种替代构造方法的方式。
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def display(self):
        print(f"Name: {self.name}, Age: {self.age}")

    @classmethod
    def from_string(cls, string):
        name, age = string.split(",")
        return cls(name, int(age))

person_str = "John,25"
person = Person.from_string(person_str)
person.display()  # 输出：Name: John, Age: 25

# 示例3：根据不同的类型参数返回不同的子类对象
class Shape:
    def __init__(self, color):
        self.color = color

    def display_color(self):
        print(f"Color: {self.color}")

    @classmethod
    def create_shape(cls, color, type):
        if type == "circle":
            return Circle(color)
        elif type == "rectangle":
            return Rectangle(color)

class Circle(Shape):
    def display_shape(self):
        print("Type: Circle")

class Rectangle(Shape):
    def display_shape(self):
        print("Type: Rectangle")

circle = Shape.create_shape("red", "circle")
circle.display_color()  # 输出：Color: red
circle.display_shape()  # 输出：Type: Circle

rectangle = Shape.create_shape("blue", "rectangle")
rectangle.display_color()  # 输出：Color: blue
rectangle.display_shape()  # 输出：Type: Rectangle
```

### @staticmethod和@classmethod区别

| 特性       | 静态方法 (@staticmethod)                | 类方法 (@classmethod)                   |
| ---------- | --------------------------------------- | --------------------------------------- |
| 绑定       | 与类或实例无关                          | 绑定到类                                |
| 第一个参数 | 无需 self 或 cls                        | 接受 cls 作为第一个参数                 |
| 访问权限   | 无法访问类属性                          | 可以访问和修改类属性                    |
| 适用场景   | 与类逻辑无关的独立功能                  | 需要操作类级别数据时                    |
| 调用方式   | ClassName.method() 或 instance.method() | ClassName.method() 或 instance.method() |

### @property

`@property`装饰器是Python中一个特殊的装饰器，用于定义类的属性。它提供了一种简洁的方式来定义属性的访问方法，并且可以在需要时进行计算或验证。应用于类的实例方法，将其转换为类的属性。通过使用@property装饰器，可以将一个方法定义为只读属性，也可以定义一个可读写的属性，并且可以实现属性删除。
`@setter`装饰器用于定义一个属性的setter方法，用于修改属性的值。使用@setter时，我们需要在`@property`装饰的属性方法之后，紧跟一 个setter方法，并使用`@属性名.setter`来装饰该方法
`@setter`通常用于以下场景：
当一个属性的值需要计算得到，而不是直接存储在类的属性中时，我们可以使用@setter来提供一个修改属性值的接口。
当某个属性的值需要经过一些处理后再进行存储时，我们可以使用@setter来自动执行处理操作。

```python
# 示例1：可读写属性、属性删除
class Person:
    def __init__(self, name):
        self._name = name # 私有属性
    
    @property       
    def name(self):        # 读取私有属性
        return self._name
    
    @name.setter          # 可写属性 
    def name(self, value):
        self._name = value
    
    @name.deleter
    def name(self):      # 删除属性
        del self._name

person = Person("Alice")
print(person.name)  # 输出: Alice
del person.name
print(person.name)  # 抛出AttributeError异常，属性已被删除

# 示例2：属性计算，@property 装饰器可以用于对属性的计算，使得通过访问属性时能够返回计算后的结果
class Rectangle:
    def __init__(self, width, height):
        self._width = width
        self._height = height

    @property
    def width(self):
        return self._width

    @width.setter
    def width(self, value):
        if value >= 0:
            self._width = value
        else:
            raise ValueError("Width must be a non-negative number.")

    @property
    def height(self):
        return self._height

    @height.setter
    def height(self, value):
        if value >= 0:
            self._height = value
        else:
            raise ValueError("Height must be a non-negative number.")

    @property
    def area(self):
        return self._width * self._height

    @property
    def perimeter(self):
        return 2 * (self._width + self._height)

rectangle = Rectangle(4, 5)
print(rectangle.width)  # Output: 4
print(rectangle.height)  # Output: 5
print(rectangle.area)  # Output: 20
print(rectangle.perimeter)  # Output: 18

rectangle.width = 6
rectangle.height = 8
print(rectangle.width)  # Output: 6
print(rectangle.height)  # Output: 8
print(rectangle.area)  # Output: 48
print(rectangle.perimeter)  # Output: 28
```

### @abstractmethod

`@abstractmethod` 是一个装饰器，用于声明抽象方法。抽象方法是在基类中定义但没有具体实现的方法，它需要在派生类中进行具体的实现。

注意事项：

- 抽象方法的主要目的是定义一个接口，规定了派生类必须提供的方法。它在面向对象设计中非常有用，因为它可以确保派生类遵循特定的接口约定。
- 需要注意的是，抽象方法只能在抽象基类中定义，而不能直接实例化抽象基类。因此，抽象基类本身无法被实例化，只能被用作其他类的基类。
- 抽象基类必须继承自ABC基类，并使用 @abstractmethod 装饰器标记抽象方法。
- 派生类必须实现基类中的抽象方法，否则会引发 TypeError。

```python
# 示例：使用抽象类进行多态
from abc import ABC, abstractmethod # 第一步：导入 abc

# 第二步： 定义抽象基类
class Animal(metaclass=abc.ABCMeta):  # 同一类事物:动物
    @abc.abstractmethod
    def talk(self):
        pass

# 第三步：创建派生类并实现抽象方法
class Cat(Animal):  # 动物的形态之一:猫
    def talk(self):
        print('This is a cat')
        
class Dog(Animal):  # 动物的形态之二:狗
    def talk(self):
        print('This is a dog')


c = Cat()
d = Dog()

def func(obj):
    obj.talk()  # 同一函数名，根据对象不同实现不同方法

func(c)  # 'This is a cat'
func(d)  # 'This is a dog'
```

### @lru_cache

`@lru_cache`，来自`functools`模块，用于缓存函数的结果，以提高性能

`@lru_cache`的核心机制：

- 缓存斐波那契数列的计算结果
- 避免重复计算相同的`n`值
- 通过`cache_info()`查看缓存命中情况

```python
from functools import lru_cache

@lru_cache(maxsize=None)  # 缓存所有结果
def fib(n):
    if n < 2:
        return n
    return fib(n-1) + fib(n-2)

# 测试性能
print(fib(10))  # 首次计算，需要递归
print(fib(10))  # 直接从缓存获取结果
print(fib.cache_info())  # 查看缓存信息
```

### @wraps

`@wraps`，来自`functools`模块，用于在创建装饰器时保留函数的原始元数据

`@wraps`的核心作用：

- 装饰器`logging_decorator`在包装原始函数时使用`@wraps(func)`
- 保留了原始函数的名称 (`__name__`) 和文档字符串 (`__doc__`)
- 避免了装饰器带来的元数据丢失问题

```python
from functools import wraps

def logging_decorator(func):
    @wraps(func)  # 保留原始函数的元数据
    def wrapper(*args, **kwargs):
        print(f"调用函数: {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@logging_decorator
def add(a, b):
    """返回两个数的和"""
    return a + b

# 测试函数
print(add(3, 4))  # 输出: 7
print(add.__name__)  # 输出: add (而不是 wrapper)
print(add.__doc__)  # 输出: 返回两个数的和
```

### @singledispatch

`@singledispatch`，来自`functools`模块，用于创建单分派通用函数，根据参数类型执行不同的操作

`@singledispatch`的核心机制：

- 主函数定义默认行为
- 使用`@func.register`装饰器注册特定类型的处理函数
- 根据第一个参数的类型自动分派到对应的实现

```python
from functools import singledispatch

@singledispatch
def format_data(data):
    return f"通用格式: {data}"

@format_data.register
def _(data: int):
    return f"整数格式: {data:,}"

@format_data.register
def _(data: list):
    return f"列表格式: [{', '.join(map(str, data))}]"

# 测试不同类型的参数
print(format_data(1234567))      # 输出: 整数格式: 1,234,567
print(format_data(['a', 'b']))   # 输出: 列表格式: [a, b]
print(format_data(True))         # 输出: 通用格式: True
```

### @dataclass

`@dataclass`，来自`dataclasses`模块，用于简化创建主要用于存储数据的类

`@dataclass`的最基本用法：

- 自动生成初始化`__init__`方法
- 自动生成格式化的`__repr__`方法
- 类型提示（可选但推荐）
- 直接访问属性

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: float
    y: float

# 创建实例并打印
p = Point(3.1, 4.2)
print(p)  # 输出: Point(x=3.1, y=4.2)
print(p.x)  # 输出: 3.1
```

### @contextmanager

`@contextmanager`，来自`contextlib`模块，用于使用基于生成器的方法定义上下文管理器

`@contextmanager`的核心机制：

- 生成器函数（`yield`之前的代码作为`__enter__`，之后的代码作为`__exit__`）
- 自动处理资源清理（文件关闭）
- 异常安全（即使发生异常也会执行`finally`块）

```python
from contextlib import contextmanager

@contextmanager
def open_file(filename, mode='r'):
    f = open(filename, mode)
    try:
        yield f
    finally:
        f.close()

# 使用上下文管理器
with open_file('test.txt', 'w') as f:
    f.write('Hello, World!')

with open_file('test.txt') as f:
    print(f.read())  # 输出: Hello, World!
```



## 自定义装饰器

### 初始

```python
"""
    装饰器
"""
import random
import time


# 装饰器的一般写法（闭包）
# def decorator(func):
#     def wrapper():
#         print("我要睡觉了...")
#         func()
#         print("我要起床了...")
#     return wrapper
#
#
# def sleep():
#     print("睡眠中...")
#     time.sleep(random.randint(1, 5))
#
# fn = decorator(sleep)
# fn()

# 装饰器的快捷写法（语法糖）
def decorator(func):
    def wrapper():
        print("我要睡觉了...")
        func()
        print("我要起床了...")
    return wrapper

# 使用装饰器语法糖，在方法上添加装饰器
@decorator
def sleep():
    print("睡眠中...")
    time.sleep(random.randint(1, 5))

sleep()
```

### @timer

优化代码性能是非常重要的。@timer装饰器可以帮助我们跟踪特定函数的执行时间。通过用这个装饰器包装函数，我可以快速识别瓶颈并优化代码的关键部分，将@timer与其他装饰器结合使用，可以全面地分析代码的性能

```python
import time
 
 def timer(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"{func.__name__} took {end_time - start_time:.2f} seconds to execute.")
        return result
    return wrapper
 @timer
 def my_data_processing_function():
    # Your data processing code here
```

### @memoize

在数据科学中，我们经常使用计算成本很高的函数。@memoize装饰器帮助我缓存函数结果，避免了相同输入的冗余计算，显著加快工作流程，在递归函数中也可以使用@memoize来优化重复计算

```python
 def memoize(func):
    cache = {}
 
 def wrapper(*args):
        if args in cache:
            return cache[args]
        result = func(*args)
        cache[args] = result
        return result
    return wrapper
 @memoize
 def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

### @validate_input

数据完整性至关重要，@validate_input装饰器可以验证函数参数，确保它们在继续计算之前符合特定的标准，可以方便的使用@validate_input在数据科学项目中一致地实现数据验证

```python
 def validate_input(func):
    def wrapper(*args, **kwargs):
        # Your data validation logic here
        if valid_data:
            return func(*args, **kwargs)
        else:
            raise ValueError("Invalid data. Please check your inputs.")
 
 return wrapper
 @validate_input
 def analyze_data(data):
    # Your data analysis code here
```

### @log_results

在运行复杂的数据分析时，跟踪每个函数的输出变得至关重要。@log_results装饰器可以帮助我们记录函数的结果，以便于调试和监控，将@log_results与日志库结合使用，以获得更高级的日志功能

```python
def log_results(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        with open("results.log", "a") as log_file:
            log_file.write(f"{func.__name__} - Result: {result}\n")
        return result
 
 return wrapper
 @log_results
 def calculate_metrics(data):
    # Your metric calculation code here
```

### @suppress_errors

数据科学项目经常会遇到意想不到的错误，可能会破坏整个计算流程。@suppress_errors装饰器可以优雅地处理异常并继续执行，@suppress_errors可以避免隐藏严重错误，还可以进行错误的详细输出，便于调试

```python
 def suppress_errors(func):
    def wrapper(*args, **kwargs):
        try:
            return func(*args, **kwargs)
        except Exception as e:
            print(f"Error in {func.__name__}: {e}")
            return None
 
 return wrapper
 @suppress_errors
 def preprocess_data(data):
    # Your data preprocessing code here
```

### @retry

@retry装饰器帮助我在遇到异常时重试函数执行，确保更大的弹性

```python
 import time
 
 def retry(max_attempts, delay):
    def decorator(func):
        def wrapper(*args, **kwargs):
            attempts = 0
            while attempts < max_attempts:
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    print(f"Attempt {attempts + 1} failed. Retrying in {delay} seconds.")
                    attempts += 1
                    time.sleep(delay)
            raise Exception("Max retry attempts exceeded.")
        return wrapper
    return decorator
 @retry(max_attempts=3, delay=2)
 def fetch_data_from_api(api_url):
    # Your API data fetching code here
```

### @visualize_results

@visualize_results装饰器数据分析中自动生成漂亮的可视化结果

```python
 import matplotlib.pyplot as plt
 
 def visualize_results(func):
    def wrapper(*args, **kwargs):
        result = func(*args, **kwargs)
        plt.figure()
        # Your visualization code here
        plt.show()
        return result
    return wrapper
 @visualize_results
 def analyze_and_visualize(data):
    # Your combined analysis and visualization code here
```

### @debug

调试复杂的代码可能非常耗时。@debug装饰器可以打印函数的输入参数和它们的值，以便于调试

```python
 def debug(func):
    def wrapper(*args, **kwargs):
        print(f"Debugging {func.__name__} - args: {args}, kwargs: {kwargs}")
        return func(*args, **kwargs)
 
 return wrapper
 @debug
 def complex_data_processing(data, threshold=0.5):
    # Your complex data processing code here
```

### @deprecated

随着我们的项目更新迭代，一些函数可能会过时。@deprecated装饰器可以在一个函数不再被推荐时通知用户

```python
 import warnings
 
 def deprecated(func):
    def wrapper(*args, **kwargs):
        warnings.warn(f"{func.__name__} is deprecated and will be removed in future versions.", DeprecationWarning)
        return func(*args, **kwargs)
    return wrapper
 @deprecated
 def old_data_processing(data):
    # Your old data processing code here
```



# 设计模式

设计模式是一种编程套路，可以极大的方便程序的开发。
最常见、最经典的设计模式，就是我们所学习的面向对象了。

除了面向对象外，在编程中也有很多既定的套路可以方便开发，我们称之为设计模式：单例模式、工厂模式、建造者、责任链、状态、备忘录、解释器、访问者、观察者、中介、模板、代理模式等等

## 单例模式

单例模式（Singleton Pattern）是一种常用的软件设计模式，该模式的主要目的是确保某一个类只有一个实例存在。

在整个系统中，某个类只能出现一个实例时，单例对象就能派上用场。

- 定义：保证一个类只有一个实例，并提供一个访问它的全局访问点中
- 适用场景：当一个类只能有一个实例，而客户可以从一个众所周知的访问点访问它时

str_tools.py

```python
"""
    使用单例模式来实现字符串处理工具类
"""

class str_tools:
    pass

str_tool = str_tools()
```

main.py

```python
"""
    单例模式示例
"""

class tools:
    pass

t1 = tools()
t2 = tools()
print(t1 is t2)  # False, 不同的实例


from str_tools import str_tool

s1 = str_tool
s2 = str_tool

print(s1 is s2)  # True, 同一个实例
```

单例模式就是对一个类，只获取其唯一的类实例对象，持续复用它。

- 节省内存
- 节省创建对象的开销



## 工厂模式

当需要大量创建一个类的实例的时候，可以使用工厂模式。
即从原生的使用类的构造去创建对象的形式，改成基于工厂提供的方法去创建对象的形式。

优点：

- 大批量创建对象的时候有统一的入口，易于代码维护
- 当发生修改，仅修改工厂类的创建方法即可
- 符合现实世界的模式，即由工厂来制作产品（对象）

```python
"""
    工厂模式
"""


# 手机
class Phone:
    pass


# 电池
class Battery:
    pass


# 键盘
class Keyboard:
    pass


# 工厂类
class ElectronFactory:
    # 工厂方法，用于创建不同类型的产品
    def create_product(self, product_type):
        if product_type == 'phone':
            return Phone()
        elif product_type == 'battery':
            return Battery()
        elif product_type == 'keyboard':
            return Keyboard()
        else:
            raise ValueError(f"Unknown product type: {product_type}")


# 使用工厂类创建产品
factory = ElectronFactory()
phone = factory.create_product("phone")
battery = factory.create_product("battery")
keyboard = factory.create_product("keyboard")
print(f"{type(phone).__name__}")
print(f"{type(battery).__name__}")
print(f"{type(keyboard).__name__}")
```



# 多线程

## 进程和线程

现代操作系统比如MacOS、UNIX、Linux、Windows等，都是支持"多任务"的操作系统。
进程：就是一个程序，运行在系统之上，那么便称之这个程序为一个运行进程，并分配进程ID方便系统管理。
线程：线程是归属于进程的，一个进程可以开启多个线程，执行不同的工作，是进程的实际工作最小单位。

操作系统中可以运行多个进程，即多任务运行
一个进程内可以运行多个线程，即多线程运行

进程之间是内存隔离的，即不同的进程拥有各自的内存空间
线程之间是内存共享的，线程是属于进程的，一个进程内的多个线程之间是共享这个进程所拥有的内存空间的

## 并行执行

并行执行的意思指的是同一时间做不同的工作。

进程之间就是并行执行的，操作系统可以同时运行好多程序，这些程序都是在并行执行。

除了进程外，线程其实也是可以并行执行的。

也就是比如一个Python程序，其实是完全可以做到：

- 一个线程在输出：你好
- 一个线程在输出：Hello

一个程序在同一时间做两件乃至多件不同的事情，称之为：多线程并行执行

## subprocess模块

`subprocess` 是Python标准库中的一个模块，用于创建和管理子进程。
`subprocess` 允许你在Python程序中执行外部命令，并与这些命令进行交互。
通过 `subprocess` 模块，你可以执行系统命令、调用其他程序，并获取它们的输出或错误信息。

`subprocess.run()` 是 `subprocess` 模块中最常用的函数之一。它可以执行一个外部命令，并等待命令完成

```python
import subprocess

result = subprocess.run(['dir'], capture_output=True, text=True, shell=True)

print("标准输出：")
print(result.stdout)

print("错误输出：")
print(result.stderr)

print("返回码：", result.returncode)
```

`subprocess.Popen` 类提供了更底层的接口，允许你更灵活地控制子进程。你可以使用 `Popen` 来启动一个子进程，并在后台运行它，或者与它进行交互

```python
import subprocess

# 启动一个子进程
process = subprocess.Popen(['ping', 'www.baidu.com'], stdout=subprocess.PIPE, text=True)

# 读取子进程的输出
while True:
    output = process.stdout.readline()
    if output == '' and process.poll() is not None:
        break
    if output:
        print(output.strip())

# 获取子进程的退出状态码
return_code = process.poll()
print(f"Process finished with return code {return_code}")
```

`subprocess` 模块允许你使用管道将多个命令连接在一起。你可以将一个命令的输出作为另一个命令的输入。

```python
import subprocess

# 使用管道连接两个命令
p1 = subprocess.Popen(['dir'], stdout=subprocess.PIPE)
p2 = subprocess.Popen(['findstr', 'py'], stdin=p1.stdout, stdout=subprocess.PIPE, text=True)

# 获取最终输出
output = p2.communicate()[0]
print(output)
```

subprocess 模块核心方法

| 方法                            | 说明                         | 示例                                                         |
| :------------------------------ | :--------------------------- | :----------------------------------------------------------- |
| **`subprocess.run()`**          | 执行命令并等待完成（推荐）   | `subprocess.run(["ls", "-l"], capture_output=True, text=True)` |
| **`subprocess.Popen()`**        | 创建子进程（底层控制）       | `proc = subprocess.Popen(["ping", "google.com"], stdout=subprocess.PIPE)` |
| **`subprocess.call()`**         | 执行命令并返回退出码（旧版） | `exit_code = subprocess.call(["python", "--version"])`       |
| **`subprocess.check_call()`**   | 执行命令，失败时抛出异常     | `subprocess.check_call(["git", "commit"])`                   |
| **`subprocess.check_output()`** | 执行命令并返回输出（旧版）   | `output = subprocess.check_output(["date"], text=True)`      |

subprocess.CompletedProcess 对象属性（run() 方法的返回对象）

| 属性         | 说明                                     |
| :----------- | :--------------------------------------- |
| `args`       | 执行的命令参数列表                       |
| `returncode` | 进程退出状态码（0表示成功）              |
| `stdout`     | 标准输出内容（若设置了`capture_output`） |
| `stderr`     | 标准错误内容（若设置了`capture_output`） |

subprocess.Popen 类常用方法/属性

| 方法/属性       | 说明                                     | 示例                                              |
| :-------------- | :--------------------------------------- | :------------------------------------------------ |
| `poll()`        | 检查进程是否终止（返回`None`表示运行中） | `if proc.poll() is None: print("Running")`        |
| `wait()`        | 阻塞等待进程结束                         | `proc.wait()`                                     |
| `communicate()` | 交互式输入/输出                          | `stdout, stderr = proc.communicate(input="data")` |
| `terminate()`   | 发送终止信号（SIGTERM）                  | `proc.terminate()`                                |
| `kill()`        | 强制终止进程（SIGKILL）                  | `proc.kill()`                                     |
| `stdin`         | 进程的标准输入流                         | `proc.stdin.write("input")`                       |
| `stdout`        | 进程的标准输出流                         | `print(proc.stdout.read())`                       |
| `stderr`        | 进程的标准错误流                         | `errors = proc.stderr.read()`                     |

常用参数说明（适用于 run() 和 Popen()）

| 参数      | 说明                            | 示例值                                    |
| :-------- | :------------------------------ | :---------------------------------------- |
| `args`    | 命令（列表或字符串）            | `["ls", "-l"]` 或 `"ls -l"`               |
| `stdin`   | 标准输入配置                    | `subprocess.PIPE`（管道）、`None`（继承） |
| `stdout`  | 标准输出配置                    | `subprocess.PIPE`、`open('log.txt', 'w')` |
| `stderr`  | 标准错误配置                    | `subprocess.STDOUT`（合并到stdout）       |
| `shell`   | 是否通过Shell执行               | `True`（支持字符串命令）                  |
| `cwd`     | 工作目录路径                    | `"/tmp"`                                  |
| `env`     | 自定义环境变量                  | `{"PATH": "/usr/bin"}`                    |
| `timeout` | 超时时间（秒）                  | `30`                                      |
| `text`    | 输入/输出是否为字符串（非字节） | `True`                                    |



## threading模块

Python的多线程可以通过threading模块来实现

```python
"""
    多线程的使用
"""
import time
# 导入threading模块中的Thread类，实现多线程
from threading import Thread


def sing(msg):
    while True:
        print(msg)
        time.sleep(1)


def dance(msg):
    while True:
        print(msg)
        time.sleep(1)


if __name__ == '__main__':
    """
        Thread参数列表：
        group参数：保留用于实现ThreadGroup类时的未来扩展。
        target参数：指定线程要执行的函数名
        name参数：指定线程的名称
        args参数: 指定线程要执行的函数的参数，使用元组传递
        kwargs参数: 指定线程要执行的函数的关键字参数，使用字典传递
        daemon参数: 是否为守护线程，默认为False
    """
    t1 = Thread(target=sing, args=('在唱歌...',))
    # 启动线程
    t1.start()

    t2 = Thread(target=dance, kwargs={"msg": '在跳舞...'})
    t2.start()
```

## asyncio模块

`asyncio` 是Python标准库中的一个模块，用于编写异步 I/O 操作的代码。
asyncio提供了一种高效的方式来处理并发任务，特别适用于 I/O 密集型操作，如网络请求、文件读写等。
通过使用 `asyncio`，你可以在单线程中同时处理多个任务，而无需使用多线程或多进程。

为什么需要 asyncio？
在传统的同步编程中，当一个任务需要等待 I/O 操作（如网络请求）完成时，程序会阻塞，直到操作完成。这会导致程序的效率低下，尤其是在需要处理大量 I/O 操作时。
`asyncio` 通过引入异步编程模型，允许程序在等待 I/O 操作时继续执行其他任务，从而提高了程序的并发性和效率。

协程是 `asyncio` 的核心概念之一。它是一个特殊的函数，可以在执行过程中暂停，并在稍后恢复执行。协程通过 `async def` 关键字定义，并通过 `await` 关键字暂停执行，等待异步操作完成

```python
import asyncio

async def say_hello():
    print("Hello")
    await asyncio.sleep(1)
    print("World")
```

事件循环是 `asyncio` 的核心组件，负责调度和执行协程。它不断地检查是否有任务需要执行，并在任务完成后调用相应的回调函数

```python
async def main():
    await say_hello()

asyncio.run(main())
```

任务是对协程的封装，表示一个正在执行或将要执行的协程。你可以通过 `asyncio.create_task()` 函数创建任务，并将其添加到事件循环中

```python
async def main():
    task = asyncio.create_task(say_hello())
    await task
```

`Future` 是一个表示异步操作结果的对象。它通常用于底层 API，表示一个尚未完成的操作。你可以通过 `await` 关键字等待 `Future` 完成

```python
async def main():
    future = asyncio.Future()
    await future
```

要运行一个协程，你可以使用 `asyncio.run()` 函数。它会创建一个事件循环，并运行指定的协程

```python
import asyncio

async def main():
    print("Start")
    await asyncio.sleep(1)
    print("End")

asyncio.run(main())
```

使用 `asyncio.gather()` 函数并发执行多个协程，并等待它们全部完成

```python
import asyncio

async def task1():
    print("Task 1 started")
    await asyncio.sleep(1)
    print("Task 1 finished")

async def task2():
    print("Task 2 started")
    await asyncio.sleep(2)
    print("Task 2 finished")

async def main():
    await asyncio.gather(task1(), task2())

asyncio.run(main())
```

使用 `asyncio.wait_for()` 函数为协程设置超时时间。如果协程在指定时间内未完成，将引发 `asyncio.TimeoutError` 异常

```python
import asyncio

async def long_task():
    await asyncio.sleep(10)
    print("Task finished")

async def main():
    try:
        await asyncio.wait_for(long_task(), timeout=5)
    except asyncio.TimeoutError:
        print("Task timed out")

asyncio.run(main())
```

使用异步队列

```python
async def producer(queue):
    for i in range(5):
        await queue.put(i)
        await asyncio.sleep(0.1)

async def consumer(queue):
    while True:
        item = await queue.get()
        print(f"Consumed {item}")
        queue.task_done()

async def main():
    queue = asyncio.Queue()
    await asyncio.gather(
        producer(queue),
        consumer(queue)
    )
```

`asyncio` 特别适用于以下场景：

- **网络请求**：如 HTTP 请求、WebSocket 通信等。
- **文件 I/O**：如异步读写文件。
- **数据库操作**：如异步访问数据库。
- **实时数据处理**：如实时消息队列处理。

**核心函数**

| 方法/函数                       | 说明                          | 示例                                                 |
| :------------------------------ | :---------------------------- | :--------------------------------------------------- |
| **`asyncio.run(coro)`**         | 运行异步主函数（Python 3.7+） | `asyncio.run(main())`                                |
| **`asyncio.create_task(coro)`** | 创建任务并加入事件循环        | `task = asyncio.create_task(fetch_data())`           |
| **`asyncio.gather(\*coros)`**   | 并发运行多个协程              | `await asyncio.gather(task1, task2)`                 |
| **`asyncio.sleep(delay)`**      | 异步等待（非阻塞）            | `await asyncio.sleep(1)`                             |
| **`asyncio.wait(coros)`**       | 控制任务完成方式              | `done, pending = await asyncio.wait([task1, task2])` |

**事件循环（Event Loop）**

| 方法                                   | 说明                 | 示例                              |
| :------------------------------------- | :------------------- | :-------------------------------- |
| **`loop.run_until_complete(future)`**  | 运行直到任务完成     | `loop.run_until_complete(main())` |
| **`loop.run_forever()`**               | 永久运行事件循环     | `loop.run_forever()`              |
| **`loop.stop()`**                      | 停止事件循环         | `loop.stop()`                     |
| **`loop.close()`**                     | 关闭事件循环         | `loop.close()`                    |
| **`loop.call_soon(callback)`**         | 安排回调函数立即执行 | `loop.call_soon(print, "Hello")`  |
| **`loop.call_later(delay, callback)`** | 延迟执行回调         | `loop.call_later(5, callback)`    |

**协程（Coroutine）与任务（Task）**

| 方法/装饰器              | 说明                               | 示例                                   |
| :----------------------- | :--------------------------------- | :------------------------------------- |
| **`@asyncio.coroutine`** | 协程装饰器（旧版，Python 3.4-3.7） | `@asyncio.coroutine` `def old_coro():` |
| **`async def`**          | 定义协程（Python 3.5+）            | `async def fetch():`                   |
| **`task.cancel()`**      | 取消任务                           | `task.cancel()`                        |
| **`task.done()`**        | 检查任务是否完成                   | `if task.done():`                      |
| **`task.result()`**      | 获取任务结果（需任务完成）         | `data = task.result()`                 |

**同步原语（类似`threading`）**

| 类                        | 说明       | 示例                                              |
| :------------------------ | :--------- | :------------------------------------------------ |
| **`asyncio.Lock()`**      | 异步互斥锁 | `lock = asyncio.Lock()` `async with lock:`        |
| **`asyncio.Event()`**     | 事件通知   | `event = asyncio.Event()` `await event.wait()`    |
| **`asyncio.Queue()`**     | 异步队列   | `queue = asyncio.Queue()` `await queue.put(item)` |
| **`asyncio.Semaphore()`** | 信号量     | `sem = asyncio.Semaphore(5)` `async with sem:`    |

**网络与子进程**

| 方法/类                                | 说明          | 示例                                                         |
| :------------------------------------- | :------------ | :----------------------------------------------------------- |
| **`asyncio.open_connection()`**        | 建立TCP连接   | `reader, writer = await asyncio.open_connection('host', 80)` |
| **`asyncio.start_server()`**           | 创建TCP服务器 | `server = await asyncio.start_server(handle, '0.0.0.0', 8888)` |
| **`asyncio.create_subprocess_exec()`** | 创建子进程    | `proc = await asyncio.create_subprocess_exec('ls')`          |

**实用工具**

| 方法                                  | 说明             | 示例                                   |
| :------------------------------------ | :--------------- | :------------------------------------- |
| **`asyncio.current_task()`**          | 获取当前任务     | `task = asyncio.current_task()`        |
| **`asyncio.all_tasks()`**             | 获取所有任务     | `tasks = asyncio.all_tasks()`          |
| **`asyncio.shield(coro)`**            | 保护任务不被取消 | `await asyncio.shield(critical_task)`  |
| **`asyncio.wait_for(coro, timeout)`** | 带超时的等待     | `try: await asyncio.wait_for(task, 5)` |

## queue模块

在 Python 中，`queue` 模块提供了一个线程安全的队列实现，用于在多线程编程中安全地传递数据。
队列是一种先进先出（FIFO）的数据结构，`queue` 模块提供了多种队列类型，包括 `Queue`、`LifoQueue` 和 `PriorityQueue`，以满足不同的需求。

`Queue` 是 `queue` 模块中最常用的队列类型，它实现了标准的先进先出（FIFO）队列

```python
import queue

# 创建一个队列
q = queue.Queue()

# 向队列中添加元素
q.put(1)
q.put(2)
q.put(3)

# 从队列中获取元素
print(q.get())  # 输出: 1
print(q.get())  # 输出: 2
print(q.get())  # 输出: 3
```

`LifoQueue` 是一种后进先出（LIFO）的队列，类似于栈

```python
import queue

# 创建一个 LIFO 队列
q = queue.LifoQueue()

# 向队列中添加元素
q.put(1)
q.put(2)
q.put(3)

# 从队列中获取元素
print(q.get())  # 输出: 3
print(q.get())  # 输出: 2
print(q.get())  # 输出: 1
```

`PriorityQueue` 是一种优先级队列，元素按照优先级顺序被取出

```python
import queue

# 创建一个优先级队列
q = queue.PriorityQueue()

# 向队列中添加元素，元素为元组 (优先级, 数据)
q.put((3, 'Low priority'))
q.put((1, 'High priority'))
q.put((2, 'Medium priority'))

# 从队列中获取元素
print(q.get())  # 输出: (1, 'High priority')
print(q.get())  # 输出: (2, 'Medium priority')
print(q.get())  # 输出: (3, 'Low priority')
```

**常用方法**

`put(item, block=True, timeout=None)`：将 `item` 放入队列。如果 `block` 为 `True` 且队列已满，则等待 `timeout` 秒，直到队列有空闲空间。如果 `timeout` 为 `None`，则无限等待。

`get(block=True, timeout=None)`：从队列中获取并移除一个元素。如果 `block` 为 `True` 且队列为空，则等待 `timeout` 秒，直到队列中有元素。如果 `timeout` 为 `None`，则无限等待。

`qsize()`：返回队列中的元素数量。

`empty()`：如果队列为空，返回 `True`，否则返回 `False`。

`full()`：如果队列已满，返回 `True`，否则返回 `False`。

使用 `Queue` 在多线程之间传递数据的示例

```python
import queue
import threading
import time

# 创建一个队列
q = queue.Queue()

# 生产者线程
def producer():
    for i in range(5):
        print(f'生产 {i}')
        q.put(i)
        time.sleep(1)

# 消费者线程
def consumer():
    while True:
        item = q.get()
        if item is None:
            break
        print(f'消费 {item}')
        q.task_done()

# 启动生产者线程
producer_thread = threading.Thread(target=producer)
producer_thread.start()

# 启动消费者线程
consumer_thread = threading.Thread(target=consumer)
consumer_thread.start()

# 等待生产者线程完成
producer_thread.join()

# 等待队列中的所有任务完成
q.join()

# 发送结束信号
q.put(None)
consumer_thread.join()
```

**queue 模块核心类**

| 类                        | 说明                            | 适用场景             |
| :------------------------ | :------------------------------ | :------------------- |
| **`queue.Queue`**         | 先进先出（FIFO）队列            | 通用任务队列         |
| **`queue.LifoQueue`**     | 后进先出（LIFO）队列（类似栈）  | 需要后进先出的场景   |
| **`queue.PriorityQueue`** | 优先级队列（最小堆实现）        | 按优先级处理任务     |
| **`queue.SimpleQueue`**   | 更简单的FIFO队列（Python 3.7+） | 不需要高级功能的场景 |

**通用方法（所有队列类都支持）**

| 方法              | 说明                         | 示例               | 返回值         |
| :---------------- | :--------------------------- | :----------------- | :------------- |
| **`put(item)`**   | 放入元素                     | `q.put("task1")`   | None           |
| **`get()`**       | 取出并移除元素               | `item = q.get()`   | 队列元素       |
| **`empty()`**     | 判断队列是否为空             | `if q.empty():`    | `True`/`False` |
| **`full()`**      | 判断队列是否已满             | `if q.full():`     | `True`/`False` |
| **`qsize()`**     | 返回队列当前大小             | `size = q.qsize()` | 整数           |
| **`task_done()`** | 标记任务完成（用于`join()`） | `q.task_done()`    | None           |
| **`join()`**      | 阻塞直到所有任务完成         | `q.join()`         | None           |

**阻塞控制参数**

| 参数      | 说明                    | 默认值 | 示例                  |
| :-------- | :---------------------- | :----- | :-------------------- |
| `block`   | 当队列为空/满时是否阻塞 | `True` | `q.get(block=False)`  |
| `timeout` | 阻塞超时时间（秒）      | `None` | `q.put(x, timeout=5)` |

生产者-消费者模型

```python
import queue, threading

q = queue.Queue(maxsize=3)  # 容量为3的队列

def producer():
    for i in range(5):
        q.put(f"Task-{i}")
        print(f"Produced: Task-{i}")

def consumer():
    while True:
        item = q.get()
        print(f"Consumed: {item}")
        q.task_done()

threading.Thread(target=producer, daemon=True).start()
threading.Thread(target=consumer, daemon=True).start()
q.join()  # 等待所有任务完成
```

优先级任务处理

```python
pq = queue.PriorityQueue()
pq.put((3, "Scan"))
pq.put((1, "Emergency"))
pq.put((2, "Log"))

while not pq.empty():
    print(pq.get()[1])  # 输出顺序: Emergency → Log → Scan
```

# 网络编程

socket（简称套接字）是进程之间通信一个工具，好比现实生活中的插座，所有的家用电器要想工作都是基于插座进行，进程之间想要进行网络通信需要socket。
Socket负责进程之间的网络数据传输，好比数据的搬运工。

2个进程之间通过Socket进行相互通讯，就必须有服务端和客户端
Socket服务端：等待其它进程的连接、可接受发来的消息、可以回复消息
Socket客户端：主动连接服务端、可以发送消息、可以接收回复

## Socket服务端

```python
"""
    服务端
"""
import socket

# 创建Socket对象
server_socket = socket.socket()

# 绑定iр地址和端口
server_socket.bind(("127.0.0.1", 8888))

# 监听端口 通过listen方法设置监听数量
server_socket.listen(1)

# 等待客户端链接 通过accept方法(阻塞方法)，返回是一个二元元组，可以通过元素1,元素2 = server_socket.accept()的方式直接获取元组中的元素
# result = server_socket.accept()
# conn = result[0]  # 客户端和服务端链接对象
# addr = result[1]  # 客户端地址信息
conn, addr = server_socket.accept()
print(f"客户端已连接，地址信息：{addr}")

while True:
    # 接受客户端信息
    # 接收数据，recv参数是缓冲区大小,recv返回的是字节类型数据，可以通过decode方法转换为字符串
    data = conn.recv(1024).decode("utf-8")
    print(data)

    # 发送回复消息 send也是接受字节类型数据，发送数据前需要将字符串转换为字节类型
    msg = input("请输入回复消息：")

    if msg == "exit":
        print("服务端已退出")
        break

    conn.send(msg.encode("utf-8"))

# 关闭链接
conn.close()
server_socket.close()
```



## Socket客户端

```python
"""
    客户端
"""

import socket

# 创建Socket对象
client_socket = socket.socket()
# 连接服务端
client_socket.connect(("127.0.0.1", 8888))
while True:
    msg = input("请输入消息（输入exit退出）：")
    if msg.lower() == "exit":
        print("客户端已退出")
        break
    # 发送消息
    client_socket.send(msg.encode("utf-8"))

    # 接收服务端回复消息
    data = client_socket.recv(1024)
    print(f"服务端回复消息：{data.decode('utf-8')}")

# 关闭链接
client_socket.close()
```



# 正则表达式

正则表达式，又称规则表达式（Regular Expression)，是使用单个字符串来描述、匹配某个句法规则的字符串，常被用来检索、替换那些符合某个模式（规则）的文本。

简单来说，正则表达式就是使用：字符串定义规则，并通过规则去验证字符串是否匹配
比如，验证一个字符串是否是符合条件的电子邮箱地址，只需要配置好正则规则，即可匹配任意邮箱
比如通过正则规则：(^[\w-]+(\-[\w-1+)*@[\w-]+(\.[\w-]+)+$)即可匹配一个字符串是否是标准邮箱格式

Python正则表达式，使用re模块，并基于re模块中三个基础方法来做正则匹配
分别是：match、search、findall三个基础方法

match(匹配规则，被匹配字符串)
从被匹配字符串开头进行匹配，匹配成功返回匹配对象（包含匹配的信息），匹配不成功返回空

```python
"""
    正则表达式
"""
import re

# match从头匹配
str = "1python is a programming language python python"
result = re.match("python", str)
print(result)
print(result.group())
print(result.span())
```

search(匹配规则，被匹配字符串)
搜索整个字符串，找出匹配的。从前向后，找到第一个后，就停止，不会继续向后

```python
"""
    正则表达式
"""
import re

# search搜索匹配
str = "1python is a programming language python python"
result = re.search("python", str)
print(result)
print(result.group())
print(result.span())
```

findall(匹配规则，被匹配字符串)
匹配整个字符串，找出全部匹配项

```python
"""
    正则表达式
"""
import re

# findall搜索全部匹配
str = "1python is a programming language python python"
result = re.findall("python", str)
print(result)
```

正则最强大的功能在于元字符匹配规则

单字符匹配：

| 字符 | 功能                                      |
| ---- | ----------------------------------------- |
| .    | 匹配任意1个字符（除了\n），`\.`匹配点本身 |
| []   | 匹配[]中列举的字符                        |
| \d   | 匹配数字，即0-9                           |
| \D   | 匹配非数字                                |
| \s   | 匹配空白，即空格、tab键                   |
| \S   | 匹配非空白                                |
| \w   | 匹配单词字符，即a-z、A-Z、0-9、_          |
| \W   | 匹配非单词字符                            |

数量匹配：

| 字符  | 功能                              |
| ----- | --------------------------------- |
| *     | 匹配前一个规则的字符出现0至无数次 |
| +     | 匹配前一个规则的字符出现1至无数次 |
| ?     | 匹配前一个规则的字符出现0或1次    |
| {m}   | 匹配前一个规则的字符出现m次       |
| {m,}  | 匹配前一个规则的字符出现最少m次   |
| {m,n} | 匹配前一个规则的字符出现m到n次    |

边界匹配：

| 字符 | 功能               |
| ---- | ------------------ |
| ^    | 匹配字符串开头     |
| $    | 匹配字符串结尾     |
| \b   | 匹配一个单词的边界 |
| \B   | 匹配非单词边界     |

分组匹配：

| 字符 | 功能                     |
| ---- | ------------------------ |
| \|   | 匹配左右任意一个表达式   |
| ()   | 将括号中字符作为一个分组 |

```python
"""
    元字符匹配
"""
import re

str = "1python is a programming 222 language python 333 python"
# 匹配数字
result = re.findall(r"\d",str) # 字符串前面带上r的标记，表示字符串中转义字符无效，就是普通字符的意思
print(result)

# 匹配账号，只能由字母和数字组成，长度限制6到10位
account = input("请输入账号（6-10位字母或数字）：")
result = re.match(r"^[a-zA-Z0-9]{6,10}$", account)
print(result)

# 匹配QQ号，要求纯数字，长度5-11，第一位不为0
qq = input("请输入QQ号（5-11位纯数字，第一位不为0）：")
result = re.match(r"^[1-9][0-9]{4,10}$", qq)
print(result)

# 匹配邮箱地址，只允许qq、163、gmail这三种邮箱地址
# {内容}.{内容}@{内容}.{内容}
email = input("请输入邮箱地址（qq、163、gmail）：")
result = re.match(r"^[a-zA-Z0-9_.+-]+@(qq|163|gmail)\.com$", email)
print(result)
```



# 递归

递归在编程中是一种非常重要的算法
递归：即方法（函数）自己调用自己的一种特殊编程写法
最典型的递归场景为找出一个文件夹中全部的文件

```python
"""
    演示Python递归操作
    需求：通过递归，找出一个指定文件夹内的全部文件
    思路：写一个函数，列出文件夹内的全部内容，如果是文件就收集到几1st
    如果是文件夹，就递归调用自己，再次判断。
"""

import os


# 列出指定文件夹内的全部文件
# print(os.listdir("E:/apache-tomcat-9.0.62"))
# 判断指定路径是否是文件夹
# print(os.path.isdir("E:/apache-tomcat-9.0.62"))
# 判断指定路径是否存在
# print(os.path.exists("E:/apache-tomcat-9.0.62"))


def get_files_recursion_from_dir(path):
    """
        从指定文件夹中使用递归的方式找到改文件夹内所有的文件
    :param path: 指定文件夹路径
    :return: 返回该文件夹内所有的文件列表
    """
    if not os.path.exists(path):
        print("指定路径不存在")
        return []

    file_list = []
    for file in os.listdir(path):
        new_path = path + "/" + file
        if os.path.isdir(new_path):
            # 如果是文件夹，则递归调用
            file_list += get_files_recursion_from_dir(new_path)
        else:
            file_list.append(new_path)

    return file_list


if __name__ == '__main__':
    file_list = get_files_recursion_from_dir("E:/apache-tomcat-9.0.62")
    print(file_list)
```



# tqdm

## 介绍

显示循环的进度条的库。taqadum, تقدّم）在阿拉伯语中的意思是进展。tqdm可以在长循环中添加一个进度提示信息，用户只需要封装任意的迭代器 tqdm(iterator），是一个快速、扩展性强的进度条工具库。

官方文档：https://tqdm.github.io/



## 为什么需要进度条？

想象一下，假如你在下载一个大文件，或者在进行一些需要大量计算的任务，程序没有进度条，你就只能等待，完全不知道程序是不是还在运行，或者是否卡住了。这种情况不仅让人焦虑，而且还会降低程序的用户体验。

进度条就像是一个"提示器"，告诉你当前任务的进度。它能帮助你判断程序是否正常运行，是否已经接近完成。



## 安装tqdm

```
pip install tqdm
```



## 基本用法

```python
from tqdm import tqdm
import time

# 模拟一个耗时的任务
for i in tqdm(range(100)):
    time.sleep(0.1)  # 每次暂停0.1秒，模拟任务执行
```

在这个例子中，`tqdm(range(100))`会生成一个带有进度条的`range`对象。当程序执行时，你会看到类似于以下的进度条：

```
100%|██████████| 100/100 [00:10<00:00,  9.86it/s]
...
...
...
```

每次循环时，进度条会自动更新，直到完成。



## 自定义进度条

除了默认的进度条样式，`tqdm`还支持自定义进度条的各种参数。比如，你可以自定义进度条的描述信息、进度条的长度等等。来看一个例子：

```python
from tqdm import tqdm
import time

# 自定义进度条
for i in tqdm(range(100), desc="处理数据", ncols=100, bar_format="{l_bar}{bar}| {n_fmt}/{total_fmt}"):
    time.sleep(0.1)
```

在这个例子中，我们给进度条添加了描述信息`desc="处理数据"`，并且设置了进度条的宽度`ncols=100`。`bar_format`参数让你可以定制进度条的格式。

**bar_format参数详解**

`{l_bar}`

这个部分表示进度条的左侧区域。`l_bar`是`tqdm`定义的一个占位符，用来显示一些与进度相关的信息，通常包括进度条的描述、已完成的数量等。

举个例子，如果你用`desc="处理数据"`，`{l_bar}`就会显示为"处理数据"。如果不指定描述，`{l_bar}`会保持为空。

`{bar}`

`{bar}`是进度条的核心部分，它表示实际的进度条图形。通常，这部分会显示一段由`█`或`#`字符组成的进度条，显示任务的完成比例。

比如，当任务完成50%时，`{bar}`会显示一半的进度条。进度条的长度和显示的字符数是自动调整的，适应不同的终端大小。

`{n_fmt}`

这个部分表示当前已经完成的任务数量，并且会格式化成你希望的样式。例如，`{n_fmt}`会显示“50”或“500”，表示当前完成的数量。

它会根据任务的实际进度自动更新，通常用于显示"当前进度/总进度"的形式。

`{total_fmt}`

`{total_fmt}`表示总的任务数量。它通常显示为任务的总数，比如“100”或“500”，表示任务的总量。

总的任务数量一般不会改变，除非任务总数被动态调整。



## 进度条与多线程

如果你的任务是多线程的，进度条的更新可能会有些问题。幸运的是，`tqdm`支持在多线程中使用进度条。这里我们需要使用`tqdm`的`concurrent`模块：

```python
from tqdm.contrib.concurrent import thread_map
import time

def task(x):
    time.sleep(0.1)
    return x

# 使用多线程并且显示进度条
result = thread_map(task, range(100), max_workers=10)
```



## 文件下载进度条

进度条不仅仅用于循环，它还能和其他功能结合使用，比如文件下载、批量处理等。

假设我们要下载一个文件，`tqdm`可以帮助我们展示下载进度：

```python
import requests
from tqdm import tqdm

url = "https://example.com/largefile.zip"
response = requests.get(url, stream=True)

# 获取文件大小
file_size = int(response.headers.get('Content-Length', 0))

# 使用进度条下载文件
with open('largefile.zip', 'wb') as f, tqdm(
    desc="下载中",
    total=file_size,
    unit='B',
    unit_scale=True
) as bar:
    for chunk in response.iter_content(chunk_size=1024):
        f.write(chunk)
        bar.update(len(chunk))
```

在这个例子中，我们通过`Content-Length`获取文件大小，并用`tqdm`实时更新下载进度。

# 虚拟环境

## 初始

Python 虚拟环境是一种隔离的环境，它允许你在同一台机器上安装不同版本的 Python 包，甚至不同版本的 Python 解释器，而不会相互干扰。每个虚拟环境都有自己独立的 Python 解释器和库安装目录，与系统全局的 Python 环境完全分离。

- **依赖隔离**：不同项目可能需要不同版本的同一个包，虚拟环境可以让每个项目使用自己需要的版本，避免版本冲突。
- **项目可重现、可移植性**：可以通过`requirements.txt`文件记录项目依赖，其他人可以轻松安装相同的依赖版本，确保项目在不同环境中运行一致。
- **系统保护**：防止全局安装的包被意外修改或删除，影响其他项目或系统功能。
- **测试不同版本**：可以为不同版本的 Python 创建虚拟环境，测试项目在不同 Python 版本下的兼容性。
- **开发自由度**：开发者可以在不影响系统 Python 的情况下尝试新包或新版本，无需担心破坏现有环境。
- **便于管理项目依赖**：虚拟环境通常结合`requirements.txt`文件使用，这样可以方便地记录和管理项目的所有依赖，其他开发者可以使用相同的环境设置。

虚拟环境的核心是创建一个独立的 Python 环境副本，它主要做了以下几件事：

- 复制 Python 解释器到虚拟环境目录
- 创建独立的 site-packages 目录用于安装包
- 修改 PATH 环境变量，使虚拟环境的 Python 优先被使用
- 提供激活 / 退出机制来切换环境

通过这种方式，不同虚拟环境中的包安装和更新不会影响其他环境，也不会影响系统 Python。

Python 有多种创建虚拟环境的工具，最常用的包括：

**venv**：Python 3.3+ 内置的标准库，无需额外安装，轻量级
**virtualenv**：第三方工具，功能比 `venv` 更丰富（如支持 Python 2），创建速度更快
**conda**：跨语言的环境和包管理器，支持 Python、R、C++ 等，自动解决依赖冲突，**主要用于数据科学、机器学习和科学计算领域**
**pipenv**：集成 `pip` 和 `virtualenv`，自动管理 `Pipfile` 和依赖锁文件（`Pipfile.lock`）
**poetry**：专注于依赖管理和打包发布，支持语义化版本控制和项目模板

## venv

`venv` 是 Python 3.3 及以上版本内置的标准库，用于创建轻量级的"虚拟环境"。它提供了一个独立的 Python 环境，包含自己的 Python 解释器和包安装目录，与系统全局 Python 环境隔离。

创建虚拟环境

```shell
# 基本语法：python -m venv <环境名称>
python -m venv myenv
```

激活虚拟环境

```shell
# Windows
myenv\Scripts\activate.bat

# Linux/macOS
source myenv/bin/activate

# 激活后，命令行会显示环境名称（如 (myenv) $）
```

使用虚拟环境

```shell
# 安装依赖（仅影响当前环境）
pip install 依赖名

# 删除依赖
pip uninstall 依赖名

# 查看已安装的包
pip list

# 运行 Python 脚本
python my_script.py
```

退出虚拟环境

```shell
deactivate
```

删除虚拟环境，直接删除环境目录即可

```shell
# Windows
rmdir /s myenv

# Linux/macOS
rm -r myenv
```

**使用 requirements.txt 管理依赖**

```shell
# 导出依赖
pip freeze > requirements.txt

# 安装依赖
pip install -r requirements.txt
```



## uv

uv 是由 Astral（Ruff 的开发者）推出的高性能 Python 包和项目管理工具，基于 Rust 编写，旨在以单一工具替代 `pip`、`poetry`、`virtualenv`、`pyenv` 等多个工具。其核心优势包括：

- **极快的速度**：比 `pip` 快 10-100 倍，依赖解析和安装效率显著提升。
- **一站式功能**：集成包管理、虚拟环境创建、Python 版本管理、项目构建发布等功能。
- **跨平台支持**：兼容 macOS、Linux 和 Windows，安装无需 Rust 或 Python 环境。

官方文档：https://docs.astral.sh/uv/

通过pip安装uv

```shell
pip install uv
```

官方一键安装

```shell
# macOS/Linux：
curl -LsSf https://astral.sh/uv/install.sh | sh
# Windows（PowerShell）：
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"  
```

创建虚拟环境

```shell
# 为已有项目进行初始化
uv init .
# 使用uv创建项目
uv init 项目名
```

管理 Python 版本与虚拟环境

```shell
# 管理python版本
uv python list

# 安装多个 Python 版本  
uv python install 3.10 3.12  

# 为当前项目锁定 Python 3.12  
uv python pin 3.12  

# 创建指定 Python 版本的虚拟环境  
uv venv --python 3.12.0  

# 激活环境（自动生成激活命令）  
source .venv/bin/activate  # Linux/macOS  
.venv\Scripts\activate     # Windows
```

**使用 requirements.txt 管理依赖**

```shell
# 导出依赖
uv pip freeze > requirements.txt

# 安装依赖
uv add -r requirements.txt
```

使用虚拟环境

```shell
# 运行项目
uv run 程序文件名 [命令行参数]

# 添加依赖（自动创建 .venv 虚拟环境）  
uv add 依赖名
# 指定具体版本添加依赖
uv add requests==版本号

# 删除依赖
uv remove 依赖名

# 一键同步环境（使用uv管理的项目，可以使用以下命令进行同步依赖）
uv sync
```

修改uv下载依赖镜像，在环境变量中添加UV_DEFAULT_INDEX，值为镜像源地址

```shell
UV_DEFAULT_INDEX="https://mirrors.cloud.tencent.com/pypi/simple"
```

项目级别修改镜像

```shell
# 在 pyproject.toml 中添加：
[[tool.uv.index]]
url = "https://pypi.tuna.tsinghua.edu.cn/simple"
default = true

# 或在 uv.toml 中添加：
[[index]]
url = "https://pypi.tuna.tsinghua.edu.cn/simple"
default = true
```



## conda

Conda 是一个开源的跨平台包管理系统和环境管理系统，由 Anaconda 开发并维护。它最初专为 Python 设计，但现在支持多种语言（如 R、Ruby、Scala 等），主要用于数据科学、机器学习和科学计算领域。

官网网站：https://www.anaconda.com/

Conda 的核心优势：

- **跨语言支持**：不仅管理 Python 包，还能管理 R、Java、C++ 等语言的依赖
- **环境隔离**：轻松创建、复制和切换不同项目的环境
- **依赖自动解析**：智能处理复杂的依赖关系，避免版本冲突
- **平台兼容**：无缝支持 Windows、macOS 和 Linux
- **高性能安装**：优化的二进制包管理，安装速度快

Conda 的两种发行版

1. **Anaconda**：
    - 包含约 250 个科学计算包（如 NumPy、Pandas、Matplotlib）
    - 适合初学者或需要完整数据科学工具链的用户
    - 安装包较大（约 3GB）
2. **Miniconda**：
    - 仅包含 Conda 和 Python
    - 适合需要精简环境的用户
    - 按需安装所需包
    - 安装包较小（约 50MB）

安装 Anaconda

```shell
# macOS/Linux（sh/pkg结尾）
https://repo.anaconda.com/archive/

# Windows（exe结尾）
https://repo.anaconda.com/archive/

# 清华大学镜像站下载地址，包含的版本信息如下：
# Anaconda-1.x：早期版本，主要基于 Python 2.x（2015 年之前），现已停止更新。
# Anaconda2-x.x：明确基于Python 2.x的系列，例如Anaconda2-5.3.1等，因 Python 2 在 2020 年停止官方支持，该系列已不再维护。
# Anaconda3-x.x：基于Python 3.x的系列，例如Anaconda3-2025.06-1等，是目前的主流版本，持续更新。
# 下载Anaconda3-x.x版本即可
https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/

# 安装时请勾选(Add Anaconda3 to my PATH environment variable)将anaconda添加到系统环境变量中，安装完成后，打开终端并验证
conda --version
```

创建虚拟环境

```shell
# 创建名为 myenv 的环境，指定 Python 版本
conda create -n myenv python=3.10.10

# 使用镜像创建环境
conda create -n myenv python=3.10.10 -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

# 创建包含特定包的环境
conda create -n myenv numpy pandas matplotlib python=3.10.10 -c https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

# 复制现有环境
conda create -n myenv_copy --clone myenv
```

激活 / 退出环境

```shell
# 激活环境
conda activate myenv

# 退出环境
conda deactivate
```

管理环境

```shell
# 列出所有环境
conda env list

# 删除环境
conda env remove -n myenv

# 导出环境配置
conda env export > environment.yml

# 从配置文件创建环境
conda env create -f environment.yml
```

管理包

```shell
# 安装包
conda install numpy pandas

# 指定包版本
conda install numpy=1.21.5

# 从特定渠道安装
conda install -c conda-forge scikit-learn

# 更新包
conda update numpy

# 更新所有包
conda update --all

# 卸载包
conda remove numpy

# 搜索包
conda search tensorflow

# 列出当前环境的所有包
conda list
```

管理 Python 版本

```shell
# 在现有环境中切换 Python 版本
conda install python=3.10

# 创建指定 Python 版本的环境
conda create -n py310 python=3.10
```

使用虚拟环境运行脚本

```shell
# 不激活环境直接运行脚本
conda run -n myenv python my_script.py

# 执行单行命令
conda run -n myenv pip list
```

**使用镜像源加速下载**

```shell
# 清华镜像
# 添加通道
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
# 删除通道
conda config --remove channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
# 查看配置
conda config --get
conda config --show
```

**更新 Conda**

```shell
conda update -n base -c defaults conda
```

