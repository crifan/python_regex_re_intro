# re学习心得

学习了`Python`的正则`re`后，会对其他一些知识理解更加深入，更能触类旁通：

## `Python`的`str`的`startswith`

举例：

```python
imgUrl = "Books/55434/Books_55434_205865_Book_20190407102211.jpg"
isImgUrlValid = imgUrl.startswith("http")
# isImgUrlValid=False

imgUrl = "http://img.xiaohuasheng.cn/Douban/Book/s11215709.jpg"
isImgUrlValid = imgUrl.startswith("http")
# isImgUrlValid=True
```

其中的`startswith`：

```python
isImgUrlValid = originCoverImgUrl.startswith("http")
```

等价于，可以换为：

```python
isMatchHttp = re.match("^http", originCoverImgUrl)
isOriginCoverImgUrlValid = isMatchHttp
```

而之前用startswith还有个缺点：

万一想要同时判断一个url是否是http或https开头的，却要写两个startswith的判断

再去逻辑或才能得到要的结果：

```python
imgUrl = "http://img.xiaohuasheng.cn/Douban/Book/s11215709.jpg"
# imgUrl = "https://img.xiaohuasheng.cn/Douban/Book/s11215709.jpg"isHttpUrl = imgUrl.startswith("http")
isHttpsUrl = imgUrl.startswith("https") 
isValidUrl = isHttpUrl or isHttpsUrl
```

而改为正则去匹配：

```python
imgUrl = "http://img.xiaohuasheng.cn/Douban/Book/s11215709.jpg"
# imgUrl = "https://img.xiaohuasheng.cn/Douban/Book/s11215709.jpg"isHttpOrHttpsUrl = re.match("^https?", imgUrl)
isValidUrl = isHttpOrHttpsUrl
```

就显得更加简洁和高效。

如此举一反三，触类旁通，可以把正则在字符串的搜索和替换等领域发挥出更大的价值。
