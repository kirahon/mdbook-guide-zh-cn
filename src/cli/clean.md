#   clean 命令

clean 命令用于删除生成的书籍和任何其他构建工件。

```bash
mdbook clean
```

#### 指定特定的文件夹

`clean` 命令可以将目录作为参数用作书的根目录，而不是当前工作目录。

```bash
mdbook clean path/to/book
```
 

#### --dest-dir

`--dest-dir` (`-d`) 选项允许您更改本书的输出目录。 相对路径是相对于本书的根目录进行解释的。 如果未指定，它将默认为 book.toml 中 build.build-dir 的值，或 ./book 。

```bash
mdbook clean --dest-dir=path/to/book
```

`path/to/book` 可以是相对路径和绝对路径.