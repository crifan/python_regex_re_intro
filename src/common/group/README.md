# 分组group

TODO：把下面之前写的帖子的内容整理至此

* [【教程】详解Python正则表达式之： (…) group 分组](https://www.crifan.com/detailed_explanation_about_python_regular_express_about_group/)
* [【教程】详解Python正则表达式之： (?…) extension notation 扩展助记符](https://www.crifan.com/detailed_explanation_about_python_regular_express_extension_notation)
* [【教程】详解Python正则表达式之： (?:…) non-capturing group 非捕获组](https://www.crifan.com/detailed_explanation_about_python_regular_express_non_capturing_group)
* [【教程】详解Python正则表达式之： \(?P<name>…\) named group 带命名的组](https://www.crifan.com/detailed_explanation_about_python_regular_express_named_group)
* [【教程】详解Python正则表达式之： (?P=name) match earlier named group 匹配前面已命名的组](https://www.crifan.com/detailed_explanation_about_python_regular_express_match_named_group)
* [【教程】详解Python正则表达式之： (?(id/name)yes-pattern|no-pattern) 条件性匹配](https://www.crifan.com/detailed_explanation_about_python_regular_express_yes_or_no_conditional_match)
* [【教程】详解Python正则表达式之： (?=…) lookahead assertion 前向匹配 /前向断言](https://www.crifan.com/detailed_explanation_about_python_regular_express_lookahead_assertion)
* [【教程】详解Python正则表达式之： (?<=…) positive lookbehind assertion 后向匹配 /后向断言](https://www.crifan.com/detailed_explanation_about_python_regular_express_positive_lookbehind_assertion)
* [【教程】详解Python正则表达式之： (?<=…) positive lookbehind assertion 后向匹配 /后向断言](https://www.crifan.com/detailed_explanation_about_python_regular_express_positive_lookbehind_assertion)

---

## 概述

* `普通的组` = `normal group`
  * 语法
    ```bash
    (...)
    ```
* `捕获的组` = `capturing group` = `captured group` = `命名的组` = `named group`
  * 语法
    ```bash
    (?P<name>...)
    ```
* `非捕获的组` = `non-capturing group` = 不带命名的组
  * 语法：
    ```bash
    (?:...)
    ```

## 文档

官网的

* [英文解释](https://docs.python.org/3/library/re.html#regular-expression-syntax)

```bash
(?...)
    This is an extension notation (a '?' following a '(' is not meaningful otherwise).
    The first character after the '?' determines what the meaning and further syntax of the construct is.
    Extensions usually do not create a new group; (?P<name>...) is the only exception to this rule.
    Following are the currently supported extensions.

(?:...)
    A non-capturing version of regular parentheses.
    Matches whatever regular expression is inside the parentheses,
    but the substring matched by the group cannot be retrieved after performing a match or referenced later in the pattern.

(?P<name>...)
    Similar to regular parentheses, but the substring matched by the group is accessible via the symbolic group name name.
    Group names must be valid Python identifiers, and each group name must be defined only once within a regular expression.
    A symbolic group is also a numbered group, just as if the group were not named.
```

* [中文解释](https://docs.python.org/zh-cn/3/library/re.html#regular-expression-syntax)

```bash
(?…)
这是个扩展标记法 （一个 '?' 跟随 '(' 并无含义）。
'?' 后面的第一个字符决定了这个构建采用什么样的语法。
这种扩展通常并不创建新的组合； (?P<name>...) 是唯一的例外。 以下是目前支持的扩展。

(?:…)
正则括号的非捕获版本。 匹配在括号内的任何正则表达式，
但该分组所匹配的子字符串 不能 在执行匹配后被获取或是之后在模式中被引用。

(?P<name>…)
（命名组合）类似正则组合，但是匹配到的子串组在外部是通过定义的 name 来获取的。
组合名必须是有效的Python标识符，并且每个组合名只能用一个正则表达式定义，只能定义一次。
一个符号组合同样是一个数字组合，就像这个组合没有被命名一样。

命名组合可以在三种上下文中引用。
如果样式是 (?P<quote>['"]).*?(?P=quote) 
（也就是说，匹配单引号或者双引号括起来的字符串)：

引用组合 "quote" 的上下文         引用方法
在正则式自身内                    (?P=quote) (如示)
                                \1
处理匹配对象 m                    m.group('quote')
                                m.end('quote') (等)
传递到 re.sub() 里的 repl 参数中   \g<quote>
                                \g<1>
                                \1
```
