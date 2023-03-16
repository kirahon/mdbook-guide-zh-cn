# SUMMARY.md

mdBook 使用摘要文件来了解要包含哪些章节、它们应该以什么顺序出现、它们的层次结构是什么以及源文件在哪里。 没有这个文件，就没有这本书。

此 markdown 必须命名为 `SUMMARY.md`。 它的格式非常严格，必须遵循下面概述的结构以便于解析。 下面未指定的任何元素，无论是格式还是文本，都可能被忽略，或者在尝试构建本书时导致错误。


### 结构

1. ***标题*** - 虽然是可选的，但以标题开头是常见的做法，通常是 `# Summary`. 不过解析器在解析时会忽略它，并且可以省略。 
   ```markdown
   # Summary
   ```

1. ***前缀章节*** - 在主要编号章节之前，可以添加不会被编号的前缀章节。 这对前言，介绍等很有用。但是前缀章节有一些限制。前缀章节不能嵌套且都应该在根级别。 你不能在编号章节后，添加前缀章节。
   ```markdown
   [A Prefix Chapter](relative/path/to/markdown.md)

   - [First Chapter](relative/path/to/markdown2.md)
   ```

2. ***分割标题*** - 分割标题作为编号章节的标题。 这可用于在逻辑上分隔本书的不同部分。 分割标题呈现为不可点击的文本。分割标题是可选的，编号的章节可以根据需要被分成多个部分。
   ```markdown
   # My Part Title

   - [First Chapter](relative/path/to/markdown.md)
   ```

3. ***编号章节*** - 带编号的章节概述了本书的主要内容，并且可以嵌套，形成好的层次结构
   ```markdown
   # Title of Part

   - [First Chapter](relative/path/to/markdown.md)
   - [Second Chapter](relative/path/to/markdown2.md)
      - [Sub Chapter](relative/path/to/markdown3.md)

   # Title of Another Part

   - [Another Chapter](relative/path/to/markdown4.md)
   ```
   Numbered chapters can be denoted with either `-` or `*` (do not mix delimiters). 
   
4. ***后缀章节*** - 与前缀章节一样，后缀章节没有编号，但它们位于编号章节之后。
   ```markdown
   - [Last Chapter](relative/path/to/markdown.md)

   [Title of Suffix Chapter](relative/path/to/markdown2.md)
   ```

5. ***草稿章节*** - 草稿章节是没有文件和内容的章节。
    草稿章节的目的是表明未来的章节仍有待编写。
    草稿章节将在 HTML 呈现器中呈现为目录中的禁用链接，正如您在左侧目录中看到的下一章一样。
    草稿章节的编写方式与普通章节一样，但没有写入文件路径。
   ```markdown
   - [Draft Chapter]()
   ```

6. ***分隔符*** - 可以在任何其他元素之前、之间和之后添加分隔符。 它们会在构建的目录中生成 HTML 渲染行。 分隔符是仅包含破折号且至少包含三个破折号的行: `---`.
   ```markdown
   # My Part Title
   
   [A Prefix Chapter](relative/path/to/markdown.md)

   ---

   - [First Chapter](relative/path/to/markdown2.md)
   ```
  

### 例子

下面是本指南的 `SUMMARY.md` 的 markdown 源代码，结果目录呈现在左侧。

```markdown
{{#include ../SUMMARY.md}}
```
