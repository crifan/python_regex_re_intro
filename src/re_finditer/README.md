# re.finditer

`re.finditer` = **iter**ator of `re.findall`=针对`re.findall`所返回的字符串相对，每个都是一个匹配的对象`MatchedObject`

对比：

* `findall`：返回`str`的list
* `finditer`：返回`MatchObject`的迭代器`iterator`
  * 可以针对每个匹配到的字符串，获取其中的`sub group`了

官网文档：

* 英文
  * [re — Regular expression operations — Python 3.8.3 documentation](https://docs.python.org/3/library/re.html#re.finditer)
    > **re.finditer(pattern, string, flags=0)**
    > 
    >   Return an iterator yielding match objects over all non-overlapping matches for the RE pattern in string. The string is scanned left-to-right, and matches are returned in the order found. Empty matches are included in the result.
    > 
    >  Changed in version 3.7: Non-empty matches can now start just after a previous empty match.
* 中文
  * [re --- 正则表达式操作 — Python 3.8.3 文档](https://docs.python.org/zh-cn/3/library/re.html#re.finditer)
    > **re.finditer(pattern, string, flags=0)**
    >
    > pattern 在 string 里所有的非重复匹配，返回为一个迭代器 iterator 保存了 匹配对象 。 string 从左到右扫描，匹配按顺序排列。空匹配也包含在结果里。
    > 
    > 在 3.7 版更改: 非空匹配现在可以在前一个空匹配之后出现了。

## 心得

### iter对象无法被重复访问

Python中的iterator类型变量，只能被访问（使用/遍历）一次，就空了。无法被重复使用。

用代码举例如下：

```python
matchIter = re.finditer(someP, someStr)
for eachMatch in matchIter:
  print("matchIter=%s" % matchIter)

resultList = list(matchIter) # -> will error, matchIter already None
```
