# 配置预处理器

预处理器是可以在将原始 Markdown 源发送到渲染器之前对其进行修改的扩展。

以下预处理器是内置且默认包含的：

- `links`：扩展章节中的 `{{ #playground }}`、`{{ #include }}` 和 `{{ #rustdoc_include }}` handlebars 助手以包含文件的内容。 有关更多信息，请参见 [包含文件][Including files]。
- `index`：将所有名为 `README.md` 的章节文件转换为 `index.md`。 也就是说，所有的 `README.md` 都会被渲染到书中的一个索引文件 `index.html` 中。

可以使用 [`build.use-default-preprocessors`] 配置选项禁用内置预处理器。

社区已经开发了几个预处理器。 有关可用预处理器列表，请参阅 [第三方插件][Third Party Plugins] wiki 页面。

有关如何创建新预处理器的信息，请参阅 [面向开发人员的预处理器][Preprocessors for Developers] 一章。

[Including files]: ../mdbook.md#including-files
[`build.use-default-preprocessors`]: general.md#build-options
[Third Party Plugins]: https://github.com/rust-lang/mdBook/wiki/Third-party-plugins
[Preprocessors for Developers]: ../../for_developers/preprocessors.md

## 自定义预处理器配置

预处理器可以通过在 `book.toml` 中包含一个带有预处理器名称的 preprocessor 表来添加。 

例如，如果你有一个名为 `mdbook-example` 的预处理器，那么你可以将它包含在：

```toml
[preprocessor.example]
```

使用此表，mdBook 将执行“mdbook-example”预处理器。

该表可以包含特定于预处理器的其他键值对。
例如，如果我们的示例预处理器需要一些额外的配置选项：

```toml
[preprocessor.example]
some-extra-feature = true
```

## 将预处理器依赖项锁定到渲染器

您可以通过将两者绑定在一起来明确指定预处理器应该为哪个渲染器运行。

```toml
[preprocessor.example]
renderers = ["html"]  # example 预处理器仅与 HTML 渲染器一起运行
```

## 提供你自己的命令

默认情况下，当您将 `[preprocessor.foo]` 表添加到 `book.toml` 文件时，`mdbook` 将尝试调用 `mdbook-foo` 可执行文件。 如果您想使用不同的程序名称或传递命令行参数，可以通过添加`command`字段来覆盖此行为。

```toml
[preprocessor.random]
command = "python random.py"
```

## 需要一定的顺序

预处理器的运行顺序可以通过“before”和“after”字段来控制。
例如，假设您希望 `linenos` 预处理器处理可能已被 `{{#include}}`d 的行； 且希望它在内置的 `links` 预处理器之后运行，您可以使用 `before` 或 `after` 字段来要求它：

```toml
[preprocessor.linenos]
after = [ "links" ]
```

或者

```toml
[preprocessor.links]
before = [ "linenos" ]
```

也可以在同一个配置文件中同时指定以上两项，尽管这有些多余。

通过 `before` 和 `after` 指定的具有相同优先级的预处理器按名称排序。 且检测到死循环时，会产生错误。
