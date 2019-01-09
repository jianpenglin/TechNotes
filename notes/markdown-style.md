# markdown 编写规范

markdown 编写规范，意在提高文档的可读性，统一性。

## 说明

文档中使用的关键字「MUST」,「MUST NOT」,「REQUIRED」,「SHALL」,「SHALL
NOT」,「SHOULD」,「SHOULD NOT」,「RECOMMENDED」,「MAY」和「OPTIONAL」在 [RFC2119](http://oss.org.cn/man/develop/rfc/RFC2119.txt) 中有说明。

## 例子

```markdown
# Document Title

Short introduction.

[TOC]

## Topic

Content.

## See also

- https://link-to-more-info
```

## 文件

- 文件名后缀必须「MUST」使用 `.md`。
- 文件名必须使用「MUST」小写，多个单词之间使用`-`分隔。
- 文件编码必须「MUST」用 UTF-8。

## Head

- 文档标题应该「SHOULD这样写。

    ```
    # markdown 编写规范
    ```
- 章节标题必须「MUST」以 `##` 开始，而不是 `#`。
- 章节标题必须「MUST」在 `#` 后加一个空格，且后面没有 `#`。

    ```
    // bad
    ##章节1

    // bad
    ## 章节1 ##

    // good
    ## 章节1
    ```

- 章节标题和内容间必须「MUST」有一个空行。

    ```
    // bad
    ## 章节1
    内容
    ## 章节2

    // good
    ## 章节1

    内容

    ## 章节2
    ```

## Lists

### Use lazy numbering for long lists

Markdown is smart enough to let the resulting HTML render your numbered lists
correctly. For longer lists that may change, especially long nested lists, use
"lazy" numbering:

```markdown
1.  Foo.
1.  Bar.
    1.  Foofoo.
    1.  Barbar.
1.  Baz.
```

However, if the list is small and you don't anticipate changing it, prefer fully
numbered lists, because it's nicer to read in source:

```markdown
1.  Foo.
2.  Bar.
3.  Baz.
```

### Nested list spacing

When nesting lists, use a 4 space indent for both numbered and bulleted lists:

```markdown
1.  2 spaces after a numbered list.
    4 space indent for wrapped text.
2.  2 spaces again.

-   3 spaces after a bullet.
    4 space indent for wrapped text.
    1.  2 spaces after a numbered list.
        8 space indent for the wrapped text of a nested list.
    2.  Looks nice, don't it?
-   3 spaces after a bullet.
```

The following works, but it's very messy:

```markdown
- One space,
with no indent for wrapped text.
     1. Irregular nesting... DO NOT DO THIS.
```

Even when there's no nesting, using the 4 space indent makes layout consistent
for wrapped text:

```markdown
-   Foo,
    wrapped.

1.  2 spaces
    and 4 space indenting.
2.  2 spaces again.
```

However, when lists are small, not nested, and a single line, one space can
suffice for both kinds of lists:

```markdown
- Foo
- Bar
- Baz.

1. Foo.
2. Bar.
```

## Code

### 总则

- 代码段的必须「MUST」使用 Fenced code blocks 风格，如下所示：

        ```
        console.log("");
        ```
- 缩进使用4个空格

### Inline

&#96;Backticks&#96; designate `inline code`, and will render all wrapped content
literally. Use them for short code quotations and field names:

```markdown
You'll want to run `really_cool_script.sh arg`.

Pay attention to the `foo_bar_whammy` field in that table.
```

Use inline code when referring to file types in an abstract sense, rather than a
specific file:

```markdown
Be sure to update your `README.md`!
```

Backticks are the most common approach for "escaping" Markdown metacharacters;
in most situations where escaping would be needed, code font just makes sense
anyway.

### Codeblocks

For code quotations longer than a single line, use a codeblock:

<pre>
```python
def Foo(self, bar):
  self.bar = bar
```
</pre>

#### Declare the language

It is best practice to explicitly declare the language, so that neither the
syntax highlighter nor the next editor must guess.

#### Indented codeblocks are sometimes cleaner

Four-space indenting is also interpreted as a codeblock. These can look
cleaner and be easier to read in source, but there is no way to specify the
language. We encourage their use when writing many short snippets:

```markdown
You'll need to run:

    bazel run :thing -- --foo

And then:

    bazel run :another_thing -- --bar

And again:

    bazel run :yet_again -- --baz
```

#### Escape newlines

Because most commandline snippets are intended to be copied and pasted directly
into a terminal, it's best practice to escape any newlines. Use a single
backslash at the end of the line:

<pre>
```shell
bazel run :target -- --flag --foo=longlonglonglonglongvalue \
--bar=anotherlonglonglonglonglonglonglonglonglonglongvalue
```
</pre>

#### Nest codeblocks within lists

If you need a codeblock within a list, make sure to indent it so as to not break
the list:

```markdown
-   Bullet.

    ```c++
    int foo;
    ```

-   Next bullet.
```

You can also create a nested code block with 4 spaces. Simply indent 4
additional spaces from the list indentation:

```markdown
-   Bullet.

        int foo;

-   Next bullet.
```

## Links

Long links make source Markdown difficult to read and break the 80 character
wrapping. **Wherever possible, shorten your links**.

### Use informative Markdown link titles

Markdown link syntax allows you to set a link title, just as HTML does. Use it
wisely.

Titling your links as "link" or "here" tells the reader precisely nothing when
quickly scanning your doc and is a waste of space:

```markdown
See the syntax guide for more info: [link](syntax_guide.md).
Or, check out the style guide [here](style_guide.md).
DO NOT DO THIS.
```

Instead, write the sentence naturally, then go back and wrap the most
appropriate phrase with the link:

```markdown
See the [syntax guide](syntax_guide.md) for more info.
Or, check out the [style guide](style_guide.md).
```

## Images

Use images sparingly, and prefer simple screenshots. This guide is designed
around the idea that plain text gets users down to the business of communication
faster with less reader distraction and author procrastination. However, it's
sometimes very helpful to show what you mean.

See [image syntax](https://gerrit.googlesource.com/gitiles/+/master/Documentation/markdown.md#Images).

## Grid

- 表格的写法应该参考 [GFM](https://help.github.com/articles/organizing-information-with-tables/)，如下所示：

    ```
    First Header  | Second Header
    ------------- | -------------
    Content Cell  | Content Cell
    Content Cell  | Content Cell

    | Left-Aligned  | Center Aligned  | Right Aligned |
    | :------------ |:---------------:| -----:|
    | col 3 is      | some wordy text | $1600 |
    | col 2 is      | centered        |   $12 |
    | zebra stripes | are neat        |    $1 |
    ```
## Content

### 中英文混排应该「SHOULD」采用如下规则：

- 英文和数字使用半角字符
- 中文文字之间不加空格
- 中文文字与英文、阿拉伯数字及 @ # $ % ^ & * . ( ) 等符号之间加空格
- 中文标点之间不加空格
- 中文标点与前后字符（无论全角或半角）之间不加空格
- 如果括号内有中文，则使用中文括号
- 如果括号中的内容全部都是英文，则使用半角英文括号
- 当半角符号 / 表示「或者」之意时，与前后的字符之间均不加空格
- 其它具体例子推荐[阅读这里](https://github.com/sparanoid/chinese-copywriting-guidelines)

### 中文符号应该「SHOULD」使用如下写法：

- 用直角引号（「」）代替双引号（“”），不同输入法的具体设置方法请[参考这里](http://www.zhihu.com/question/19755746)
- 省略号使用「……」，而「。。。」仅用于表示停顿
- 其它可以参考[知乎规范](http://www.zhihu.com/question/20414919)

### 表达方式，应当「SHOULD」遵循《The Element of Style》：

- 使段落成为文章的单元：一个段落只表达一个主题
- 通常在每一段落开始要点题，在段落结尾要扣题
- 使用主动语态
- 陈述句中使用肯定说法
- 删除不必要的词
- 避免连续使用松散的句子
- 使用相同的结构表达并列的意思
- 将相关的词放在一起
- 在总结中，要用同一种时态（这里指英文中的时态，中文不适用，所以可以不理会）
- 将强调的词放在句末

## Strongly prefer Markdown to HTML

Please prefer standard Markdown syntax wherever possible and avoid HTML hacks.
If you can't seem to accomplish what you want, reconsider whether you really
need it. Except for [big tables](#prefer-lists-to-tables), Markdown meets almost
all needs already.

Every bit of HTML or Javascript hacking reduces the readability and portability.
This in turn limits the usefulness of integrations with
other tools, which may either present the source as plain text or render it. See
[Philosophy](philosophy.md).

Gitiles does not render HTML.

## 扩展阅读

- Google  [Markdown 规范](https://github.com/google/styleguide/blob/gh-pages/docguide/style.md)，可以参考
