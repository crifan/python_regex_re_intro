# re.match

官网文档：

* 英文
  * [re.match — Regular expression operations — Python 3 documentation](https://docs.python.org/3/library/re.html#re.match)
    > **re.match(pattern, string, flags=0)**
    >
    > If zero or more characters at the beginning of string match the regular expression pattern, return a corresponding [match object](https://docs.python.org/3/library/re.html#match-objects). Return `None` if the string does not match the pattern; note that this is different from a zero-length match.
    >
    > Note that even in [MULTILINE](https://docs.python.org/3/library/re.html#re.MULTILINE) mode, [re.match()](https://docs.python.org/3/library/re.html#re.match) will only match at the beginning of the string and not at the beginning of each line.
    >
    > If you want to locate a match anywhere in string, use [search()](https://docs.python.org/3/library/re.html#re.search) instead (see also [search() vs. match()](https://docs.python.org/3/library/re.html#search-vs-match)).
* 中文
  * [re.match --- 正则表达式操作 — Python 3 文档](https://docs.python.org/zh-cn/3/library/re.html#re.match)
    > **re.match(pattern, string, flags=0)**
    >
    > 如果 _string_ 开始的0或者多个字符匹配到了正则表达式样式，就返回一个相应的 [匹配对象](https://docs.python.org/zh-cn/3/library/re.html#match-objects) 。 如果没有匹配，就返回 `None` ；注意它跟零长度匹配是不同的。
    >
    > 注意即便是 [MULTILINE](https://docs.python.org/zh-cn/3/library/re.html#re.MULTILINE) 多行模式， [re.match()](https://docs.python.org/zh-cn/3/library/re.html#re.match) 也只匹配字符串的开始位置，而不匹配每行开始。
    >
    > 如果你想定位 _string_ 的任何位置，使用 [search()](https://docs.python.org/zh-cn/3/library/re.html#re.search) 来替代（也可参考 [search() vs. match()](https://docs.python.org/zh-cn/3/library/re.html#search-vs-match) ）
