# re.findall vs re.finditer 以及 非捕获组

```py
# https://zhidao.baidu.com/question/1738729970599497667.html

import re

emailStr = "abc123@163.com xxx 456def@qq.com yyy 789ghi@gmail.com"

# allEmailList = re.findall("[a-zA-Z0-9]@(163|qq|gmail)\.com", emailStr) # ['163', 'qq', 'gmail']
# allEmailList = re.findall("([a-zA-Z0-9]+@(163|qq|gmail)\.com)", emailStr) # [('abc123@163.com', '163'), ('456def@qq.com', 'qq'), ('789ghi@gmail.com', 'gmail')]
# allEmailList = re.finditer("([a-zA-Z0-9]+@(163|qq|gmail)\.com)", emailStr) # <callable_iterator object at 0x10f94abe0>
allEmailList = re.findall("([a-zA-Z0-9]+@(?:163|qq|gmail)\.com)", emailStr) # ['abc123@163.com', '456def@qq.com', '789ghi@gmail.com']
print(allEmailList)
```
