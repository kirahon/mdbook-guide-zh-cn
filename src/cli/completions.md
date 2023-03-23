#   completions 命令

完成命令用于为一些常见的 shell 生成自动完成。 这意味着当您在 shell 中键入 `mdbook` 时，您可以按下 shell 的自动完成键（通常是 Tab 键），它可能会显示有效选项，或者完成部分输入。

首先需要为您的 shell 安装补全：

```bash
mdbook completions bash > ~/.local/share/bash-completion/completions/mdbook
```

该命令打印给定 shell 的完成脚本。 运行 `mdbook completions --help` 以获得支持的 shell 列表。

在哪里放置补全取决于您使用的 shell 和您的操作系统。 有关放置脚本的位置的更多信息，请参阅您的 shell 文档。
