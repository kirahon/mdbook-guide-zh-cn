# 创作

当你安装了 `mdbook` CLI 工具，您就可以使用它来创建和渲染一本书。

## 初始化书籍

`mdbook init` 命令将创建一个包含一本空书的新文件夹，供您开始使用。

并且您需要为它指定要创建的文件夹的名称：

```sh
mdbook init my-first-book
```

在生成书时，它会问几个问题。
回答完问题后，就可以进入生成新书的文件夹了：

```sh
cd my-first-book
```

渲染书籍的方法有多种，但最简单的方法之一是使用 `serve` 命令，它将构建您的书籍并启动本地网络服务器：

```sh
mdbook serve --open
```

`--open` 选项将打开您的默认网络浏览器以查看您的新书。
即使在编辑本书内容时，您也可以让服务器保持运行状态，`mdbook` 将自动重建输出**并且**自动刷新您的网络浏览器。

查看 [CLI 指南](../cli/index.html) 以获取有关其他 `mdbook` 命令和 CLI 选项的更多信息。
 
## 书籍的结构

一本书是由几个文件构建的，这些文件定义了书的设置和布局。

### `book.toml`

 
在你的书的根目录中，有一个 `book.toml` 文件，其中包含有关您所构建的书的设置。
这是用 [TOML 标记语言](https://toml.io/) 编写的。
默认设置通常足以让您入门。
如果您有兴趣探索 mdBook 提供的更多功能和选项，请查看 [配置章节](../format/configuration/index.html) 了解更多详细信息。

一个非常基本的 `book.toml` 可以像这样简单：

```toml
[book]
title = "My First Book"
```

### `SUMMARY.md`

 

本书的下一个主要部分是位于 `src/SUMMARY.md` 的摘要文件。
该文件包含本书所有章节的列表。
要使新章节可以被查看，必须将其添加到此列表中。

这是一个包含着前几章的 Summary 文件示例：

```md
# Summary

[Introduction](README.md)

- [My First Chapter](my-first-chapter.md)
- [Nested example](nested/README.md)
    - [Sub-chapter](nested/sub-chapter.md)
```

尝试在编辑器中打开 `src/SUMMARY.md` 并添加几章。
如果任何章节文件不存在，`mdbook` 会自动为您创建它们。

有关摘要文件的其他格式化选项的更多详细信息，请查看[摘要章节](../format/summary.md)。

### 源文件

你的书的内容都包含在 `src` 目录中。
每一章都是一个单独的 Markdown 文件。
通常，每一章都以带有章节标题的 1 级标题开始。

```md
# My First Chapter

Fill out your content here.
```


文件精确的布局由您决定。
文件的组织将与生成的 HTML 文件相对应，因此请记住，文件布局是每章 URL 的一部分。

当 `mdbook serve` 命令运行时，您可以打开任何章节文件并开始编辑它们。
每次保存文件时，`mdbook` 都会重建这本书并刷新您的网络浏览器。

查看 [Markdown 章节](../format/markdown.md) 以获取有关格式化章节内容的更多信息。

`src` 文件夹中的所有其他文件都将包含在输出中。
因此，如果您有图像或其他静态文件，只需将它们包含在 `src` 文件夹中的某个位置。

## 发布书籍



写完书后，您可能希望将它放在某个地方供其他人查看。
第一步是构建本书的输出。
在 `book.toml` 文件的同一文件夹目录中使用 `mdbook build` 命令来完成：

```sh
mdbook build
```

这将生成一个名为 `book` 的目录，其中包含您的书的 HTML 内容。
然后，您可以将此目录放在任何 Web 服务器上以托管它。

有关发布和部署的更多信息，请查看 [持续集成](../continuous-integration.md) 了解更多。
