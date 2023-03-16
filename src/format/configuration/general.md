# 常用配置

您可以在 ***book.toml*** 文件中为您的图书配置参数。

这是一个 ***book.toml*** 文件的示例：

```toml
[book]
title = "Example book"
authors = ["John Doe"]
description = "The example book covers examples."

[rust]
edition = "2018"

[build]
build-dir = "my-example-book"
create-missing = false

[preprocessor.index]

[preprocessor.links]

[output.html]
additional-css = ["custom.css"]

[output.html.search]
limit-results = 15
```

## 支持的配置选项

注意，配置中指定的**任何**相对路径将始终相对于配置文件所在的书的根目录。

### 元数据

这是关于您的图书的一般信息。

- **title:** 书名
- **authors:** 本书的作者
- **description:** 书籍的描述，作为元信息添加到每个页面的 html `<head>` 中
- **src:** 默认情况下，源目录位于根文件夹下名为 src 的目录中。 但这可以通过配置文件中的 `src` 进行配置
- **language:** 本书的主要语言，例如用作语言属性`<html lang="en">`

**book.toml**
```toml
[book]
title = "Example book"
authors = ["John Doe", "Jane Doe"]
description = "The example book covers examples."
src = "my-src"  # the source files will be found in `root/my-src` instead of `root/src`
language = "en"
```

### Rust 配置

Rust 语言的选项，与运行测试和演练场集成相关。

```toml
[rust]
edition = "2015"   # the default edition for code blocks
```

- **edition**: 默认情况下用于代码片段的 Rust 版本，默认值为“2015”。 也可以使用 `edition2015`、`edition2018` 或`edition2021` 注释控制单个代码块，例如：

  ~~~text
  ```rust,edition2015
  // This only works in 2015.
  let try = true;
  ```
  ~~~

### Build 配置

控制着书籍的构建过程。

```toml
[build]
build-dir = "book"                # 放置构建输出的文件的文件夹
create-missing = true             # 是否自动创建目录中缺失的页面
use-default-preprocessors = true  # 使用默认预处理器
extra-watch-dirs = []             # 监视额外的可以触发构建的文件夹
```


- **build-dir:** 放置渲染书籍的目录。默认情况下，这是书籍根目录中的 `book/` 。 这可以用 `--dest-dir` CLI 选项覆盖。
- **create-missing:** 默认情况下，任何在 `SUMMARY.md` 中指定的缺失文件都将在本书构建时创建（即 `create-missing = true`）, 如果是 `false`，那么如果文件不存在，构建过程将退出并报错。
- **use-default-preprocessors:** 通过将此选项设置为“false”来禁用（`links` &  `index`）的默认预处理器。

   如果您有相同预处理器, 或其他通过配置表声明的预处理器，它们将替代默认预处理器运行。

   - 为清楚起见，在没有预处理器配置的情况下，将运行默认的`links` &  `index`。
   - 设置 `use-default-preprocessors = false` 将禁止默认预处理器运行。
   - 添加 `[preprocessor.links]` 将确保，无论 `use-default-preprocessors` 怎样 `links` 它将运行。
- **extra-watch-dirs**：在 `watch` 和 `serve` 命令中监视的目录路径列表。 更改这些目录下的文件将触发重建。 如果您的书依赖于其 `src` 目录之外的文件，则很有用。