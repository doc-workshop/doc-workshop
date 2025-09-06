技术文档 Workshop
===================

欢迎来到技术文档 Workshop！

在本次 Workshop 中我们将一起走一下从技术文档编写到在线文档部署的完整流程。通过实战操作，我们将共同学习如何使用 RST (reStructuredText) 编写技术文档，并通过 Sphinx 工具将文档编译为 HTML，最终部署至 Read the Docs (RTD) 平台或 GitHub Pages，形成专业的在线文档系统。

准备工作
--------

在开始之前，我们需要做一些准备工作：

- GitHub 账号
- Read the Docs 账号，选择免费版，可使用 GitHub 账号登录
- VPN（国内访问 GitHub 不稳定，建议使用）
- 文本编辑器（如 Cursor、VSCode 等，建议选择支持 AI 辅助编写的编辑器）

Workshop 内容
-------------

在本次 Workshop 中，我们将一起完成以下任务。任务由易到难，逐步带你掌握技术文档编写和部署的完整流程。

.. note::

  每个行业基本上都会涉及到技术文档，因此技术文档的具体内容因行业不同而不同。在本 Workshop 中，我们着重于技术文档涉及的通用技术，而非行业具体内容，以便掌握技术文档编写和部署的完整流程。

初级任务及成果交付
~~~~~~~~~~~~~~~~~~~~

**任务：**

- 使用 RST 编写技术文档
- 在本地使用 Sphinx 将文档编译为 HTML，并查看效果

**交付：**

- 本阶段完成后，应自主编写一份 RST 文档，需要用到文档 :doc:`basic-tasks/rst-syntax` 中介绍的多数功能。编写完成后，在 :doc:`basic-tasks/check-rst-syntax` 页面提交。
- 本阶段结束后，应在本地编译一份 HTML 文档，其中 author 为自己小红书账号名称，主题为：alabaster。完成后，在 :doc:`basic-tasks/check-html-output` 页面提交生成的 ``_build/html/index.html`` 文档。


中阶任务及成果交付
~~~~~~~~~~~~~~~~~~~~

**任务：**

- 使用 GitHub 账号创建自己的 GitHub 仓库，或 fork 本项目仓库
- 使用 git 工具将初级任务中完成的 RST 文档推送到自己的 GitHub 仓库
- 配置 GitHub 仓库，将文档导入 Read the Docs (RTD) 平台
- 在 Read the Docs (RTD) 平台查看文档效果

**交付：**

.. todo::

   待定


高阶任务（文档自动化）
~~~~~~~~~~~~~~~~~~~~~~~~~~

**任务：**

- 自动编译 API 文档
- 使用 Google Analytics 自动追踪用户数据
- 支持多版本和多语言文档管理
- 配置 GitHub Actions 实现自动检查、自动编译、自动部署至 GitHub Pages
- 使用 Docker 保证环境统一

**交付：**

.. todo::

   待定

.. toctree::
   :hidden:
   :maxdepth: 2

   basic-tasks/index.rst
   intermediate-tasks/index.rst
   advanced-tasks/index.rst