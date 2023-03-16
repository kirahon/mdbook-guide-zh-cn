# 安装

有多种方法可以安装 mdBook CLI 工具。
选择以下最适合您需要的任何一种方法。
如果您正在安装 mdBook 以进行自动部署，请查看 [持续集成][continuous integration] 一章以获取有关如何安装的更多示例。

[continuous integration]: ../continuous-integration.md

## 预编译二进制文件

可执行二进制文件可在 [GitHub 发布页面][releases] 上下载。
下载适用于您的平台（Windows、macOS 或 Linux）的二进制文件并解压缩存档。
该存档包含一个“mdbook”可执行文件，您可以运行它来构建您的书籍。

为了使其更方便运行，请将二进制文件的路径放入您的 `PATH` 中。


[releases]: https://github.com/rust-lang/mdBook/releases

## 从源码构建

要从源代码构建 `mdbook` 可执行文件，您首先需要安装 Rust 和 Cargo。
您可按照 [Rust 安装页面][Rust installation page] 上的说明进行操作。
mdBook 目前至少需要 Rust 版本 1.60。

安装 Rust 后，可以使用以下命令构建和安装 mdBook：

```sh
cargo install mdbook
```

这将自动从 [crates.io] 下载 mdBook，构建它，并将其安装在 Cargo 的全局二进制目录中（默认为 `~/.cargo/bin/`）。

要卸载，请运行命令 `cargo uninstall mdbook`。

[Rust installation page]: https://www.rust-lang.org/tools/install
[crates.io]: https://crates.io/

### 安装最新版本

发布到 crates.io 的版本将略微落后于 GitHub 上托管的版本。
如果您需要最新版本，您可以自己构建 mdBook 的 git 版本。
Cargo 可以让这个***超级简单***！


```sh
cargo install --git https://github.com/rust-lang/mdBook.git mdbook
```

同样，确保将 Cargo bin 目录添加到您的 `PATH` 中。

如果您有兴趣对 mdBook 本身进行修改，请查看 [贡献指南] 以获取更多信息。


[Contributing Guide]: https://github.com/rust-lang/mdBook/blob/master/CONTRIBUTING.md
