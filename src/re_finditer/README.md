# re.finditer

`re.finditer` = **iter**ator of `re.findall`=针对`re.findall`所返回的字符串相对，每个都是一个匹配的对象`MatchedObject`

对比：

* `findall`：返回`str`的list
* `finditer`：返回`MatchObject`的迭代器`iterator`
  * 可以针对每个匹配到的字符串，获取其中的`sub group`了

可以理解为：

`re.finditer` = `re.findall` + 每个字符串再用`re.search`处理

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

## 举例

### 更新crifan的github.io中README.md中book的list

之前折腾：

【已解决】给crifan的gitbook的template添加部署时更新github.io的README

期间，需要对于：

```markdown
    * [老少皆宜的运动：羽毛球](https://crifan.github.io/all_age_sports_badminton/website)
    * [app抓包利器：Charles](https://crifan.github.io/app_capture_package_tool_charles/website)
    * [安卓应用的安全和破解](https://crifan.github.io/android_app_security_crack/website)
```

去提取出，每个book的中文名称`bookTitle`，和对应的git仓库地址`bookRepoName`

可以写成：

```python
allBookMatchList = re.finditer("\[(?P<bookTitle>[^]]+)\]\(https://crifan\.github\.io/(?P<bookRepoName>\w+)/website\)", curGitbookListMd)
```

即可获取到对应匹配到的，Match对象的列表

其中每个元素都是一个Match对象，即每个元素都相当于用`re.search`去匹配到的结果

所以可以用循环，依次从每个Match对象中，提取出我们要的`bookTitle`和`bookRepoName`了：

```python
  curBookDict = {}
  for curIdx, eachBookMatch in enumerate(allBookMatchList):
    # print("eachBookMatch=%s" % eachBookMatch)
    # print("%s %s %s" % ("-"*10, curIdx, "-"*10))
    bookTitle = eachBookMatch.group("bookTitle")
    # print("bookTitle=%s" % bookTitle)
    bookRepoName = eachBookMatch.group("bookRepoName")
    # print("bookRepoName=%s" % bookRepoName)
    curBookDict[bookRepoName] = bookTitle
```
