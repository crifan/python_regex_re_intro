# 非捕获组

官网的

* [英文解释](https://docs.python.org/3/library/re.html#regular-expression-syntax)

```bash
(?...)
    This is an extension notation (a '?' following a '(' is not meaningful otherwise).
    The first character after the '?' determines what the meaning and further syntax of the construct is.
    Extensions usually do not create a new group; (?P<name>...) is the only exception to this rule.
    Following are the currently supported extensions.

(?:...)
    A non-capturing version of regular parentheses.
    Matches whatever regular expression is inside the parentheses,
    but the substring matched by the group cannot be retrieved after performing a match or referenced later in the pattern.

(?P<name>...)
    Similar to regular parentheses, but the substring matched by the group is accessible via the symbolic group name name.
    Group names must be valid Python identifiers, and each group name must be defined only once within a regular expression.
    A symbolic group is also a numbered group, just as if the group were not named.
```

* [中文解释](https://docs.python.org/zh-cn/3/library/re.html#regular-expression-syntax)

```bash
(?…)
这是个扩展标记法 （一个 '?' 跟随 '(' 并无含义）。
'?' 后面的第一个字符决定了这个构建采用什么样的语法。
这种扩展通常并不创建新的组合； (?P<name>...) 是唯一的例外。 以下是目前支持的扩展。

(?:…)
正则括号的非捕获版本。 匹配在括号内的任何正则表达式，
但该分组所匹配的子字符串 不能 在执行匹配后被获取或是之后在模式中被引用。

(?P<name>…)
（命名组合）类似正则组合，但是匹配到的子串组在外部是通过定义的 name 来获取的。
组合名必须是有效的Python标识符，并且每个组合名只能用一个正则表达式定义，只能定义一次。
一个符号组合同样是一个数字组合，就像这个组合没有被命名一样。

命名组合可以在三种上下文中引用。
如果样式是 (?P<quote>['"]).*?(?P=quote) 
（也就是说，匹配单引号或者双引号括起来的字符串)：

引用组合 "quote" 的上下文         引用方法
在正则式自身内                    (?P=quote) (如示)
                                \1
处理匹配对象 m                    m.group('quote')
                                m.end('quote') (等)
传递到 re.sub() 里的 repl 参数中   \g<quote>
                                \g<1>
                                \1
```

代码演示如何使用：

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
# Author: Crifan Li
# Update: 20191223
# Function: Demo python re (?:…) non-capture usage

import re

def demoReNonCapturingGroup():
    normalGroupPattern = """(请?点击[“”"'])(.+?)([“”"'])"""
    nonCapturingGroupPattern = """(?:请?点击[“”"'])(?:.+?)(?:[“”"'])"""
    namedGroupPattern = """(请?点击[“”"'])(?P<strToClick>.+?)([“”"'])"""

    inputStrList = [
        "请点击“升级”按钮取210000经验,需50元宝提取经验",
        "点击”+“，放入吞噬道具",
        "请点击”战骑“",
    ]
    for eachInputStr in inputStrList:
        print("="*60)
        foundNormalGroup = re.search(normalGroupPattern, eachInputStr)
        foundNonCapturingGroup = re.search(nonCapturingGroupPattern, eachInputStr)
        foundNamedGroup = re.search(namedGroupPattern, eachInputStr)

        if foundNormalGroup and foundNonCapturingGroup and foundNamedGroup:
            print("-"*60)
            print("eachInputStr=%s -> " % eachInputStr)

            matchedWholeStrNormal = foundNormalGroup.group(0)
            print("matchedWholeStrNormal=%s" % matchedWholeStrNormal)
            matchedWholeStrNonCapturing = foundNonCapturingGroup.group(0)
            print("matchedWholeStrNonCapturing=%s" % matchedWholeStrNonCapturing)
            matchedWholeStrNamed = foundNamedGroup.group(0)
            print("matchedWholeStrNamed=%s" % matchedWholeStrNamed)

            matchedGroupListNormal = foundNormalGroup.groups()
            print("matchedGroupListNormal=%s" % (matchedGroupListNormal, ))
            matchedGroupListNonCapturing = foundNonCapturingGroup.groups()
            print("matchedGroupListNonCapturing=%s" % (matchedGroupListNonCapturing, ))
            matchedGroupListNamed = foundNamedGroup.groups()
            print("matchedGroupListNamed=%s" % (matchedGroupListNamed, ))

            strToClickNormal = foundNormalGroup.group(2)
            print("strToClickNormal=%s" % strToClickNormal)
            strToClickNamed = foundNamedGroup.group("strToClick")
            print("strToClickNamed=%s" % strToClickNamed)

            pass

    pass

    # ============================================================
    # ------------------------------------------------------------
    # eachInputStr=请点击“升级”按钮取210000经验,需50元宝提取经验 ->
    # matchedWholeStrNormal=请点击“升级”
    # matchedWholeStrNonCapturing=请点击“升级”
    # matchedWholeStrNamed=请点击“升级”
    # matchedGroupListNormal=('请点击“', '升级', '”')
    # matchedGroupListNonCapturing=()
    # matchedGroupListNamed=('请点击“', '升级', '”')
    # strToClickNormal=升级
    # strToClickNamed=升级
    # ============================================================
    # ------------------------------------------------------------
    # eachInputStr=点击”+“，放入吞噬道具 ->
    # matchedWholeStrNormal=点击”+“
    # matchedWholeStrNonCapturing=点击”+“
    # matchedWholeStrNamed=点击”+“
    # matchedGroupListNormal=('点击”', '+', '“')
    # matchedGroupListNonCapturing=()
    # matchedGroupListNamed=('点击”', '+', '“')
    # strToClickNormal=+
    # strToClickNamed=+
    # ============================================================
    # ------------------------------------------------------------
    # eachInputStr=请点击”战骑“ ->
    # matchedWholeStrNormal=请点击”战骑“
    # matchedWholeStrNonCapturing=请点击”战骑“
    # matchedWholeStrNamed=请点击”战骑“
    # matchedGroupListNormal=('请点击”', '战骑', '“')
    # matchedGroupListNonCapturing=()
    # matchedGroupListNamed=('请点击”', '战骑', '“')
    # strToClickNormal=战骑
    # strToClickNamed=战骑

    # 结论：
    # non-capturing group = 非捕获组
    # 含义：正常去匹配，但是匹配后的match的group中，是无法获取到对应的值的
    # 用途：（感觉唯一的用途就只是）在匹配时，用group去匹配，容易看懂相关内容的逻辑和关系，但是匹配的结果中，不关心这部分的内容

if __name__ == "__main__":
    demoReNonCapturingGroup()
```
