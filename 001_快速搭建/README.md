# 快速搭建

## 1. Sphinx + Read the Docs

### 1.1 **环境搭建**

```bash
 sudo apt install git
 sudo apt install make
 sudo apt install python3
 sudo apt install python3-pip 
```

然后安装最新版本的 Sphinx 及依赖：

```bash
pip3 install -U Sphinx
```

为了完成本示例，还需要安装以下软件包:

```bash
 pip3 install sphinx-autobuild
 pip3 install sphinx_rtd_theme
 pip3 install recommonmark
 pip3 install sphinx_markdown_tables
```

### 1.2 **快速开始**

### **1.2.1 创建项目**

我们先创建并进入项目文件夹（后续所有操作都在该文件夹内）。执行 `sphinx-quickstart` 构建项目框架，将会出现如下对话窗口。

首先，询问你是否要创建独立的源文件和构建目录。实际上对应两种目录结构，一种是在根路径下创建“_build”目录，另一种是在根路径下创建“source”和“build”两个独立的目录，前者用于存放文档资源，后者用于保存构建生成的各种文件。根据个人喜好选择即可，比如我更倾向于独立目录，因此输入 `y`。

接着，需要输入项目名称、作者、项目语言等信息。

此时我们在项目录中执行 `make html`，就会在 build/html 目录生成 html 相关文件。这样就可以直接在浏览器中打开 index.html。

当然，直接访问 html 文件不是很方便，所以我们借助 `sphinx-autobuild` 工具启动 HTTP 服务。

```bash
sphinx-autobuild source build/html
```

默认启动 8000 端口，在浏览器输入 [http://127.0.0.1:8000](https://link.zhihu.com/?target=http%3A//127.0.0.1%3A8000/) 可以直接访问页面。

### 1.2.2 修改主题

打开 conf.py 文件，找到 html_theme 字段，修改为你想要的主题。Sphinx 为我们提供了好多可选的主题，在 [Sphinx Themes](https://link.zhihu.com/?target=https%3A//sphinx-themes.org/) 都可以找到。大家最熟悉的应该是 sphinx_rtd_theme 主题，其实我们前面已经安装好了。

```python
 #html_theme = 'alabaster'
 #html_theme = 'classic'
 html_theme = 'sphinx_rtd_theme'
```

### 1.2.3 **支持 Markdown**

前面我们都是用 reST 语法来操作，但如果我们想用 Markdown 写，或者有大量 Markdown 文档需要迁移怎么办呢？

虽然 Sphinx 默认不支持 Markdown 语法，但可以通过 recommonmark 插件来支持。另外，如果需要支持 markdown 的表格语法，还需要安装 sphinx-markdown-tables 插件。这两个插件其实我们前面已经安装好了，现在只需要在 conf.py 配置文件中添加扩展支持即可。

```python
extensions = [
     'recommonmark',
     'sphinx_markdown_tables'
 ]
```

### 1.2.4 修改内容区域的宽度

在conf.py中加入内容:

```
html_static_path = ['_static']
html_css_files = [
    'custom.css',
]
```

在_static/custom.css文件中加入如下样式：

```css
/*修改内容区域的宽度*/
.wy-nav-content {
   max-width: 1200px; /*设置你想要的宽度, 例如 1200px */
}
```

## 1.3 **文档托管**

在 Read the Docs 网站 [https://readthedocs.org/](https://link.zhihu.com/?target=https%3A//readthedocs.org/) 注册，并绑定 GitHub 账户。点击“Import a Project”导入项目，输入项目名称和仓库地址即可。



**参考**

- [ReadTheDocs搭建第一本电子书 - 知乎](https://zhuanlan.zhihu.com/p/388640347)

