#   watch 命令

当您希望在每次文件更改时渲染您的书时，`watch` 命令很有用。 每次更改文件时，您都可以重复使用 `mdbook build` 。 但是使用 `mdbook watch` 将监视您的文件，并在您修改文件时自动触发`build`； 这包括重新创建 SUMMARY.md 中仍然提到的已删除文件！

#### 指定特定的文件夹

`watch` 命令可以将目录作为参数用作书的根目录，而不是当前工作目录。

```bash
mdbook watch path/to/book
```

#### --open

当您使用 `--open` (`-o`) 标志时，`mdbook` 将在构建后在您的默认 Web 浏览器中打开渲染的书。

#### --dest-dir

`--dest-dir` (`-d`) 选项允许您更改本书的输出目录。 相对路径是相对于本书的根目录进行解释的。 如果未指定，它将默认为 book.toml 中 build.build-dir 的值，或 ./book 。


#### 指定排除的文件

`watch` 命令不会自动触发本书根目录中 `.gitignore` 文件中列出的文件的构建。 `.gitignore` 文件可以使用 [gitignore
文档](https://git-scm.com/docs/gitignore) 中描述的模式。 这对于忽略某些编辑器创建的临时文件很有用。

_注意：仅使用书籍根目录中的 `.gitignore`。 不使用父目录中的全局 `$HOME/.gitignore` 或 `.gitignore` 文件。_