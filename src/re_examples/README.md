# re应用举例

## 提取csdn帖子地址

```python
foundLastListPageUrl = re.search('<a\s+?href="(?P<lastListPageUrl>/\w+?/article/list/\d+)">尾页</a>', homeRespHtml, re.I);
logging.debug("foundLastListPageUrl=%s", foundLastListPageUrl);

if(foundLastListPageUrl):
    lastListPageUrl = foundLastListPageUrl.group("lastListPageUrl");
```

详见：

https://github.com/crifan/BlogsToWordpress/blob/master/libs/crifan/blogModules/BlogCsdn.py

从内容中

```html
<a href="/chenglinhust/article/list/22">尾页</a>
```

提取出

```bash
/chenglinhust/article/list/22
```

## 提取csdn帖子的标题

```python
foundTitle = re.search('<span class="link_title"><a href="[\w/]+?">\s*(<font color="red">\[置顶\]</font>)?\s*(?P<titleHtml>.+?)\s*</a>\s*</span>', html, re.S);
logging.debug("foundTitle=%s", foundTitle);

if(foundTitle):
    titleHtml = foundTitle.group("titleHtml");
    logging.debug("titleHtml=%s", titleHtml);
```

详见：

https://github.com/crifan/BlogsToWordpress/blob/master/libs/crifan/blogModules/BlogCsdn.py

从内容中

```html
<span class="link_title"><a href="/v_july_v/article/details/6543438">
<font color="red">[置顶]</font>
程序员面试、算法研究、编程艺术、红黑树4大系列集锦与总结
</a></span>
```

或

```html
<span class="link_title"><a href="/chdhust/article/details/7252155">
         windows编程中wParam和lParam消息        
        
         </a>
         </span>
```

提取出

```bash
程序员面试、算法研究、编程艺术、红黑树4大系列集锦与总结
```

或

```bash
windows编程中wParam和lParam消息
```
