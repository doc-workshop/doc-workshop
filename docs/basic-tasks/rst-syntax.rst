RST 基本语法
============

reStructuredText（简称 RST）是一种轻量级标记语言，广泛用于 Python 生态及其文档编写。RST 语法简洁，支持丰富的排版格式，适合编写技术文档和说明书。

本阶段你将学习：

.. contents::
  :local:
  :depth: 2 
 

学习过程中，可使用下面的在线工具进行练习：

.. raw:: html

   <iframe src="https://rsted.info.ucl.ac.be/" 
           width="100%" 
           height="600px" 
           style="border:1px solid #ccc; border-radius: 4px;">
   </iframe>


段落
----------

段落是 RST 文档中最基本的块，由一个或多个空行分隔。在写 RST 文档时，请注意缩进。


内联格式
------------

什么是内联格式呢？内联格式是指在文本中使用特殊符号来指定格式，而不会影响文本的结构。

在 RST 中，可通过特殊符号来指定内联格式。常用的特殊符号包括：

- 星号（*）：斜体
- 双星号（**）：粗体
- 反引号（`）：字面量
- 波浪线（~）：删除线
- 下划线（_）：下划线
- 等号（=）：标题


斜体
^^^^^^

在 RST 中，可以使用单个星号来将文本显示为斜体。

语法：

.. code-block:: rst

  *text*

渲染结果：

*text*


粗体
^^^^

在 RST 中，可以使用双星号来将文本显示为加粗。

语法：

.. code-block:: rst

  **text**

渲染结果：

**text**


字面量
^^^^^^^

你可以使用双引号来将文本显示为字面量，以指示代码片段、变量名、UI 元素等。

语法：

.. code-block:: rst

  ``code``

渲染结果：

``code``


标题和标题级别
-------------------

标题级别由标题的排列顺序自动确定，因此无需为特定字符分配固定的级别。然而，在项目中保持统一的约定有助于维护一致性。推荐遵循如下规范：

- ``=``，用于表示「节」（sections）
- ``-``，用于表示「小节」（subsections）
- ``^``，用于表示「子小节」（subsubsections）
- ``"``，用于表示「段落」（paragraphs）

列表
-----

使用列表对有序或无序事件进行说明

无序列表
^^^^^^^^^^^^^^

语法和示例：

.. code-block:: rst

  - 每个列表项以符号和空格开头。
  - 可使用的符号包括 ``-``、``*``、``+`` 等。

渲染效果：

- 每个列表项以符号和空格开头。
- 可使用的符号包括 ``-``、``*``、``+`` 等。

有序列表
^^^^^^^^^^^^^^

语法与示例：

.. code-block:: rst

    1. 每个编号列表项以数字或字母、点号和空格开头。
    2. 可使用的符号包括 1、A、i、(1) 等。

渲染效果：

1. 每个编号列表项以数字或字母、点号和空格开头。
2. 可使用的符号包括 1、A、i、(1) 等。

代码块
-----------

代码块由 ``code-block`` 指令和实际代码组成。为与其他代码库保持一致，代码部分通常缩进四个空格。对于 Python、C、Bash 等编程语言，关键字会默认高亮显示。下面以 Python 语言为例进行说明。

语法与示例：

.. code-block:: rst

  .. code-block:: python

      for i in range(10):
          print(i)

渲染效果：

.. code-block:: python

    for i in range(10):
        print(i)

更多内容，见 `RST 代码块 <https://docs.anaconda.com/restructuredtext/detailed/#code-blocks>`_。

索引 (Index) 文件
-------------------

索引文件使用 toctree 指令创建跨文件的目录。Sphinx 编译文档时，安装 index.rst 中索引的文件进行编译。所以，如果项目中存在 RST 文档，且希望被编译出来，则必须放在 index.rst 文件中。

语法与示例：

.. code-block:: rst

    .. toctree::
    :hidden:
    :maxdepth: 2

    basic-tasks/index.rst
    intermediate-tasks/index.rst
    advanced-tasks/index.rst
      

编译结果：

见 :doc:`../index`

该指令支持以下选项：

- ``:maxdepth:``：指定目录的最大深度。
- ``:hidden:``：隐藏 toctree，使其用于构建左侧导航栏，但不显示在主页面中。

更多信息，见 `Sphinx TOC tree <https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html#directive-toctree>`__。
