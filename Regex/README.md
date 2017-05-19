# Regex in Python

## re usage example
```
import re

re.match(r'(.+)\+(.+)i', '12+34i').groups()
# ('12', '34')
```

## Tutorials
* [Regular Expression HOWTO](https://docs.python.org/2/howto/regex.html)

## raw string
* r'' is a raw string，能讓字串裡面的反斜線 \ 沒有功能，詳見 [string literals](https://docs.python.org/2/reference/lexical_analysis.html#string-literals)
* example:
  http://stackoverflow.com/questions/2241600/python-regex-r-prefix
  ```
  >>> '\n'
  '\n'
  >>> r'\n'
  '\\n'
  >>> print '\n'


  >>> print r'\n'
  \n
  ```
