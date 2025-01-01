# 环视断言

## 概述

* `环视断言` = `look around (assertion)`
  * 包括
    * `look ahead (assertion)`=`正向断言`
      * `positive lookahead assertion` ：`(?=xxx)`
      * `negative lookahead assertion` ：`(?!xxx)`
    * `look behind (assertion)`=`反向断言`
      * `positive lookbehind assertion`：`(?<=xxx)`
      * `negative lookbehind assertion`：`(?<!xxx)`

如果觉得look ahead和look behind很费解的话，看这个图，就容易懂了：

![python_look_ahead_and_look_behind](../../../assets/img/python_look_ahead_and_look_behind.png)

总体就2个逻辑：

* 站在 当前所要匹配的内容
  * 往哪看
    * ahead：向前 向右 ➡️ 当前字符串继续往后的方向
      * **从左到右** 叫做 向前，属于正向
    * behind：向左 ◀️ 向后 ⬅️ 当前字符串之前的方向
      * 所以会额外加上一个 `<`**小于号** 表示向后看的意思
        * `(?<=xxx)`
        * `(?<!xxx)`
  * positive/negative：
    * positive=正面的，肯定的，用 **等于号**`=`，意思是：`=xxx`
    * negative=负面的，否定的，用 **不等于号**`!`，意思是：`!=xxx`

==》因此推导出：

* `positive lookahead assertion`：`(?=xxx)`
* `negative lookahead assertion`：`(?!xxx)`
* `positive lookbehind assertion`： `(?<=xxx)`
* `negative lookbehind assertion`：`(?<!xxx)`

## 文档

[官网](https://docs.python.org/3/library/re.html#regular-expression-syntax)文档：

```bash
(...)
    Matches whatever regular expression is inside the parentheses, and indicates the start and end of a group;
    the contents of a group can be retrieved after a match has been performed,
    and can be matched later in the string with the \number special sequence, described below.
    To match the literals '(' or ')', use \( or \), or enclose them inside a character class: [(], [)].


(?=...)
    Matches if ... matches next, but doesn’t consume any of the string.
    This is called a lookahead assertion.
    For example, Isaac (?=Asimov) will match 'Isaac ' only if it’s followed by 'Asimov'.


(?!...)
    Matches if ... doesn’t match next.
    This is a negative lookahead assertion.
    For example, Isaac (?!Asimov) will match 'Isaac ' only if it’s not followed by 'Asimov'.


(?<=...)
    Matches if the current position in the string is preceded by a match for ... that ends at the current position.
    This is called a positive lookbehind assertion.
    (?<=abc)def will find a match in 'abcdef', since the lookbehind will back up 3 characters and check if the contained pattern matches.
    The contained pattern must only match strings of some fixed length, meaning that abc or a|b are allowed, but a* and a{3,4} are not.
    Note that patterns which start with positive lookbehind assertions will not match at the beginning of the string being searched;


(?<!...)
    Matches if the current position in the string is not preceded by a match for ....
    This is called a negative lookbehind assertion.
    Similar to positive lookbehind assertions, the contained pattern must only match strings of some fixed length.
    Patterns which start with negative lookbehind assertions may match at the beginning of the string being searched.
```

