# re.finditer心得

## iter对象无法被重复访问

Python中的iterator类型变量，只能被访问（使用/遍历）一次，就空了。无法被重复使用。

用代码举例如下：

```python
matchIter = re.finditer(someP, someStr)
for eachMatch in matchIter:
  print("matchIter=%s" % matchIter)

resultList = list(matchIter) # -> will error, matchIter already None
```
