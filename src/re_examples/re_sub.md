# re.sub实例

## Evernote的content处理

### 去掉最开始的xml头

处理前：

```html
<?xml version="1.0" encoding="UTF-8" standalone="no"?>\n<!DOCTYPE en-note SYSTEM "http://xml.evernote.com/pub/enml2.dtd">\n<en-note>xxx
```

代码：

```python
re.sub('<\?xml version="1.0" encoding="UTF-8" standalone="no"\?>\s*', "", noteHtmlWithXml)
```

处理后：

```html
<!DOCTYPE en-note SYSTEM "http://xml.evernote.com/pub/enml2.dtd">\n<en-note>xxx
```

### 去掉开始的en-note头

处理前：

```html
<!DOCTYPE en-note SYSTEM "http://xml.evernote.com/pub/enml2.dtd">xxx
```

或：

```html
<!DOCTYPE en-note SYSTEM "http://xml.evernote.com/pub/enml2.dtd">\nxxx
```

或：

```html
<!DOCTYPE en-note SYSTEM 'http://xml.evernote.com/pub/enml2.dtd'>xxx
```

代码：

```python
noteHtmlNoEnNote = re.sub("""<!DOCTYPE en-note SYSTEM ((")|('))http://xml\.evernote\.com/pub/enml2\.dtd((")|('))>\s*""", "", eachNoteWithEnNote)
```

处理后：

```html
xxx
```

代码解析：

* `((")|('))`：用于匹配双引号`"`或`'`都支持
* `\s*`：用于匹配最后的`\n`

### 处理en-meida的tag

处理前：

```html
<en-media hash="7c54d8d29cccfcfe2b48dd9f952b715b" type="image/png"></en-media>
```

代码：

```python
re.sub("(?P<enMedia><en-media\s+[^<>]+)>\s*</en-media>", "\g<enMedia> />", noteHtmlEnMedia)
```

处理后：

```bash
<en-media hash="7c54d8d29cccfcfe2b48dd9f952b715b" type="image/png" />
```

### 替换最顶层tag

处理前：

```html
<html>
  xxx
  yyy
  zzz
</html>
```

代码：

```python
noteContent = re.sub('<html>(?P<contentBody>.+)</html>', "<en-note>\g<contentBody></en-note>", noteHtml)
```

处理后：

```html
<en-note>
  xxx
  yyy
  zzz
</en-note>
```

代码解析：

* `(?P<contentBody>.+)`和`\g<contentBody>`
  * `(?P<contentBody>.+)`：是替换前的 pattern，是普通的命名的组`named group`
  * `\g<contentBody>`：是被替换为的`repl`的内容，其中可以用`\g<groupName>`，表示引用替换内容中的命名的组
    * 此处用来：引用之前html的内容主体contentBody部分的字符串
