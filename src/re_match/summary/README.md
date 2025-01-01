# re.match心得

## error multiple repeat at position

### 现象

代码

```py
hrefP = "(https?://)?%s/?" % aStr
isSameUrl = re.match(hrefP, hrefValue, re.I)
```

要去匹配的值aStr

```
'Is there a way to get a call graph for certain c++ function in Visual Studio? - Stack Overflow'
```

报错：

```bash
发生异常: error
multiple repeat at position 61
```

### 原因

字符串中包含特殊的正则字符`+`，且是连续的`++`

导致逻辑上不成立：`++`在规则中是不合法的

### 解决办法

确保正则的pattern中，没有无效的规则。

此处即，把特殊字符，都替换，加上反斜杠\去转义：

### 具体步骤

改为：

```py
SpecialCharList = [
    ".",
    "+",
    "*",
    "?",
]
for eachSpecialChar in SpecialCharList:
    escapedChar = "\%s" % eachSpecialChar # '\\.'
    aStr = aStr.replace(eachSpecialChar, escapedChar)
# 'Is there a way to get a call graph for certain c++ function in Visual Studio? - Stack Overflow'
# ->
# 'Is there a way to get a call graph for certain c\\+\\+ function in Visual Studio\\? - Stack Overflow'

hrefP = "(https?://)?%s/?" % aStr
isSameUrl = re.match(hrefP, hrefValue, re.I)
```
