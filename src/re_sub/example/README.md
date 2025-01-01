# re.sub举例

先列举一些其他小的例子：

```py
orignalStr = "http://udpdcs.4399sy.com/init_info.php?time=1607061237&flag=364804364fefa8226cf4be09a944694a|None"
curAppName = "巨刃"
replaceP = "\g<url>|巨刃" % curAppName # '\\g<url>|巨刃'
replacedStr = re.sub("(?P<url>https?[^\|]+)\|(?P<type>\w+)", replaceP, eachLine)
# http://udpdcs.4399sy.com/init_info.php?time=1607061237&flag=364804364fefa8226cf4be09a944694a|巨刃
```

