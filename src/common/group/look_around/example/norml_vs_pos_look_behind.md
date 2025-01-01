# 普通组vs正向向后看

* `named group` vs `positive lookbehind`

官网解释：

```bash
(?<=...)
    Matches if the current position in the string is preceded by a match for ... that ends at the current position.
    This is called a positive lookbehind assertion.
    (?<=abc)def will find a match in 'abcdef', since the lookbehind will back up 3 characters and check if the contained pattern matches.
    The contained pattern must only match strings of some fixed length, meaning that abc or a|b are allowed, but a* and a{3,4} are not.
    Note that patterns which start with positive lookbehind assertions will not match at the beginning of the string being searched;

(?P<name>...)
    Similar to regular parentheses, but the substring matched by the group is accessible via the symbolic group name name.
    Group names must be valid Python identifiers, and each group name must be defined only once within a regular expression.
    A symbolic group is also a numbered group, just as if the group were not named.
```

用代码详细解释：

```python
#!/usr/bin/python
# -*- coding: utf-8 -*-
# Author: Crifan Li
# Update: 20191224
# Function: Demo python re lookbehind group

import re

def demoReLookbehind():
    namedGroupPattern = "(SID=)(?P<sidValue>[^&]+)"
    lookBehindGroupPattern = "(?<=SID=)(?P<sidValue>[^&]+)"
    """
    正则含义的解释：
        (?<=SID=)[^&]+
            (?<=SID=) 属于(?<=XXX)，其中XXX是"SID="这个固定长度的4个字符的字符串 用于匹配你要的值的前面的部分 SID=YYY中的 SID=
            [^&]+
                [] 中括号中是所允许出现的字符
                ^ 是取反，除了...之外的，所以^&就是除了&字符之外的，因为你要匹配的字符串是
                    SID=8E3qOreRiOnbhkl84Uc&YYY 可以避免匹配到 最后的&和YYY
                + 表示1个或更多个 直到遇到 不允许出现的&字符，匹配此处的 即从8到c，即8E3qOreRiOnbhkl84Uc
    """

    inputStrList = [
        "GeneralSearch&SID=8E3qOreRiOnbhkl84Uc&preferencesSaved",
    ]
    for eachInputStr in inputStrList:
        print("="*60)
        foundNamedGroup = re.search(namedGroupPattern, eachInputStr)
        foundLookbehindGroup = re.search(lookBehindGroupPattern, eachInputStr)
        if foundNamedGroup and foundLookbehindGroup:
            print("foundNamedGroup=%s" % foundNamedGroup)
            print("foundLookbehindGroup=%s" % foundLookbehindGroup)

            groupsNamedGroup = foundNamedGroup.groups()
            print("groupsNamedGroup=%s" % (groupsNamedGroup, ))
            groupsLookbehindGroup = foundLookbehindGroup.groups()
            print("groupsLookbehindGroup=%s" % (groupsLookbehindGroup, ))

            wholeStrNamedGroup = foundNamedGroup.group(0)
            print("wholeStrNamedGroup=%s" % wholeStrNamedGroup)
            wholeStrLookbehindGroup = foundLookbehindGroup.group(0)
            print("wholeStrLookbehindGroup=%s" % wholeStrLookbehindGroup)

            sidValueNamedGroup = foundNamedGroup.group("sidValue")
            print("sidValueNamedGroup=%s" % sidValueNamedGroup)
            sidValueLookbehindGroup = foundLookbehindGroup.group("sidValue")
            print("sidValueLookbehindGroup=%s" % sidValueLookbehindGroup)

    # foundNamedGroup=<re.Match object; span=(14, 37), match='SID=8E3qOreRiOnbhkl84Uc'>
    # foundLookbehindGroup=<re.Match object; span=(18, 37), match='8E3qOreRiOnbhkl84Uc'>
    # groupsNamedGroup=('SID=', '8E3qOreRiOnbhkl84Uc')
    # groupsLookbehindGroup=('8E3qOreRiOnbhkl84Uc',)
    # wholeStrNamedGroup=SID=8E3qOreRiOnbhkl84Uc
    # wholeStrLookbehindGroup=8E3qOreRiOnbhkl84Uc
    # sidValueNamedGroup=8E3qOreRiOnbhkl84Uc
    # sidValueLookbehindGroup=8E3qOreRiOnbhkl84Uc

if __name__ == "__main__":
    demoReLookbehind()
```
