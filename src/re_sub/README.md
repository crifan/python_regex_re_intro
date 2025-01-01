# re.sub

## 概述

* re.sub
  * 语法
    ```bash
    re.sub(pattern, repl, string, count=0, flags=0)
    ```

## 文档

官网文档：

* 英文
  * [re.sub — Regular expression operations — Python 3 documentation](https://docs.python.org/3/library/re.html#re.sub)
    > **re.sub(pattern, repl, string, count=0, flags=0)**
    > 
    > Return the string obtained by replacing the leftmost non-overlapping occurrences of pattern in string by the replacement repl. If the pattern isn’t found, string is returned unchanged. repl can be a string or a function; if it is a string, any backslash escapes in it are processed. That is, `\n` is converted to a single newline character, `\r` is converted to a carriage return, and so forth. Unknown escapes of ASCII letters are reserved for future use and treated as errors. Other unknown escapes such as `\&` are left alone. Backreferences, such as `\6`, are replaced with the substring matched by group `6` in the pattern. For example:
    >
    ```python
    >>> re.sub(r'def\s+([a-zA-Z_][a-zA-Z_0-9]*)\s*\(\s*\):',
    ...        r'static PyObject*\npy_\1(void)\n{',
    ...        'def myfunc():')
    'static PyObject*\npy_myfunc(void)\n{'
    ```
    >
    > If repl is a function, it is called for every non-overlapping occurrence of pattern. The function takes a single [match object](https://docs.python.org/3/library/re.html#match-objects) argument, and returns the replacement string. For example:
    ```python
    >>> def dashrepl(matchobj):
    ...     if matchobj.group(0) == '-': return ' '
    ...     else: return '-'
    >>> re.sub('-{1,2}', dashrepl, 'pro----gram-files')
    'pro--gram files'
    >>> re.sub(r'\sAND\s', ' & ', 'Baked Beans And Spam', flags=re.IGNORECASE)
    'Baked Beans & Spam'
    ```
    > 
    > The pattern may be a string or a [pattern object](https://docs.python.org/3/library/re.html#re-objects).
    > 
    > The optional argument count is the maximum number of pattern occurrences to be replaced; count must be a non-negative integer. If omitted or zero, all occurrences will be replaced. Empty matches for the pattern are replaced only when not adjacent to a previous empty match, so `sub('x*', '-', 'abxd')` returns `'-a-b--d-'`.
    > 
    > In string-type repl arguments, in addition to the character escapes and backreferences described above, `\g<name>` will use the substring matched by the group named `name`, as defined by the `(?P<name>...)` syntax. `\g<number>` uses the corresponding group number; `\g<2>` is therefore equivalent to `\2`, but isn’t ambiguous in a replacement such as `\g<2>0`. `\20` would be interpreted as a reference to group 20, not a reference to group 2 followed by the literal character `'0'`. The backreference `\g<0>` substitutes in the entire substring matched by the RE.
    > 
    > * Change Log
    >   * Changed in version 3.1: Added the optional flags argument.
    >   * Changed in version 3.5: Unmatched groups are replaced with an empty string.
    >   * Changed in version 3.6: Unknown escapes in pattern consisting of `'\'` and an ASCII letter now are errors.
    >   * Changed in version 3.7: Unknown escapes in repl consisting of `'\'` and an ASCII letter now are errors.
    >   * Changed in version 3.7: Empty matches for the pattern are replaced when adjacent to a previous non-empty match.
* 中文
  * [re.sub --- 正则表达式操作 — Python 3 文档](https://docs.python.org/zh-cn/3/library/re.html#re.sub)
    > **re.sub(pattern, repl, string, count=0, flags=0)**
    >
    > 返回通过使用 _repl_ 替换在 _string_ 最左边非重叠出现的 _pattern_ 而获得的字符串。 如果样式没有找到，则不加改变地返回 _string_。 _repl_ 可以是字符串或函数；如为字符串，则其中任何反斜杠转义序列都会被处理。 也就是说，`\n` 会被转换为一个换行符，`\r` 会被转换为一个回车附，依此类推。 未知的 `ASCII` 字符转义序列保留在未来使用，会被当作错误来处理。 其他未知转义序列例如 `\&` 会保持原样。 向后引用像是 `\6` 会用样式中第 6 组所匹配到的子字符串来替换。 例如:
    ```python
    >>> re.sub(r'def\s+([a-zA-Z_][a-zA-Z_0-9]*)\s*\(\s*\):',
    ...        r'static PyObject*\npy_\1(void)\n{',
    ...        'def myfunc():')
    'static PyObject*\npy_myfunc(void)\n{'
    ```
    >
    > 如果 _repl_ 是一个函数，那它会对每个非重复的 _pattern_ 的情况调用。这个函数只能有一个 匹配对象 参数，并返回一个替换后的字符串。比如
    > 
    ```python
    >>> def dashrepl(matchobj):
    ...     if matchobj.group(0) == '-': return ' '
    ...     else: return '-'
    >>> re.sub('-{1,2}', dashrepl, 'pro----gram-files')
    'pro--gram files'
    >>> re.sub(r'\sAND\s', ' & ', 'Baked Beans And Spam', flags=re.IGNORECASE)
    'Baked Beans & Spam'
    ```
    >
    > 样式可以是一个字符串或者一个 [样式对象](https://docs.python.org/zh-cn/3/library/re.html#re-objects) 。
    >
    > 可选参数 _count_ 是要替换的最大次数；_count_ 必须是非负整数。如果忽略这个参数，或者设置为0，所有的匹配都会被替换。空匹配只在不相临连续的情况被更替，所以 `sub('x*', '-', 'abxd')` 返回 `'-a-b--d-'` 。
    >
    > 在字符串类型的 _repl_ 参数里，如上所述的转义和向后引用中，`\g<name>` 会使用命名组合 name，（在 `(?P<name>…)` 语法中定义） `\g<number>` 会使用数字组；`\g<2>` 就是 `\2`，但它避免了二义性，如 `\g<2>0`。 `\20` 就会被解释为组20，而不是组2后面跟随一个字符 `'0'`。向后引用 `\g<0>` 把 _pattern_ 作为一整个组进行引用。
    >
    > * 更新日志
    >   * 在 3.1 版更改: 增加了可选标记参数。
    >   * 在 3.5 版更改: 不匹配的组合替换为空字符串。
    >   * 在 3.6 版更改: _pattern_ 中的未知转义（由 `'\'` 和一个 `ASCII` 字符组成）被视为错误。
    >   * 在 3.7 版更改: _repl_ 中的未知转义（由 `'\'` 和一个 `ASCII` 字符组成）被视为错误。
    >   * 在 3.7 版更改: 样式中的空匹配相邻接时会被替换。

## 举例

把

```markdown
最后更新：`20190825`
```

中的日期换成最新的，比如`20200919`

则可以用代码：

```py
oldReamdMdStr = "最后更新：`20190825`"
newLastUpdateStr = "最后更新：`20200919`"
newReamdMdStr = re.sub("最后更新：`\d+`", newLastUpdateStr, oldReamdMdStr)
```

详细过程可参考：

* 【已解决】给crifan的gitbook的template添加部署时更新github.io的README
