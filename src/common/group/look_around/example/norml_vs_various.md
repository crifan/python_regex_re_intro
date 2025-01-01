# 普通组vs各种环视断言

## `normal group` vs `positive lookahead` vs `negative lookahead` vs `positive lookbehind` vs `negative lookbehind`

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
# Author: Crifan Li
# Update: 20191224
# Function: Demo python re lookahead and lookbehind group

import re

def demoReLookAheadBehind():
    inputStrList = [
        "date=20191224&name=CrifanLi&language=python",
        "language=python&name=CrifanLi&date=20191224", # lookahead will NOT match
        "language=python&name=CrifanLi date=20191224", # negative lookahead CAN match, the whole 'name=CrifanLi'
        "language=go&name=CrifanLi date=20191224", # positive lookbehind CAN match
        "language=go name=CrifanLi date=20191224", # negative lookbehind CAN match
    ]

    groupNormalPattern = "name=(\w+)" # 匹配任何 name=XXX 其中XXX是字母数字下划线均可
    groupLookaheadPattern = "name=(\w+)(?=&language)" # 只匹配后面 是&language 的情况
    groupNegativelookaheadPattern = "name=(\w+)(?!&)" # 只匹配后面 不是& 的情况
    groupPositivelookbehindPattern = "(?<=go&)name=(\w+)" # 只匹配前面 是go& 的情况
    groupNegativelookbehindPattern = "(?<!&)name=(\w+)" # 只匹配前面 不是& 的情况

    for curIdx, eachInputStr in enumerate(inputStrList):
        print("\n%s [%d] %s %s" % ("="*20, curIdx, eachInputStr, "="*20))

        print("%s %s %s" % ("-"*10, "normal group", "-"*10))
        foundGroupNormal = re.search(groupNormalPattern, eachInputStr)
        print("foundGroupNormal=%s" % foundGroupNormal)
        if foundGroupNormal:
            wholeMatchStrNormal = foundGroupNormal.group(0)
            print("wholeMatchStrNormal=%s" % wholeMatchStrNormal)
            matchedGroupsNormal = foundGroupNormal.groups()
            print("matchedGroupsNormal=%s" % (matchedGroupsNormal, ))
            foundName = foundGroupNormal.group(1)
            print("foundName=%s" % foundName)

        print("%s %s %s" % ("-"*10, "lookahead group", "-"*10))
        foundGroupLookahead = re.search(groupLookaheadPattern, eachInputStr)
        print("foundGroupLookahead=%s" % foundGroupLookahead)
        if foundGroupLookahead:
            wholeMatchStrLookahead = foundGroupLookahead.group(0)
            print("wholeMatchStrLookahead=%s" % wholeMatchStrLookahead)
            matchedGroupsLookahead = foundGroupLookahead.groups()
            print("matchedGroupsLookahead=%s" % (matchedGroupsLookahead, ))
            foundName = foundGroupLookahead.group(1)
            print("foundName=%s" % foundName)

        print("%s %s %s" % ("-"*10, "negative lookahead group", "-"*10))
        foundGroupNegativelookahead = re.search(groupNegativelookaheadPattern, eachInputStr)
        print("foundGroupNegativelookahead=%s" % foundGroupNegativelookahead)
        if foundGroupNegativelookahead:
            wholeMatchStrNegativelookahead = foundGroupNegativelookahead.group(0)
            print("wholeMatchStrNegativelookahead=%s" % wholeMatchStrNegativelookahead)
            matchedGroupsNegativelookahead = foundGroupNegativelookahead.groups()
            print("matchedGroupsNegativelookahead=%s" % (matchedGroupsNegativelookahead, ))
            foundName = foundGroupNegativelookahead.group(1)
            print("foundName=%s" % foundName)

        print("%s %s %s" % ("-"*10, "positive lookahead group", "-"*10))
        foundGroupPositivelookbehind = re.search(groupPositivelookbehindPattern, eachInputStr)
        print("foundGroupPositivelookbehind=%s" % foundGroupPositivelookbehind)
        if foundGroupPositivelookbehind:
            wholeMatchStrPositivelookbehind = foundGroupPositivelookbehind.group(0)
            print("wholeMatchStrPositivelookbehind=%s" % wholeMatchStrPositivelookbehind)
            matchedGroupsPositivelookbehind = foundGroupPositivelookbehind.groups()
            print("matchedGroupsPositivelookbehind=%s" % (matchedGroupsPositivelookbehind, ))
            foundName = foundGroupPositivelookbehind.group(1)
            print("foundName=%s" % foundName)

        print("%s %s %s" % ("-"*10, "positive lookahead group", "-"*10))
        foundGroupNegativelookbehind = re.search(groupNegativelookbehindPattern, eachInputStr)
        print("foundGroupNegativelookbehind=%s" % foundGroupNegativelookbehind)
        if foundGroupNegativelookbehind:
            wholeMatchStrNegativelookbehind = foundGroupNegativelookbehind.group(0)
            print("wholeMatchStrNegativelookbehind=%s" % wholeMatchStrNegativelookbehind)
            matchedGroupsNegativelookbehind = foundGroupNegativelookbehind.groups()
            print("matchedGroupsNegativelookbehind=%s" % (matchedGroupsNegativelookbehind, ))
            foundName = foundGroupNegativelookbehind.group(1)
            print("foundName=%s" % foundName)

    # ==================== [0] date=20191224&name=CrifanLi&language=python ====================
    # ---------- normal group ----------
    # foundGroupNormal=<re.Match object; span=(14, 27), match='name=CrifanLi'>
    # wholeMatchStrNormal=name=CrifanLi
    # matchedGroupsNormal=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- lookahead group ----------
    # foundGroupLookahead=<re.Match object; span=(14, 27), match='name=CrifanLi'>
    # wholeMatchStrLookahead=name=CrifanLi
    # matchedGroupsLookahead=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- negative lookahead group ----------
    # foundGroupNegativelookahead=<re.Match object; span=(14, 26), match='name=CrifanL'>
    # wholeMatchStrNegativelookahead=name=CrifanL
    # matchedGroupsNegativelookahead=('CrifanL',)
    # foundName=CrifanL
    # ---------- positive lookahead group ----------
    # foundGroupPositivelookbehind=None
    # ---------- positive lookahead group ----------
    # foundGroupNegativelookbehind=None

    # ==================== [1] language=python&name=CrifanLi&date=20191224 ====================
    # ---------- normal group ----------
    # foundGroupNormal=<re.Match object; span=(16, 29), match='name=CrifanLi'>
    # wholeMatchStrNormal=name=CrifanLi
    # matchedGroupsNormal=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- lookahead group ----------
    # foundGroupLookahead=None
    # ---------- negative lookahead group ----------
    # foundGroupNegativelookahead=<re.Match object; span=(16, 28), match='name=CrifanL'>
    # wholeMatchStrNegativelookahead=name=CrifanL
    # matchedGroupsNegativelookahead=('CrifanL',)
    # foundName=CrifanL
    # ---------- positive lookahead group ----------
    # foundGroupPositivelookbehind=None
    # ---------- positive lookahead group ----------
    # foundGroupNegativelookbehind=None

    # ==================== [2] language=python&name=CrifanLi date=20191224 ====================
    # ---------- normal group ----------
    # foundGroupNormal=<re.Match object; span=(16, 29), match='name=CrifanLi'>
    # wholeMatchStrNormal=name=CrifanLi
    # matchedGroupsNormal=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- lookahead group ----------
    # foundGroupLookahead=None
    # ---------- negative lookahead group ----------
    # foundGroupNegativelookahead=<re.Match object; span=(16, 29), match='name=CrifanLi'>
    # wholeMatchStrNegativelookahead=name=CrifanLi
    # matchedGroupsNegativelookahead=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- positive lookahead group ----------
    # foundGroupPositivelookbehind=None
    # ---------- positive lookahead group ----------
    # foundGroupNegativelookbehind=None

    # ==================== [3] language=go&name=CrifanLi date=20191224 ====================
    # ---------- normal group ----------
    # foundGroupNormal=<re.Match object; span=(12, 25), match='name=CrifanLi'>
    # wholeMatchStrNormal=name=CrifanLi
    # matchedGroupsNormal=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- lookahead group ----------
    # foundGroupLookahead=None
    # ---------- negative lookahead group ----------
    # foundGroupNegativelookahead=<re.Match object; span=(12, 25), match='name=CrifanLi'>
    # wholeMatchStrNegativelookahead=name=CrifanLi
    # matchedGroupsNegativelookahead=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- positive lookahead group ----------
    # foundGroupPositivelookbehind=<re.Match object; span=(12, 25), match='name=CrifanLi'>
    # wholeMatchStrPositivelookbehind=name=CrifanLi
    # matchedGroupsPositivelookbehind=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- positive lookahead group ----------
    # foundGroupNegativelookbehind=None

    # ==================== [4] language=go name=CrifanLi date=20191224 ====================
    # ---------- normal group ----------
    # foundGroupNormal=<re.Match object; span=(12, 25), match='name=CrifanLi'>
    # wholeMatchStrNormal=name=CrifanLi
    # matchedGroupsNormal=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- lookahead group ----------
    # foundGroupLookahead=None
    # ---------- negative lookahead group ----------
    # foundGroupNegativelookahead=<re.Match object; span=(12, 25), match='name=CrifanLi'>
    # wholeMatchStrNegativelookahead=name=CrifanLi
    # matchedGroupsNegativelookahead=('CrifanLi',)
    # foundName=CrifanLi
    # ---------- positive lookahead group ----------
    # foundGroupPositivelookbehind=None
    # ---------- positive lookahead group ----------
    # foundGroupNegativelookbehind=<re.Match object; span=(12, 25), match='name=CrifanLi'>
    # wholeMatchStrNegativelookbehind=name=CrifanLi
    # matchedGroupsNegativelookbehind=('CrifanLi',)
    # foundName=CrifanLi

