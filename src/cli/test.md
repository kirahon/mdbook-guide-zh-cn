#   test 命令

写书时，有时需要自动化一些测试。 例如，[The Rust Programming Book](https://doc.rust-lang.org/stable/book/) 中使用了大量可能过时的代码示例。 因此，能够自动测试这些代码示例对他们来说非常重要。

mdBook 支持 `test` 命令，该命令将运行书中所有可用的测试。 目前，仅支持 rustdoc 测试，但将来可能会扩展。

#### 取消某个代码块的测试

rustdoc 不测试包含 `ignore` 属性的代码块：

    ```rust,ignore
    fn main() {}
    ```

rustdoc 也不测试指定除 Rust 以外的语言的代码块：

    ```markdown
    **Foo**: _bar_
    ```

rustdoc *确实*测试未指定语言的代码块：

    ```
    This is going to cause an error!
    ```

#### 指定特定的文件夹

`test` 命令可以将目录作为参数用作书的根目录，而不是当前工作目录。

```bash
mdbook test path/to/book
```

#### --library-path

The `--library-path` (`-L`) option allows you to add directories to the library search path used by `rustdoc` when it builds and tests the examples. Multiple directories can be specified with multiple options (`-L foo -L bar`) or with a comma-delimited list (`-L foo,bar`). The path should point to the Cargo [build cache](https://doc.rust-lang.org/cargo/guide/build-cache.html) `deps` directory that contains the build output of your project. For example, if your Rust project's book is in a directory named `my-book`, the following command would include the crate's dependencies when running `test`:

`--library-path` (`-L`) 选项允许您将目录添加为 `rustdoc` 在构建和测试示例时使用的库路径。 可以使用多个选项（`-L foo -L bar`）或逗号分隔列表（`-L foo,bar`）指定多个目录。 该路径应指向包含项目构建输出的 Cargo [构建缓存](https://doc.rust-lang.org/cargo/guide/build-cache.html) `deps` 目录。 例如，如果你的 Rust 项目的书在一个名为 my-book 的目录中，下面的命令将在运行 test 时包含 crate 的依赖项：

```shell
mdbook test my-book -L target/debug/deps/
```

请参阅 `rustdoc` 命令行 [文档](https://doc.rust-lang.org/rustdoc/command-line-arguments.html#-l--library-path-where-to-look-for-dependencies) 了解更多信息。


#### --dest-dir

`--dest-dir` (`-d`) 选项允许您更改本书的输出目录。 相对路径是相对于本书的根目录进行解释的。 如果未指定，它将默认为 book.toml 中 build.build-dir 的值，或 ./book 。


#### --chapter

`--chapter` (`-c`) 选项允许您使用章节名称或章节的相对路径来测试书中的特定章节。