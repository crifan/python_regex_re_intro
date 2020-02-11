# re简介

## 关于正则表达式

关于正则表达式，之前已整理了教程：

* 新
  * [应用广泛的超强搜索：正则表达式](https://book.crifan.com/books/super_search_regex/website/)
* 旧
  * [正则表达式学习心得](https://www.crifan.com/files/doc/docbook/regular_expression/release/html/regular_expression.htm)

## 关于`Python`中的`re`

关于Python的正则表达式方面的教程，之前也有整理过：

* 旧
  * [Python专题教程：正则表达式re模块详解](https://www.crifan.com/files/doc/docbook/python_topic_re/release/html/python_topic_re.html)
  * [【教程】详解Python正则表达式 – 在路上](https://www.crifan.com/detailed_explanation_about_python_regular_express/)
    * 之前没完全写完

此处再次重新整理。

`re`是`Python`中内置的正则表达式模块。功能十分强大。

先概述如下：

* 最常用：
  * 搜索：`re.search`
  * 替换：`re.sub`
  * 匹配：`re.match`
* 其他
  * 匹配所有：`re.findall`
  * 匹配所有，且每个都可获取匹配对象的详情：`re.finditer`
    * = `re.findall` + `re.search`

下面来详细介绍其相关功能。

## 官网资料

此处先贴出来，`Python`**官网**关于`re`的的文档资料，供后续参考：

* 官网文档
  * 英文
    * [re — Regular expression operations - Python 3](https://docs.python.org/3/library/re.html#regular-expression-syntax)
  * 中文
    * [re --- 正则表达式操作 — Python 3 文档](https://docs.python.org/zh-cn/3/library/re.html#regular-expression-syntax)
* 官网教程
  * 英文
    * [Regular Expression HOWTO — Python 3 documentation](https://docs.python.org/3/howto/regex.html)
  * 中文
    * [正则表达式HOWTO — Python 3 文档](https://docs.python.org/zh-cn/3/howto/regex.html)