if __name__ == "__main__":
    demoReLookAheadBehind()
```

对于代码中的结果，总结起来就是：

* name=(\w+)：普通的group
  * 匹配结果
    * 5个都匹配
      * date=20191224&name=CrifanLi&language=python
      * language=python&name=CrifanLi&date=20191224
      * language=python&name=CrifanLi date=20191224
      * language=go&name=CrifanLi date=20191224
      * language=go name=CrifanLi date=20191224
    * 匹配到内容都是：
      * name=CrifanLi
  * 解析：因为只是普通的(xxx)的组，没有限制，所以都能匹配到
* name=(\w+)(?=&language)：lookahead=positive lookahead=正向先行断言
  * 匹配结果
    * 只匹配了1个：
      * date=20191224&name=CrifanLi&language=python
    * 其余4个都不匹配
      * language=python&name=CrifanLi&date=20191224
      * language=python&name=CrifanLi date=20191224
      * language=go&name=CrifanLi date=20191224
      * language=go name=CrifanLi date=20191224
  * 解析：
    * (?=&language) 表示 后面一定是 &language
      * 而上面4个的后面，分别是：
        * &date=
        * date=
        * date=
        * date=
      * 所以都不匹配
* name=(\w+)(?!&)：negative look ahead=负向先行断言
  * 匹配结果
    * 5个都匹配到了，但是匹配的内容不一样
      * 2个匹配到了：name=CrifanL
        * date=20191224&name=CrifanLi&language=python
        * language=python&name=CrifanLi&date=20191224
      * 3个匹配到了：name=CrifanLi
        * language=python&name=CrifanLi date=20191224
        * language=go&name=CrifanLi date=20191224
        * language=go name=CrifanLi date=20191224
  * 解析
    * 注意 前2个匹配到的 最后没有i，是CrifanL，而不是CrifanLi
    * 因为(?!&)表示 后面不能是 &
      * 所以类似于
        * name=CrifanLi&language
        * name=CrifanLi&date
      * 这种，只能匹配到L，而不是i，因为i后面是&，此处要求后面不能是&
* (?<=go&)name=(\w+)：positive look behind=正向后行断言
  * 匹配结果
    * 只匹配到1个
      * language=go&name=CrifanLi date=20191224
  * 解析
    * 因为此处(?<=go&)意思是，前面一定要是 go& 所以只有这个匹配
    * 其他的
      * 20191224&name=
      * python&name=
      * python&name=
      * go name=
    * 中name=的前面 都不符合条件
* (?<!&)name=(\w+)：negative look behind=负向后行断言
  * 匹配结果
    * 只匹配到1个：
      * language=go name=CrifanLi date=20191224
  * 解析
    * 因为(?<!&)的意思是：前面不能是 &
      * 所以只有
        * go name=
      * 这个符合，而其余的
        * 20191224&name=
        * python&name=
        * python&name=
        * go&name=
      * name=前面都是&，所以不符合条件，不匹配
