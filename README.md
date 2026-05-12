# Yida Handbook

## 📖 项目简介

本项目是一个基于 **Sphinx + uv** 构建的现代化文档站点，支持使用 Markdown 语法编写内容，并提供了自动构建与实时预览功能。它适用于技术文档、开发手册、知识库等多种场景。

## ✨ 功能特性

- 基于 Sphinx 的现代文档构建体系
- 支持 Markdown（MyST 解析器）编写
- 自动构建与浏览器实时热重载功能
- 内置国内 PyPI 镜像加速
- 可扩展的插件生态，支持 Mermaid 图表、复制按钮、评论系统等

## 🚀 快速开始

### 环境依赖

- Python 3.13+
- [uv](https://github.com/astral-sh/uv)（推荐的 Python 包管理器）

### 安装步骤

**1. 初始化项目**

```bash
uv init
```

**2. 创建虚拟环境**（以 Python 3.14 为例）

```bash
uv venv --python 3.14
```

**3. 配置国内镜像源（可选，用于加速）**

在 `pyproject.toml` 文件中添加阿里云 PyPI 镜像配置：

```toml
[[tool.uv.index]]
url = "https://mirrors.aliyun.com/pypi/simple"
default = true
```

**4. 安装项目依赖**

```bash
uv sync
```

> 项目依赖已通过 `pyproject.toml` 统一管理，无需手动逐个安装。

**5. 初始化 Sphinx 项目**

```bash
sphinx-quickstart
```

## 💡 使用示例

### 手动构建文档

执行以下命令生成静态 HTML 文档：

```bash
make html
```

生成的文档默认位于 `build` 目录下。

### 自动构建与实时预览（推荐）

安装 `sphinx-autobuild` 工具：

```bash
pip install sphinx-autobuild
```

启动自动构建服务：

```bash
sphinx-autobuild source build
```

服务启动后，访问 `http://127.0.0.1:8000` 即可预览。

**特性**：
- 监听源文件变化，自动触发构建
- 浏览器页面将自动刷新

**常用进阶参数**：

| 参数 | 作用 |
|------|------|
| `--open-browser` | 启动时自动打开浏览器 |
| `--port=0` | 自动选择空闲端口 |
| `--watch <dir>` | 额外监听指定的静态资源目录 |

**示例**：

```bash
sphinx-autobuild source build --open-browser
```

### 集成到 Makefile（可选）

在 `Makefile` 文件末尾添加以下内容：

```makefile
livehtml:
    sphinx-autobuild "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
```

之后即可通过以下命令启动实时预览：

```bash
make livehtml
```

### 新手推荐流程

对于初次使用的用户，可以按照以下命令顺序快速上手：

```bash
uv init
uv venv --python 3.14
uv sync
sphinx-autobuild source build --open-browser
```

## 🤝 贡献指南

[待补充]

## 📜 开源协议

[待补充]

## 📄 附录：Read the Docs 配置

为了使项目能够被 [Read the Docs](https://readthedocs.org/) 服务自动构建，需要在项目根目录添加 `.readthedocs.yaml` 配置文件。

**文件路径**：`.readthedocs.yaml`

**文件内容**：

```yaml
# Read the Docs configuration file
# See https://docs.readthedocs.io/en/stable/config-file/v2.html for details

# Required
version: 2

# Set the OS, Python version, and other tools you might need
build:
  os: ubuntu-24.04
  tools:
    python: "3.14"

# Build documentation in the "docs/" directory with Sphinx
sphinx:
  configuration: source/conf.py

# Optionally, but recommended,
# declare the Python requirements required to build your documentation
# See https://docs.readthedocs.io/en/stable/guides/reproducible-builds.html
python:
  install:
    - requirements: requirements.txt
```
