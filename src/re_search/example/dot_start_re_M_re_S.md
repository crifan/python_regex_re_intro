# 点和星 + re.M + re.S

## 点`.`和星`*`

普通的html中的title，一般格式是：

```html
<!DOCTYPE html><html lang="zh-cn">\n<head>  。。。  <title>三维推关于短网址_二维码_多场景应用过期使用提醒</title> 。。。</body></html>
```

此处想要去匹配其中的title中的内容

所以用

* 语法：`.+`
  * `.` = `点`：任意字符
  * `+` = `加号`：1或任意个数，即 `>=1` 个

或者再加上个问号：

* `?`：表示能匹配上的字符，越少越好
  * 比如万一遇到特殊情况：
    * `<title>xxx<title>yyy</title>`
        * 加了问号，就只匹配 `<title>yyy</title>`，得到title值是`yyy`
        * 不加问号，则就是 贪婪匹配，则匹配到`<title>xxx<title>yyy</title>`，得到title值是`xxx<title>yyy`

代码：

```py
# Function: Python re greedy demo
# Author: Crifan Li
# Update: 20210719

import re

inputStr = "<title>xxx</title>yyy</title>"

normalGreedyMatchPattern = "<title>(?P<matchTitle>.+)</title>"
foundGreedyTitle = re.search(normalGreedyMatchPattern, inputStr)
if foundGreedyTitle:
    greedyMatchTitle = foundGreedyTitle.group("matchTitle")
    print("greedyMatchTitle=%s" % greedyMatchTitle)
    # greedyMatchTitle=xxx</title>yyy

nonGreedyMatchPattern = "<title>(?P<matchTitle>.+?)</title>"
foundNonGreedyTitle = re.search(nonGreedyMatchPattern, inputStr)
if foundNonGreedyTitle:
    nonGreedyMatchTitle = foundNonGreedyTitle.group("matchTitle")
    print("nonGreedyMatchTitle=%s" % nonGreedyMatchTitle)
    # nonGreedyMatchTitle=xxx
```

简述：

* `"<title>xxx</title>yyy</title>"`
    * 默认=贪婪匹配=尽量多匹配：`<title>(?P<matchTitle>.+)</title>`
        * `greedyMatchTitle=xxx</title>yyy`
    * 非贪婪匹配 = 尽量少匹配：`<title>(?P<matchTitle>.+?)</title>`
        * `nonGreedyMatchTitle=xxx`

完整代码：

```py
foundTitle = re.search("<title>(?P<title>.+?)</title>", respHtml, re.I)
```

就可以提取出：title值：

```bash
三维推关于短网址_二维码_多场景应用过期使用提醒
```

## 遇到title为空的情况

```html
<!DOCTYPE html><html lang="en"><head>xxx<title></title>xxx</html>
```

也能匹配到，则就要把：

`.+?`

改为：

`.*`

代码：

```py
foundTitle = re.search("<title>(?P<title>.*?)</title>", respHtml, re.I)
```

才能匹配到此处的：

`title=空的字符串=''`

## 遇到输入的字符串（此处的html）中包含回车换行符的

```html
<!DOCTYPE html>\r\n<html lang="zh-CN">\r\n<head>\r\n  <meta charset="UTF-8">\r\n  <meta name=。。。>\r\n  。。。         doc.addEventListener(\'DOMContentLoaded\', recalc, false);\r\n      })(document, window);\r\n  </script>\r\n  <title></title>。。。
```

则就要，新增参数

`re.M`

代码：

```py
foundTitle = re.search("<title>(?P<title>.*?)</title>", respHtml, re.I|re.M)
```

解释：

* `re.M` = `re.MULTILINE`=`多行模式`：允许输入的字符串本身是多行的 == 字符串本身内部带回车换行符（\r或\n）的
  * 此处输入的html中，包含多个`\r`和`\n`
    * 用了`re.M`模式，才能匹配到

## 遇到title值中间包含换行符

```html
'\r\n\r\n<!DOCTYPE html>\r\n\r\n<html>\r\n<head>。。。</script>\r\n    <title>\r\n\t网址信息\r\n</title></head>\r\n<body>
```

加参数：

* `re.S` = `re.DOTALL` = dot match all char=点`.`匹配所有字符
  * 作用：用`.`去匹配任意字符时，也能匹配到换行符
    * 对比：默认的话，`.`去匹配任意字符，是**不包含**换行符的
  * 对应着此处的
    * `<title>\r\n\t网址信息\r\n</title>`
      * 中的： `\r\n\t网址信息\r\n`
        * 其中的 **点**`.` 也能匹配到`\r`和`\n`

代码：

```py
foundTitle = re.search("<title>(?P<title>.*?)</title>", respHtml, re.I|re.M|re.S)
```

## 后记

此处，顺带说一下，可见，如果用re正则，去匹配html，则显得很复杂，很不好写出完美的正则去匹配所有特殊情况

所以，单独对于解析html字符串来说，推荐用专门的独立的库：

* html中，变数很多，为了完美兼容，常见的各种情况，甚至包括html标签语法有问题的情况，建议用：
  * 专门的html的解析的库，比如BeautifulSoup，第四版=version 4简称bs4
    * `BeautifulSoup`
        ```bash
        pip install bs4
        ```
