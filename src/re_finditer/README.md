# re.finditer

`re.finditer` = **iter**ator of `re.findall`=针对`re.findall`所返回的字符串相对，每个都是一个匹配的对象`MatchedObject`

对比：

* `findall`：返回`str`的list
* `finditer`：返回`MatchObject`的迭代器`iterator`
  * 可以针对每个匹配到的字符串，获取其中的`sub group`了

TODO：

 [【已解决】Python中用正则re去搜索分组的集合](http://www.crifan.com/python_use_re_regex_to_search_group_collection)

待整理过来

另外：好像此处属于 python中 iterator的特点 或 坑：访问一次就空了（而不一定是re的问题），待确认
