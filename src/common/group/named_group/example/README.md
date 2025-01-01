# 命名的组举例

## getMitmdumpStatus

```py
def getMitmdumpStatus():
    """Get current mitmdump status"""
    isRunning, processInfoList = False, []
    if osIsMacOS():
        shellCmdStr = "ps aux | grep mitmdump"
    elif osIsWinows():
        shellCmdStr = "tasklist | findstr mitmdump"
    print("shellCmdStr=%s" % shellCmdStr)
    shellRespStr = subprocess.check_output(
        shellCmdStr,
        shell=True,
        universal_newlines=True,
    )
    print("shellRespStr=%s" % shellRespStr)
    singleLineList = shellRespStr.split(os.linesep)
    print("singleLineList=%s" % singleLineList)
    for eachLineStr in singleLineList:
        # print("eachLineStr=%s" % eachLineStr)
        # mitmdumpCmdPattern = "mitmdump\s+-p\s+\d+-s\s+\S+\.py"
        # mitmdumpCmdPattern   = "mitmdump\s+-p\s+\d+\s+-s\s+\S+\.py"
        # mitmdumpCmdPattern   = "mitmdump\s+-p\s+(?P<portStr>\d+)\s+-s\s+(?P<scriptFile>\S+?\.py)"
        # mitmdumpCmdPattern   = "\s+(?P<mitmdumpFile>\S+mitmdump)\s+-p\s+(?P<portStr>\d+)\s+-s\s+(?P<scriptFile>\S+?\.py)"
        # mitmdumpCmdPattern   = "^\w+\s+(?P<pidStr>\d+).+?\s+(?P<mitmdumpFile>\S+mitmdump)\s+-p\s+(?P<portStr>\d+)\s+-s\s+(?P<scriptFile>\S+?\.py)"
        mitmdumpCmdPattern   = "^\w+\s+(?P<pidStr>\d+).+\s+(?P<mitmdumpFile>\S+mitmdump)\s+-p\s+(?P<portStr>\d+)\s+-s\s+(?P<scriptFile>\S+?\.py)"
        # foundMitmdump = re.match(mitmdumpCmdPattern, eachLineStr, re.IGNORECASE)
        foundMitmdump = re.search(mitmdumpCmdPattern, eachLineStr, re.IGNORECASE)
        print("foundMitmdump=%s" % foundMitmdump)
        if foundMitmdump:
            isRunning = True
            matchedMitmdumpStr = foundMitmdump.group(0)
            print("matchedMitmdumpStr=%s" % matchedMitmdumpStr)
            pidStr = foundMitmdump.group("pidStr")
            pidInt = int(pidStr)
            mitmdumpFile = foundMitmdump.group("mitmdumpFile")
            portStr = foundMitmdump.group("portStr")
            portInt = int(portStr)
            scriptFile = foundMitmdump.group("scriptFile")
            # print("found mitmdump servive running=%s" % eachLineStr)
            curProcessDict = {
                "pid": pidInt,
                "mitmdumpFile": mitmdumpFile,
                "port": portInt,
                "scriptFile": scriptFile,
            }
            print("curProcessDict=%s" % curProcessDict)
            processInfoList.append(curProcessDict)

    return isRunning, processInfoList
```

输出：

可以检测到多种mitmdump的服务进程：

```bash
limao            20494  10.0  0.5  4722796  40256 s006  S+    5:52下午   1:02.40 /Users/limao/.pyenv/versions/3.8.0/bin/python3.8 /Users/limao/.pyenv/versions/3.8.0/bin/mitmdump -p 8081 -s electron-python-example/pymitmdump/mitmdumpUrlSaver.py

limao            20494   0.0  0.0  4508624   3212 s006  S+    5:52下午   1:05.88 /Users/limao/.pyenv/versions/3.8.0/bin/python3.8 /Users/limao/.pyenv/versions/3.8.0/bin/mitmdump -p 8081 -s electron-python-example/pymitmdump/mitmdumpUrlSaver.py

limao            25812   0.0  0.0  4344832    520 s012  S     9:19下午   0:00.20 /Users/limao/dev/crifan/mitmdump/mitmdumpUrlSaver/electron_python/electron-python-example/pymitmdump/mitmdump_executable/mac/mitmdump -p 8081 -s /Users/limao/dev/crifan/mitmdump/mitmdumpUrlSaver/electron_python/electron-python-example/pymitmdump/mitmdumpUrlSaver.py


limao            25051   0.0  0.7  4367712  54636 s004  S+    9:13下午   0:00.82 /Users/limao/dev/xxx/crawler/mitmdumpUrlSaver/venv/bin/python3.8 /Users/limao/dev/xxx/crawler/mitmdumpUrlSaver/venv/bin/mitmdump -p 8082 -s pymitmdump/mitmdumpUrlSaver.py

limao            25813   0.0  0.7  8604076  55424 s012  S+    9:19下午   0:00.53 /Users/limao/dev/crifan/mitmdump/mitmdumpUrlSaver/electron_python/electron-python-example/pymitmdump/mitmdump_executable/mac/mitmdump -p 8081 -s /Users/limao/dev/crifan/mitmdump/mitmdumpUrlSaver/electron_python/electron-python-example/pymitmdump/mitmdumpUrlSaver.py
```

可以解析返回出相关字段（另外一次调试的返回）：

```json
[
  {
    "pid": 25812,
    "mitmdumpFile": "/Users/limao/dev/crifan/mitmdump/mitmdumpUrlSaver/electron_python/electron-python-example/pymitmdump/mitmdump_executable/mac/mitmdump",
    "port": 8081,
    "scriptFile": "/Users/limao/dev/crifan/mitmdump/mitmdumpUrlSaver/electron_python/electron-python-example/pymitmdump/mitmdumpUrlSaver.py"
  },
...
]
```
