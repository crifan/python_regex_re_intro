# dsdump解析优化

输入：

```objc
@protocol NSSecureCoding <NSCoding>
  // class methods
 +(BOOL)supportsSecureCoding

@end

@protocol NSCoding
  // instance methods
 -(void)encodeWithCoder:(id)arg1 
 -(void)encodeWithCoder:(id)arg1 
 -(id)initWithCoder:(id)arg1 

@end

@protocol TransactionListener
  // instance methods
 -(void)onTransactionStarted
 -(void)onTransactionCompleted:(id)arg1 isTransactionSuccessful:(SEL)arg2 

@end
```

代码：

```py
import re

protocolEndP = r"\@protocol (?P<protocolName>\w+).+?\@end"
logging.debug("protocolEndP=%s", protocolEndP)
protocolStrIterator = re.finditer(protocolEndP, out, flags=re.DOTALL)
protocolStrList = list(protocolStrIterator)
logging.debug("protocolStrList=%s", protocolStrList)

for curIdx, eachProtocolMatch in enumerate(protocolStrList):
    curNum = curIdx + 1
    protocolName = eachProtocolMatch.group("protocolName")
    crifanLogging.logSingleLine(curNum, protocolName)

    logging.debug("eachProtocolMatch=%s", eachProtocolMatch)
    eachProtocolStr = eachProtocolMatch.group(0)
    logging.debug("eachProtocolStr=%s", eachProtocolStr)

    logging.debug("protocolName=%s", protocolName)
    protocolFilename = "%s.h" % protocolName
    logging.debug("protocolFilename=%s", protocolFilename)
    ...
```

输出效果：

```bash
20250101 11:31:51 crifanLogging.py:492  DEBUG   ---------- [1] NSSecureCoding ----------
20250101 11:31:51 dsdump.py:225  DEBUG   eachProtocolMatch=<re.Match object; span=(0, 89), match='@protocol NSSecureCoding <NSCoding>\n  // class m>
20250101 11:31:52 dsdump.py:227  DEBUG   eachProtocolStr=@protocol NSSecureCoding <NSCoding>
  // class methods
 +(BOOL)supportsSecureCoding

@end
20250101 11:32:02 dsdump.py:231  DEBUG   protocolName=NSSecureCoding
20250101 11:32:02 dsdump.py:233  DEBUG   protocolFilename=NSSecureCoding.h
20250101 11:32:04 crifanLogging.py:492  DEBUG   ---------- [2] NSCoding ----------
20250101 11:32:04 dsdump.py:225  DEBUG   eachProtocolMatch=<re.Match object; span=(91, 235), match='@protocol NSCoding\n  // instance methods\n -(voi>
20250101 11:32:04 dsdump.py:227  DEBUG   eachProtocolStr=@protocol NSCoding
  // instance methods
 -(void)encodeWithCoder:(id)arg1 
 -(void)encodeWithCoder:(id)arg1 
 -(id)initWithCoder:(id)arg1 

@end
20250101 11:32:05 dsdump.py:231  DEBUG   protocolName=NSCoding
20250101 11:32:05 dsdump.py:233  DEBUG   protocolFilename=NSCoding.h
20250101 11:32:06 crifanLogging.py:492  DEBUG   ---------- [3] TransactionListener ----------
20250101 11:32:06 dsdump.py:225  DEBUG   eachProtocolMatch=<re.Match object; span=(237, 398), match='@protocol TransactionListener\n  // instance meth>
20250101 11:32:06 dsdump.py:227  DEBUG   eachProtocolStr=@protocol TransactionListener
  // instance methods
 -(void)onTransactionStarted
 -(void)onTransactionCompleted:(id)arg1 isTransactionSuccessful:(SEL)arg2 

@end
20250101 11:32:06 dsdump.py:231  DEBUG   protocolName=TransactionListener
20250101 11:32:06 dsdump.py:233  DEBUG   protocolFilename=TransactionListener.h
```
