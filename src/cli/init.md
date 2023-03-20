# init 命令


每本新的书籍都有一些相同的最小样板。 正是出于这个目的，mdBook 包含了一个 `init` 命令。

`init` 命令的用法如下：

```bash
mdbook init
```

第一次使用 `init` 命令时，会为您设置几个文件：

```bash
book-test/
├── book
└── src
    ├── chapter_1.md
    └── SUMMARY.md
```


- `src` 目录是您用 markdown 写书的地方。 它包含所有的源文件、配置文件等。

- `book` 目录是呈现您的书的地方。 所有输出都已准备好上传到服务器，供您的观众查看。

- `SUMMARY.md` 是您书的骨架，[在另一章](../format/summary.md) 中有更详细的讨论。

#### Tip: 从 SUMMARY.md 生成章节

当 `SUMMARY.md` 文件已经存在时，`init` 命令会先解析它，并根据 `SUMMARY.md` 中使用的路径生成缺失的文件。 这使您可以思考和创建书籍的整个结构，然后让 mdBook 为您生成它。

#### 指定目录

`init` 命令可以将目录作为参数用作书的根目录，而不是当前工作目录。

```bash
mdbook init path/to/book
```

#### --theme


当您使用 `--theme` 标志时，默认主题将被复制到源目录中名为 `theme` 的目录中，以便您可以修改它。

主题是选择性覆盖的，这意味着如果您不想覆盖特定文件，只需将其删除即可，将使用默认文件。

#### --title

指定书籍的标题。 如果未提供，交互式命令行将会询问您标题。

```bash
mdbook init --title="my amazing book"
```

#### --ignore

创建一个 `.gitignore` 文件，默认为忽略 [构建][building] 一本书时创建的 `book` 目录。
如果未提供，交互式提示将询问是否应创建它。

[building]: build.md
