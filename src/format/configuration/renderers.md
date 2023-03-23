# 配置渲染器

渲染器（也称为`后端`）负责创建本书的输出。

以下后端是内置的：

* [`html`](#html-renderer-options) — 将书呈现为 HTML。 如果在 book.toml 中没有定义其他 [output] 表，则默认情况下启用此功能。
* [`markdown`](#markdown-renderer) — 在运行预处理器后将书输出为 markdown。 这对于调试预处理器很有用。

社区已经开发了几个后端。
请参阅 [第三方插件][Third Party Plugins] wiki 页面以获取可用后端列表。

有关如何创建新后端的信息，请参阅 [面向开发者的后端][Backends for Developers] 一章。

[Third Party Plugins]: https://github.com/rust-lang/mdBook/wiki/Third-party-plugins
[Backends for Developers]: ../../for_developers/backends.md

## Output tables

可以通过在 `book.toml` 中包含一个带有后端名称的 `output` 表来添加后端。
例如，如果您有一个名为 `mdbook-wordcount` 的后端，那么您可以将其包含在：

```toml
[output.wordcount]
```

使用此表，mdBook 将执行 `mdbook-wordcount` 后端。

此表可以包含特定于后端的其他键值对。
例如，如果我们的示例后端需要一些额外的配置选项：

```toml
[output.wordcount]
ignores = ["Example Chapter"]
```

如果您定义任何 `[output]` 表，则默认情况下不会启用 `html` 后端。
如果你想保持 `html` 后端运行，那么只需将它包含在 `book.toml` 文件中。
例如：

```toml
[book]
title = "My Awesome Book"

[output.wordcount]

[output.html]
```

如果包含多个 `output` 表，这会更改输出目录布局的行为。
如果只有一个后端，那么它会将其输出直接放在 `book` 目录中（请参阅 [`build.build-dir`] 以覆盖此位置）。
如果有多个后端，则每个后端都放在 `book` 下的一个单独目录中。
例如，上面的目录有 `book/html` 和 `book/wordcount`。

[`build.build-dir`]: general.md#build-options

### 自定义后端命令

默认情况下，当您将 `[output.foo]` 表添加到 `book.toml` 文件时，`mdbook` 将尝试调用 `mdbook-foo` 可执行文件。
如果您想使用不同的程序名称或传递命令行参数，可以通过添加`command`字段来覆盖此行为。

```toml
[output.random]
command = "python random.py"
```

### 可选后端

如果启用未安装的后端，默认行为是抛出错误。
可以通过将后端标记为可选来更改此行为：

```toml
[output.wordcount]
optional = true
```

这会将错误降级为警告。


## HTML 渲染器选项

HTML 渲染器有多种选项，详述如下。
它们应该在 book.toml 文件的 [output.html] 表中指定。

```toml
# 包含所有 output 选项的示例 book.toml 文件。
[book]
title = "Example book"
authors = ["John Doe", "Jane Doe"]
description = "The example book covers examples."

[output.html]
theme = "my-theme"
default-theme = "light"
preferred-dark-theme = "navy"
curly-quotes = true
mathjax-support = false
copy-fonts = true
additional-css = ["custom.css", "custom2.css"]
additional-js = ["custom.js"]
no-section-label = false
git-repository-url = "https://github.com/rust-lang/mdBook"
git-repository-icon = "fa-github"
edit-url-template = "https://github.com/rust-lang/mdBook/edit/master/guide/{path}"
site-url = "/example-book/"
cname = "myproject.rs"
input-404 = "not-found.md"
```

以下配置选项可用：

 

- **theme:** mdBook 带有一个默认主题和它需要的所有资源文件。但如果设置了这个选项，mdBook 将有选择本地指定文件夹中的主题文件封面主题。
- **default-theme：** 在`更改主题`下拉列表中默认选择的主题配色方案。 默认为`light`。
- **preferred-dark-theme：** 默认的深色主题。 如果浏览器通过 ['prefers-color-scheme'](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme) CSS 媒体查询。 默认为`navy`。
- **curly-quotes：** 将直引号转换为弯引号，代码块和代码跨度中出现的引号除外。 默认为`false`。
- **mathjax-support：** 添加对 [MathJax](../mathjax.md) 的支持。 默认为`false`。
- **copy-fonts:**（**已弃用**）如果为`true`（默认值），mdBook 使用其内置字体，这些字体被复制到输出目录。 如果为 `false`，则不会使用内置字体。 此选项已弃用。 如果您想定义自己的自定义字体，请创建一个`theme/fonts/fonts.css`文件并将字体存储在`theme/fonts/`目录中。
- **google-analytics：**（**已弃用**）并将在未来的版本中删除。 使用 `theme/head.hbs` 文件来添加适当的 Google Analytics 代码。
- **additional-css:** 如果您需要在不覆盖整个样式的情况下稍微更改书籍的外观，您可以指定一组样式表，这些样式表将在默认样式表之后加载，您可以在其中更改样式。
- **additional-js：** 如果您需要在不删除当前行为的情况下向书中添加一些行为，您可以指定一组将与默认文件一起加载的 JavaScript 文件。
- **no-section-label:** 默认情况下，mdBook 在目录列中添加数字部分标签。 例如，`1.`、`2.1`。 将此选项设置为 `true` 以禁用这些标签。 默认为`false`。
- **git-repository-url：** 本书的 git 存储库的 url。 如果提供了一个图标链接，将在本书的菜单栏中输出。
- **git-repository-icon：** 用于 git 存储库链接的 FontAwesome 图标类。 默认为 `fa-github`，看起来像 <i class="fa fa-github"></i>。 如果您不使用 GitHub，另一个要考虑的选项是 `fa-code-fork`，它看起来像 <i class="fa fa-code-fork"></i>。
- **edit-url-template：** 编辑 url 模板，当提供时显示一个`建议编辑`按钮（看起来像 <i class="fa fa-edit"></i>）用于直接跳转到编辑 当前查看的页面。 例如 GitHub 项目将其设置为 `https://github.com/<owner>/<repo>/edit/master/{path}` 或对于 Bitbucket 项目将其设置为 `https://bitbucket.org/<owner>/ <repo>/src/master/{path}?mode=edit` 其中 {path} 将替换为存储库中文件的完整路径。
- **input-404:** 用于未找到的文件。默认为`404.md`。
- **site-url：** 指明书籍将托管在哪里的。 这是确保 404 文件中的导航链接和 script/css 导入正常所必需的，即使在访问子目录中的 url 时也是如此。 默认为`/`。 如果设置了 `site-url`，请确保为您的资源使用文档相对路径链接，这意味着它们不应以 `/` 开头。
- **cname：** 将托管您的图书的 DNS 子域或顶级域。 根据 GitHub Pages 的要求，此字符串将写入站点根目录中名为 CNAME 的文件（请参阅[*管理 GitHub Pages 站点的自定义域*][custom domain]）。

[custom domain]: https://docs.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site

### `[output.html.print]`

`[output.html.print]` 表提供了用于控制可打印输出的选项。
默认情况下，mdBook 将在书的右上角包含一个图标（看起来像 <i class="fa fa-print"></i>），它将书打印为单页。

```toml
[output.html.print]
enable = true    # 包括对可打印输出的支持
page-break = true # 在每章后插入分页符
```

- **enable:** 启用打印支持。 当为 `false` 时，将不会呈现打印支持。 默认为`true`。
- **page-break** 在章节之间插入分页符。 默认为`true`。

### `[output.html.fold]`

`[output.html.fold]` 表提供了用于控制导航侧边栏中章节列表折叠的选项。

```toml
[output.html.fold]
enable = false    # 是否启用折叠
level = 0         # 开始折叠的深度
```

- **enable:** 启用折叠。 关闭时，所有折叠都打开。默认为 `false`。
- **level:** 开始折叠的深度。 当 level 为 0 时，所有折叠都关闭。 默认为 `0`。

### `[output.html.playground]`

`[output.html.playground]` 表提供了用于控制 Rust 示例代码块的选项，以及它们与 [Rust 演练场][Rust Playground] 的集成。

[Rust Playground]: https://play.rust-lang.org/

```toml
[output.html.playground]
editable = false         # 允许编辑源代码
copyable = true          # 用于复制代码的复制按钮
copy-js = true           # 用于代码编辑器的 JavaScript
line-numbers = false     # 显示可编辑代码的行号
runnable = true          # 显示 rust 代码的运行按钮
```

- **editable:** 允许编辑源代码。 默认为 `false`。
- **copyable:** 在代码片段上显示复制按钮。 默认为 `true` 。
- **copy-js:** 将编辑器的 JavaScript 文件复制到输出目录。
   默认为 `true` 。
- **line-numbers** 在代码的可编辑部分显示行号。 要求 `editable` 和 `copy-js` 都为 `true`。 默认为 `false`。
- **runnable** 显示 Rust 代码片段的运行按钮。 将其更改为 `false` 将全局禁用演练场功能。 默认为 `true` 。

[Ace]: https://ace.c9.io/

### `[output.html.search]`

`[output.html.search]` 表提供了用于控制内置文本 [搜索][search] 的选项。
mdBook 必须在启用`search`功能（默认情况下启用）的情况下进行编译。

[search]: ../../guide/reading.md#search

```toml
[output.html.search]
enable = true            # 启用搜索功能
limit-results = 30       # 最大搜索结果数
teaser-word-count = 30   # 用于搜索结果预告的单词数
use-boolean-and = true   # 多个搜索词必须全部匹配
boost-title = 2          # 标题中匹配项的排名提升因子
boost-hierarchy = 1      # 页面名称匹配的排名提升因子
boost-paragraph = 1      # 文本匹配的排名提升因子
expand = true            # 部分单词将匹配较长的术语
heading-split-level = 3  # 将结果链接到标题级别
copy-js = true           # 包含用于搜索的 Javascript 代码
```
<!-- 
- **enable:** Enables the search feature. Defaults to `true`.
- **limit-results:** The maximum number of search results. Defaults to `30`.
- **teaser-word-count:** The number of words used for a search result teaser.
  Defaults to `30`.
- **use-boolean-and:** Define the logical link between multiple search words. If
  true, all search words must appear in each result. Defaults to `false`.
- **boost-title:** Boost factor for the search result score if a search word
  appears in the header. Defaults to `2`.
- **boost-hierarchy:** Boost factor for the search result score if a search word
  appears in the hierarchy. The hierarchy contains all titles of the parent
  documents and all parent headings. Defaults to `1`.
- **boost-paragraph:** Boost factor for the search result score if a search word
  appears in the text. Defaults to `1`.
- **expand:** True if search should match longer results e.g. search `micro`
  should match `microwave`. Defaults to `true`.
- **heading-split-level:** Search results will link to a section of the document
  which contains the result. Documents are split into sections by headings this
  level or less. Defaults to `3`. (`### This is a level 3 heading`)
- **copy-js:** Copy JavaScript files for the search implementation to the output
  directory. Defaults to `true`. -->

### `[output.html.redirect]`

`[output.html.redirect]` 表提供了一种添加重定向的方法。
当您移动、重命名或删除页面以确保指向旧 URL 的链接将转到新位置时，这很有用。

```toml
[output.html.redirect]
"/appendices/bibliography.html" = "https://rustc-dev-guide.rust-lang.org/appendix/bibliography.html"
"/other-installation-methods.html" = "../infra/other-installation-methods.html"
```
该表包含键值对，其中键是需要创建重定向文件的位置，作为构建目录的绝对路径（例如 `/appendices/bibliography.html`）。
该值可以是浏览器应导航到的任何有效 URI（例如 `https://rust-lang.org/`、`/overview.html` 或 `../bibliography.html`）。

这将生成一个 HTML 页面，该页面将自动重定向到给定位置。
请注意，源位置不支持 `#` 锚重定向。

## Markdown 渲染器

Markdown 渲染器将运行预处理器，然后输出生成的 Markdown。 这对于调试预处理器非常有用，尤其是与 `mdbook test` 结合使用以查看 `mdbook` 传递给 `rustdoc` 的 Markdown。

Markdown 渲染器包含在 `mdbook` 中，但默认情况下禁用。
通过向 `book.toml` 添加一个空表来启用它，如下所示：

```toml
[output.markdown]
```

目前没有 Markdown 渲染器的配置选项； 只有它是启用还是禁用。

请参阅 [预处理器文档](preprocessors.md)，了解如何指定哪些预处理器应在 Markdown 渲染器之前运行。
