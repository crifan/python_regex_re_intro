# 非捕获组举例

# 举例1

```py
# Function: Demo python re non-capture effect
# Author: Crifan Li
# Update: 20210707

import re

inputStr = "Please 42.121.252.58:443 contact 127.0.0.1 ..."

capturePattern = "\d+\.\d+\.\d+\.\d+(:\d+)?"
ipList_capture = re.findall(capturePattern, inputStr)
print("ipList_capture=%s" % ipList_capture)
# ipList_capture=[':443', '']

nonCapturePattern = "\d+\.\d+\.\d+\.\d+(?::\d+)?"
ipList_nonCapture = re.findall(nonCapturePattern, inputStr)
print("ipList_nonCapture=%s" % ipList_nonCapture)
# ipList_nonCapture=['42.121.252.58:443', '127.0.0.1']
```

解释：

* 普通的组=捕获的组=capture group：返回，带括号的组(xxx)的部分
  * -》 此处`re.findall`，返回 被捕获的组的部分： `[':443', '']`
* 非捕获的组=non-capture group：带括号的组(xxx)的部分，没有被捕获，所以不返回
  * -》 此处`re.findall`，返回  不被捕获组，没有组被捕获，所以是整个匹配到的字符串：`['42.121.252.58:443', '127.0.0.1']`

## 举例2

```py
inputStr = """
logging.info("some info")
logging.debug("some debug")
"""
```

用普通的组，即捕获的组：

```py
capturedStrList = re.findall("logging\.((debug)|(info)).+?$", inputStr, re.M)
```

输出的是：

```bash
[('info', '', 'info'), ('debug', 'debug', '')]
```

而此处想要匹配整个字符串，则可以改为：非捕获组：

```py
nonCaptureStrList = re.findall("logging\.(?:(?:debug)|(?:info)).+?$", inputStr, re.M)
```

输出：

```bash
['logging.info("some info")', 'logging.debug("some debug")']
```

完整代码：

```py
# Function: demo python re non-capture
# Author: Crifan Li
# Update: 20210107

import re

inputStr = """
logging.info("some info")
logging.debug("some debug")
"""

capturedStrList = re.findall("logging\.((debug)|(info)).+?$", inputStr, re.M)
print("capturedStrList=%s" % capturedStrList)
# capturedStrList=[('info', '', 'info'), ('debug', 'debug', '')]

nonCaptureStrList = re.findall("logging\.(?:(?:debug)|(?:info)).+?$", inputStr, re.M)
print("nonCaptureStrList=%s" % nonCaptureStrList)
# nonCaptureStrList=['logging.info("some info")', 'logging.debug("some debug")']
```

## 举例3

```py
def isPythonLanguage(codeStr):
。。。
    # sys.path.append("lib")
    # sys.path.append("libs/evernote-sdk-python3/lib")
    # logging.debug(
    # logging.warning(
    # logging.error(
    # logging.exception(
    commonFuncNum = 0
    CommonFunctionPList = [
        "logging\.(?:(?:debug)|(?:info)|(?:warning)|(?:warn)|(?:error)|(?:critical)|(?:exception)|(?:log))",
        "sys\.path\.(?:(?:clear)|(?:copy)|(?:append)|(?:extend)|(?:pop)|(?:index)|(?:count)|(?:insert)|(?:remove)|(?:reverse)|(?:sort))",
        "os\.path\.(?:(?:abspath)|(?:basename)|(?:commonpath)|(?:commonprefix)|(?:dirname)|(?:exists)|(?:lexists)|(?:expanduser)|(?:expandvars)|(?:getatime)|(?:getmtime)|(?:getctime)|(?:getsize)|(?:isabs)|(?:isfile)|(?:isdir)|(?:islink)|(?:ismount)|(?:join)|(?:normcase)|(?:normpath)|(?:realpath)|(?:relpath)|(?:samefile)|(?:sameopenfile)|(?:samestat)|(?:split)|(?:splitdrive)|(?:splitext)|(?:supports_unicode_filenames))",
    ]
    for curCommonFuncP in CommonFunctionPList:
        allCommonFunc = re.findall(curCommonFuncP, codeStr, re.I)
        curCommonFuncNum = len(allCommonFunc)
        commonFuncNum += curCommonFuncNum
    curValidNum += commonFuncNum
。。。
    return isPyLang
```
