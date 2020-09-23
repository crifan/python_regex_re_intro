# re.findall

官网文档：

* 英文
  * [re.findall — Regular expression operations — Python 3 documentation](https://docs.python.org/3/library/re.html#re.findall)
    > **re.findall(pattern, string, flags=0)**
    > 
    > Return all non-overlapping matches of pattern in string, as a list of strings. The string is scanned left-to-right, and matches are returned in the order found. If one or more groups are present in the pattern, return a list of groups; this will be a list of tuples if the pattern has more than one group. Empty matches are included in the result.
    > 
    > Changed in version 3.7: Non-empty matches can now start just after a previous empty match.

* 中文
  * [re.findall --- 正则表达式操作 — Python 3 文档](https://docs.python.org/zh-cn/3/library/re.html#re.findall)
    > **re.findall(pattern, string, flags=0)**
    >
    > 对 string 返回一个不重复的 pattern 的匹配列表， string 从左到右进行扫描，匹配按找到的顺序返回。如果样式里存在一到多个组，就返回一个组合列表；就是一个元组的列表（如果样式里有超过一个组合的话）。空匹配也会包含在结果里。
    >
    > 在 3.7 版更改: 非空匹配现在可以在前一个空匹配之后出现了。
