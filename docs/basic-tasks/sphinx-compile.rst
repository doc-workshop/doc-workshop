使用 Sphinx 把文档编译成 HTML
===============================

Sphinx 是 Python 官方推荐的文档生成工具，基于 RST 格式，将文档转化成多种格式（HTML、PDF、EPUB 等）。

本指南将详细介绍使用 Sphinx 把 RST 文档编译为 HTML 的完整流程。

1. 下载项目
-----------

**情况 1：如果你之前用过 git，则可以通过 git clone 下载本项目。**

具体操作为：

- 登录自己的 GitHub 账户，找到 https://github.com/doc-workshop/doc-workshop。
- 点击右侧的 fork 按钮，这个操作会帮你在自己 GitHub 中创建一个副本。

.. figure:: ../_static/fork.png
    :align: center
    :scale: 35%
    :alt: 使用 fork 复制副本到自己的 GitHub

    使用 fork 复制副本到自己的 GitHub

- 最后，打开终端，运行下面的命令，把你自己的 GitHub 项目克隆到本地。注意，请把下面的链接替换成你自己项目的链接。

.. code-block:: bash

   git clone https://github.com/username/your-docs-project.git

**情况 2：如果你之前没有接触过 git，则可以使用下面的方法下载本项目。**

- 打开链接：https://github.com/doc-workshop/doc-workshop
- 点击右侧的 code -> Download ZIP

.. figure:: ../_static/download.png
    :align: center
    :scale: 35%
    :alt: 使用 download 下载副本到自己的电脑

    使用 download 下载副本到自己的电脑

- 在本地把下载的压缩包解压，在编辑器（例如 VS Code）中打开编辑即可。


2. 配置 conf.py
---------------

``conf.py`` 是 Sphinx 的核心配置文件，位于 ``docs`` 目录下。以下是一些关键配置项：

项目基本信息
~~~~~~~~~~~~

.. code-block:: python

   # 项目基本信息。在本次任务中，你需要替换成自己的信息
    project = "技术文档实战"
    copyright = "2025, 文档小栈"
    author = "文档小栈"

    # HTML 主题配置。该项目使用 sphinx_rtd_theme，在本次任务中，你需要替换成 alabaster

    html_theme = "sphinx_rtd_theme"

扩展配置
~~~~~~~~

如果项目需要使用一些特殊功能，例如加 todo 笔记或者想在代码块处加一个复制的按钮，则需要使用 sphinx.ext.todo 和 sphinx_copybutton 扩展功能。

.. code-block:: python

   # 扩展列表
   extensions = [
       "sphinx.ext.autodoc",
       "sphinx.ext.viewcode",
       "sphinx.ext.todo",
       "sphinx.ext.napoleon",
       "sphinx_copybutton",
   ]

   # Todo 配置
   todo_include_todos = True

3. 安装依赖包
----------------

编译所使用的工具包已全部在 ``docs/requirements.txt`` 中列出。运行编译命令之前，需要先安装这些依赖包。以 macOS 系统为例，具体步骤为：

1. 在编辑器中打开项目
2. 新开一个 New Terminal，如下图：

.. figure:: ../_static/install-requirements.png
    :align: center
    :scale: 25%
    :alt: 安装依赖包

    安装依赖包

3. 进入到 docs 目录，运行安装命令：

.. code-block:: bash

    # cd 的意思就是进入某个目录
    cd docs
    pip install -r requirements.txt


4. 编译生成 HTML
----------------

在 docs 目录下，使用以下命令编译文档：

.. code-block:: bash

   # 本项目已配置好 make 编译系统，可直接使用 make
   make html

生成的 HTML 文件位于 ``docs/_build/html`` 目录中。

.. figure:: ../_static/html-output.png
    :align: center
    :scale: 25%
    :alt: 检查生成的 HTML

    检查生成的 HTML

5. 本地预览与调试
-----------------

在浏览器中打开生成的 HTML 文件：

.. code-block:: bash

   # 在 macOS 上使用 open 命令，后面加 html 文档的路径。把文档拖到命令行光标处，会自动生成路径，如上图所示。
   open _build/html/index.html

调试常见问题：

- 检查 RST 语法错误
- 确认所有引用文件存在
- 验证内部链接是否正确

更多资源
--------

- `Sphinx 官方文档 <https://www.sphinx-doc.org/>`_
- `reStructuredText 入门 <https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html>`_
