# 普通分组vs命名分组vs非捕获分组

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
