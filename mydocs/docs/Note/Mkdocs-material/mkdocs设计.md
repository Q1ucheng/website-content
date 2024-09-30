# Customize your mkdocs
> Here are some custom configurations about mkdocs.

[Access to official documentation](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/){ .md-button .md-button--primary }

------

今天（2024年3月3日）突然心血来潮，准备把整个博客重新整理一遍（刚开始接触`MkDocs-material`时对一些文件的编写不太熟悉，所以初始的博客配置显得混乱，没有条理）

## 设置Navigation tabs

在阅读官方文档时我发现在页面顶部有一些小标签，作者将不同类型的文件分别存储在其中，感觉不错：

```yaml
theme:
  features:
    - navigation.tabs
```

成功，但它是以我`./docs`中每个文件夹为类别生成的标题，但我想要能自定义标签名称，所以尝试在`yaml`文件中手动设置目录：

**注意：**需要加入相对路径

```yaml
nav:
  - Home: index.md
  - Note: 
    - CS61A Fall20:
      - introduction: Note/CS61A/1. CS61A Structure and Interpretation of Computer Programs.md
      - Functions: Note/CS61A/2. Functions.md
      - Control: Note/CS61A/3. Control.md
      - Higher-Order Function: Note/CS61A/4. Higher-Order Function.md
      - Environments: Note/CS61A/5. Environments.md
    - LaTeX related:
      - 数学建模中的LaTeX代码: Note/LaTeX related/数学建模中的LaTeX代码.md
    - Markdown related:
      - practice: Note/Markdown related/practice.md
    - MkDocs-material:
      - MkDocs部署配置中error的解决: Note/Mkdocs-material/mkdocs部署配置中error的解决.md
      - 设计MkDocs: Note/Mkdocs-material/mkdocs设计.md
  - Blog: Blog/Blog.md
```



