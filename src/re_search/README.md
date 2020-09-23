# re.search

TODO：之前已写过相关的帖子，抽空把内容整理至此。

* [【教程】详解Python正则表达式之： ‘.’ dot 点 匹配任意单个字符](https://www.crifan.com/detailed_explanation_about_python_regular_express_dot_match_any_single_char)
* [【教程】详解Python正则表达式之： ‘^’ Caret 脱字符/插入符 匹配字符串开始](https://www.crifan.com/detailed_explanation_about_python_regular_express_caret_match_string_start)
* [【教程】详解Python正则表达式之： ‘$’ dollar 美元符号 匹配字符串末尾](https://www.crifan.com/detailed_explanation_about_python_regular_express_dollar_match_string_end)
* [【教程】详解Python正则表达式之： ‘*’ star 星号 匹配0或多个](https://www.crifan.com/detailed_explanation_about_python_regular_express_match_zero_or_more)
* [【教程】详解Python正则表达式之： [] bracket 中括号 匹配某集合内的字符](https://www.crifan.com/detailed_explanation_about_python_regular_express_match_a_set_of_chars)
* [【教程】详解Python正则表达式之： ‘|’ vertical bar 竖杠](https://www.crifan.com/detailed_explanation_about_python_regular_express_about_vertical_bar)
* [【教程】详解Python正则表达式之：\s 匹配任一空白字符](https://www.crifan.com/detailed_explanation_about_python_regular_express_match_any_whitespace_char)
* [【教程】详解Python正则表达式之：re.LOCALE re.L 本地化标志](https://www.crifan.com/detailed_explanation_about_python_regular_express_flag_re_locale_re_l)
* [【教程】详解Python正则表达式之：re.UNICODE re.U 统一码标志](https://www.crifan.com/detailed_explanation_about_python_regular_express_flag_re_unicode_re_u)

和其他一些心得：

* [【已解决】Python 3中用正则匹配多段的脚本内容 – 在路上](https://www.crifan.com/python_3_use_re_regex_match_multiple_part_text_content/)

---

官网文档：

* 英文
  * [re.search — Regular expression operations — Python 3 documentation](https://docs.python.org/3/library/re.html#re.search)
    > **re.search(pattern, string, flags=0)**
    > 
    > Scan through string looking for the first location where the regular expression pattern produces a match, and return a corresponding match object. Return None if no position in the string matches the pattern; note that this is different from finding a zero-length match at some point in the string.
* 中文
  * [re.search --- 正则表达式操作 — Python 3 文档](https://docs.python.org/zh-cn/3/library/re.html#re.search)
    > **re.search(pattern, string, flags=0)**
    >
    > 扫描整个 字符串 找到匹配样式的第一个位置，并返回一个相应的 匹配对象。如果没有匹配，就返回一个 None ； 注意这和找到一个零长度匹配是不同的。
