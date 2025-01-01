# 更新crifan的github.io中README.md中book的list

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
