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

  protocolStrList = re.findall(r"\@protocol \w+.+?\@end", inputStr, flags=re.DOTALL)
  logging.debug("protocolStrList=%s", protocolStrList)

  for eachProtocolStr in protocolStrList:
      logging.info("eachProtocolStr=%s", eachProtocolStr)
```

输出效果：

```bash
20250101 11:26:44 dsdump.py:218  INFO    eachProtocolStr=@protocol NSSecureCoding <NSCoding>
  // class methods
 +(BOOL)supportsSecureCoding

@end
20250101 11:26:46 dsdump.py:218  INFO    eachProtocolStr=@protocol NSCoding
  // instance methods
 -(void)encodeWithCoder:(id)arg1 
 -(void)encodeWithCoder:(id)arg1 
 -(id)initWithCoder:(id)arg1 

@end
20250101 11:26:52 dsdump.py:218  INFO    eachProtocolStr=@protocol TransactionListener
  // instance methods
 -(void)onTransactionStarted
 -(void)onTransactionCompleted:(id)arg1 isTransactionSuccessful:(SEL)arg2 

@end
```
