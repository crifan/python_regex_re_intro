# match vs findall vs finditer

## 背景需求

希望从自己的[Crifan的电子书的使用说明](https://github.com/crifan/crifan_ebook_readme)的[README.md](https://raw.githubusercontent.com/crifan/crifan_ebook_readme/master/README.md)中提取相关book的信息，比如url，name，title等。

## re.search处理单行，返回匹配对象`Match Object`

对于普通的，单行字符串：

```markdown
* [科学上网](https://book.crifan.com/books/scientific_network_summary/website)
```

一般用`re.search`代码去查找：

```python
foundBook = re.search("https?://book\.crifan\.com/books/(?P<bookName>\w+)/website", singleLineMdStr)
print("foundBook=%s" % foundBook)
```

代码解析：

* `https?` = `https`加上问号`?`
  * 表示：`http`后面，可能有`s`，也可能没有`s`
  * 用于匹配：`http://xxx`和`https://xxx`的链接
* `(?P<bookName>\w+)`
  * 典型的`named group`=`命名的组`的写法
    * 语法：`(?P<yourGroupName>match_pattern)`
      * 此处
        * `yourGroupName` = `bookName`
          * 用于：若匹配到，后续可通过`foundBook.group("bookName")`提取这部分的值
        * `match_pattern` = `\w+`
          * 表示：至少1个（1个或更多个）的大小写字母或下划线
          * 用于匹配：此处的`scientific_network_summary`

得到的是一个`Match Object`

```bash
foundBook=<re.Match object; span=(9, 73), match='https://book.crifan.com/books/scientific_network_>
```

后来典型写法就是提取出所需的部分，比如

```python
if foundBook:
  bookName = foundBook.group("bookName")
  print("bookName=%s" % bookName)
```

得到book的name：

```bash
bookName=scientific_network_summary
```

### re.findall处理多行，返回整个匹配字符串或group部分的字符串

对于多行字符串：

```markdown
* 推荐工具
  * [科学上网](https://book.crifan.com/books/scientific_network_summary/website)
  * 编辑器和IDE
    * [总结](https://book.crifan.com/books/editor_ide_summary/website/)
    * 好用工具
      * [VSCode](http://book.crifan.com/books/best_editor_vscode/website)
```

#### 返回单条全部内容

如果只是想要获取所有的book的url，则可以用`re.findall`，且不要加组group：

```python
allBookUrlList = re.findall("https?://book\.crifan\.com/books/\w+/website", multipleLineDdStr)
print("allBookUrlList=%s" % allBookUrlList)
```

输出：

```bash
allBookUrlList=['https://book.crifan.com/books/scientific_network_summary/website', 'https://book.crifan.com/books/editor_ide_summary/website', 'http://book.crifan.com/books/best_editor_vscode/website']
```

#### 返回单条中的部分内容=组的内容

如果只想要获取，每条匹配的内容中的其中一部分，即其中某个或某几个group组的内容，则加上group：

```python
allBookNameList = re.findall("https?://book\.crifan\.com/books/(?P<bookName>\w+)/website", multipleLineDdStr, re.S)
print("allBookNameList=%s" % allBookNameList)
```

输出：

```bash
# allBookNameList=['scientific_network_summary', 'editor_ide_summary', 'best_editor_vscode']
```

#### re.findall的两种用法对比

* re.findall的两种用法对比
  * 规则：`"https?://book\.crifan\.com/books/\w+/website"`
    * 不带group组
      * 返回：单条匹配的所有内容，即whole single match string
        * 举例：
          * `'https://book.crifan.com/books/scientific_network_summary/website'`
  * 规则：`https?://book\.crifan\.com/books/(?P<bookName>\w+)/website`
    * 带group组
      * 返回：单条匹配到的所有内容中的其中一部分，即group组的部分，matched group string
        * 举例：
          * `'scientific_network_summary'`

### re.finditer处理多行，返回多个(re.search所返回的)匹配对象

而对于re.finditer，可以视为 = `re.findall` + `re.search`

即：就像`re.findall`一样，返回多个值，但是每个值，不是`re.findall`直接返回（匹配到的）字符串，而是(re.search所返回的)匹配的对象`Match Object`

下面用具体例子来解释：

#### `re.finditer`内部就像`re.findall`

和之前一样，想要返回所有的book的url，则可以写成：

```python
allBookUrlMatchObjIterator = re.finditer("https?://book\.crifan\.com/books/\w+/website", multipleLineDdStr)
print("allBookUrlMatchObjIterator=%s" % allBookUrlMatchObjIterator)
```

此处注意返回的是`iterator`：

```bash
# allBookUrlMatchObjIterator=<callable_iterator object at 0x11063f160>
```

可以将其转换为`list`：

```python
allBookUrlMatchObjList = list(allBookUrlMatchObjIterator)
print("allBookUrlMatchObjList=%s" % allBookUrlMatchObjList)
```

得到了`Match Object`的`list`:

```bash
# allBookUrlMatchObjList=[<re.Match object; span=(19, 83), match='https://book.crifan.com/books/scientific_network_>, <re.Match object; span=(108, 164), match='https://book.crifan.com/books/editor_ide_summary/>, <re.Match object; span=(195, 250), match='http://book.crifan.com/books/best_editor_vscode/w>]
```

接着就可以对list去枚举处理了：

```python
for curIdx, eachMatchObj in enumerate(allBookUrlMatchObjList):
  singleMatchWholeStr = eachMatchObj.group(0)
  print("[%d] singleMatchWholeStr=%s" % (curIdx, singleMatchWholeStr))
```

从每个匹配的对象获取所需要的完整的url值：

```bash
# [0] singleMatchWholeStr=https://book.crifan.com/books/scientific_network_summary/website
# [1] singleMatchWholeStr=https://book.crifan.com/books/editor_ide_summary/website
# [2] singleMatchWholeStr=http://book.crifan.com/books/best_editor_vscode/website
```

#### `re.finditer`内部就像`re.search`

而如果想要一次性的匹配得到多个匹配对象`Match Object`，且每个都可以提取对应的group组的值，则可以给规则中加上group组：

```python
allBookNameMatchObjIterator = re.finditer("https?://book\.crifan\.com/books/(?P<bookName>\w+)/website", multipleLineDdStr)
print("allBookNameMatchObjIterator=%s" % allBookNameMatchObjIterator)
```

同理先是得到`iterator`：

```bash
# allBookNameMatchObjIterator=<callable_iterator object at 0x10e9a9fd0>
```

再转换为`list`：

```python
allBookNameMatchObjList = list(allBookNameMatchObjIterator)
print("allBookNameMatchObjList=%s" % allBookNameMatchObjList)
```

即多个匹配对象：

```bash
# allBookNameMatchObjList=[<re.Match object; span=(19, 83), match='https://book.crifan.com/books/scientific_network_>, <re.Match object; span=(108, 164), match='https://book.crifan.com/books/editor_ide_summary/>, <re.Match object; span=(195, 250), match='http://book.crifan.com/books/best_editor_vscode/w>]
```

然后继续针对每个匹配对象去处理：

```python
for curIdx, eachMatchObj in enumerate(allBookNameMatchObjList):
  singleMatchWholeStr = eachMatchObj.group(0)
  singleMatchBookName = eachMatchObj.group("bookName")
  print("[%d] singleMatchWholeStr=%s, singleMatchBookName=%s" % (curIdx, singleMatchWholeStr, singleMatchBookName))
```

即可，既能获取到 单个匹配的完整字符串，又能获取到 每个匹配的全部字符串中特定的组的内容了：

```bash
# [0] singleMatchWholeStr=https://book.crifan.com/books/scientific_network_summary/website, singleMatchBookName=scientific_network_summary
# [1] singleMatchWholeStr=https://book.crifan.com/books/editor_ide_summary/website, singleMatchBookName=editor_ide_summary
# [2] singleMatchWholeStr=http://book.crifan.com/books/best_editor_vscode/website, singleMatchBookName=best_editor_vscode
```

附录：

完整代码详见：

[reSearchFindallFinditer.py](https://book.crifan.com/books/python_regex_re_intro/website/assets/file/reSearchFindallFinditer.py)
