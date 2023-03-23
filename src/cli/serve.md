#   serve 命令

默认情况下，serve 命令用于通过 `localhost:3000` 上的 HTTP 服务来预览一本书：

```bash
mdbook serve
```

`serve` 命令监视图书的 `src` 目录的变化，重建图书并为每次变化刷新客户端； 这包括重新创建 `SUMMARY.md` 中提到的，但已删除文件！ Websocket 连接用于触发客户端刷新。

***注意：*** *`serve` 命令用于测试书籍的 HTML 输出，并不打算成为网站的完整 HTTP 服务器。*

#### 指定特定的文件夹

`serve` 命令可以将目录作为参数用作书的根目录，而不是当前工作目录。

```bash
mdbook serve path/to/book
```

### 服务器选项

`serve` 主机名默认为 `localhost`，端口默认为 `3000`。 可以在命令行上指定任一选项：

```bash
mdbook serve path/to/book -p 8000 -n 127.0.0.1 
```

#### --open

当您使用 `--open` (`-o`) 标志时，`mdbook` 将在构建后在您的默认 Web 浏览器中打开渲染的书。


#### --dest-dir

`--dest-dir` (`-d`) 选项允许您更改本书的输出目录。 相对路径是相对于本书的根目录进行解释的。 如果未指定，它将默认为 book.toml 中 build.build-dir 的值，或 ./book 。

#### 指定排除的文件

`serve` 命令不会自动触发本书根目录中 `.gitignore` 文件中列出的文件的构建。 `.gitignore` 文件可以使用 [gitignore
文档](https://git-scm.com/docs/gitignore) 中描述的模式。 这对于忽略某些编辑器创建的临时文件很有用。

_注意：仅使用书籍根目录中的 `.gitignore`。 不使用父目录中的全局 `$HOME/.gitignore` 或 `.gitignore` 文件。_
