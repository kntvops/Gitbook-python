## 字符串

- 一个个字符组成的有序的序列，是字符的集合
- 使用单引号、双引号、三引号引住的字符序列
-  字符串是**不可变**对象

### 字符串初始化


```python
s1 = 'string'
```


```python
s2 = "string2"
```


```python
s3 = '''this's a "strings"'''
```


```python
s4 = 'hello \nworld'
```


```python
print(s4)
```

    hello 
    world
    


```python
s5 = r'hello \nworld'
```


```python
print(s5)
```

    hello \nworld
    


```python
sql = """select * from user where user = 'root'"""
```

### 字符串元素访问-下标


```python
s = 'hello python'
```


```python
s[4]
```




    'o'




```python
for i in s:
    if i=='o':
        break
    print(i)
```

    h
    e
    l
    l
    


```python
list(s)
```




    ['h', 'e', 'l', 'l', 'o', ' ', 'p', 'y', 't', 'h', 'o', 'n']



### 字符串连接

- `"string".join(iterable) -> str`：将可迭代对象连接起来，使用string作为分隔符，返回一个新串。要求可迭代对象元素为字符串
- `+`: 将2个字符串连接在一起，返回一个新串 `'abc' + 'edf'= 'abcedf'`


```python
lst = ['a', 'b', 'c']
```


```python
'-'.join(lst), type('-'.join(lst))
```




    ('a-b-c', str)




```python
lst2 = [1, 'a', 'b', 2]
```


```python
'_'.join(lst2) # 报错，可迭代对象不为字符串
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-23-58458b361598> in <module>
    ----> 1 '_'.join(lst2)
    

    TypeError: sequence item 0: expected str instance, int found


### 字符串分割

- `split系`: 将字符串按照分隔符分割成若干字符串，并返回列表，分隔符号不在列表中
    - `split(sep=None, maxsplit=-1) -> list of strings`
    - `rsplit(sep=None, maxsplit=-1) -> list of strings`
- `partition系`: 将字符串按照分隔符分割成2段，返回这2段和分隔符的三元素的元组
    - `splitlines([keepends]) -> list of strings`
    - `partition(sep) -> (head, sep, tail)`
    - `rpartition(sep) -> (head, sep, tail)`


```python
# split(sep=None, maxsplit=-1) -> list of strings
#  从左至右
#  sep 指定分割字符串，缺省的情况下空白字符串作为分隔符
#  maxsplit 指定分割的次数，-1 表示遍历整个字符串
```


```python
s1 = "I'm \ta good student"
```


```python
s1.split()
```




    ["I'm", 'a', 'good', 'student']




```python
s1.split('g') # 分隔符不在列表中
```




    ["I'm \ta ", 'ood student']




```python
s1.split(' ', 1) # 一刀两段
```




    ["I'm", '\ta good student']




```python
s1.split('o', 2) # 2刀三段
```




    ["I'm \ta g", '', 'd student']




```python
# rsplit(sep=None, maxsplit=-1) -> list of strings
# 从右向左
# sep 指定分割字符串，缺省的情况下空白字符串作为分隔符
# maxsplit 指定分割的次数，-1 表示遍历整个字符串
```


```python
s1 = "I'm \ta good student"
```


```python
s1.rsplit()
```




    ["I'm", 'a', 'good', 'student']




```python
s1.rsplit('g')
```




    ["I'm \ta ", 'ood student']




```python
s1.rsplit(' ', 1)
```




    ["I'm \ta good", 'student']




```python
s1.rsplit('o', maxsplit=3)
```




    ["I'm \ta g", '', 'd student']




```python
# splitlines([keepends]) -> list of strings
# 按照行来切分字符串
# keepends 指的是是否保留行分隔符
# 行分隔符包括\n、\r\n、\r等
```


```python
'ab c\n\nde fg\rkl\r\n'.splitlines()
```




    ['ab c', '', 'de fg', 'kl']




```python
'ab c\n\nde fg\rkl\r\n'.splitlines(True)
```




    ['ab c\n', '\n', 'de fg\r', 'kl\r\n']




```python
s1 = '''I'm a super student.
You're a super teacher.'''
```


```python
print(s1)
```

    I'm a super student.
    You're a super teacher.
    


```python
s1.splitlines()
```




    ["I'm a super student.", "You're a super teacher."]




```python
s1.splitlines(keepends=True)
```




    ["I'm a super student.\n", "You're a super teacher."]




```python
#partition(sep) -> (head, sep, tail)
# 从左至右，遇到分隔符就把字符串分割成两部分，返回头、分隔符、尾三部分的三元组；如果
# 没有找到分隔符，就返回头、2个空元素的三元组
# sep 分割字符串，必须指定
```


```python
s1 = "i'm a good student"
```


```python
s1.partition('g')
```




    ("i'm a ", 'g', 'ood student')




```python
s1.partition('goo')
```




    ("i'm a ", 'goo', 'd student')




```python
s1.partition('z')
```




    ("i'm a good student", '', '')




```python
# rpartition(sep) -> (head, sep, tail)
# 从右至左，遇到分隔符就把字符串分割成两部分，返回头、分隔符、尾三部分的三元组；如果
# 没有找到分隔符，就返回2个空元素和尾的三元组
```


```python
s1
```




    "i'm a good student"




```python
s1.rpartition('g')
```




    ("i'm a ", 'g', 'ood student')




```python
s1.rpartition('goo')
```




    ("i'm a ", 'goo', 'd student')




```python
s1.rpartition('z')
```




    ('', '', "i'm a good student")



### 字符串大小写

- `upper()`：全大写
- `lower()`：全小写
- `swapcase()`：交互大小写


```python
s = "hElLo"
```


```python
s.upper()
```




    'HELLO'




```python
s.lower()
```




    'hello'




```python
s.swapcase()
```




    'HeLlO'



### 字符串排版

- `title() -> str`: 标题的每个单词都大写
- `capitalize() -> str`: 首个单词大写
- `center(width[, fillchar]) -> str`: `width` 打印宽度, `fillchar` 填充的字符
- `zfill(width) -> str`: `width` 打印宽度，居右，左边用0填充
- `ljust(width[, fillchar]) -> str`: 左对齐
- `rjust(width[, fillchar]) -> str`:  右对齐


```python
s = 'hello world'
```


```python
s.title()
```




    'Hello World'




```python
s.capitalize()
```




    'Hello world'




```python
s.center(20)
```




    '    hello world     '




```python
s.center(20, '_')
```




    '____hello world_____'




```python
s.zfill(20)
```




    '000000000hello world'




```python
s.ljust(20)
```




    'hello world         '




```python
s.rjust(20, "*")
```




    '*********hello world'



### 字符串修改

- `replace(old, new[, count]) -> str`: 字符串中找到匹配替换为新子串，返回新字符串, count表示替换几次，不指定就是全部替换
- `strip([chars]) -> str`: 从字符串两端去除指定的字符集chars中的所有字符, 如果chars没有指定，去除两端的空白字符
    - `lstrip([chars]) -> str`: 从左到右
    - `rstrip([chars]) -> str`: 从右至左


```python
'www python java hello com python'.replace('python', 'PYTHON')
```




    'www PYTHON java hello com PYTHON'




```python
'www python java hello com python'.replace('python', 'PYTHON', 1)
```




    'www PYTHON java hello com python'




```python
s = "\r \n \t Hello Python \n \t"
```


```python
s.strip()
```




    'Hello Python'




```python
s = "l am very very very sorry"
```


```python
s.strip('ly')
```




    ' am very very very sorr'



### 字符串查找

- `find(sub[, start[, end]]) -> int`: 在指定的区间`[start, end)`，从左至右，查找子串sub。找到返回索引，没找到返回-1
- `rfind(sub[, start[, end]]) -> int`: 在指定的区间`[start, end)`，从右至左，查找子串sub。找到返回索引，没找到返回-1
- `index(sub[, start[, end]]) -> int`: 在指定的区间`[start, end)`，从左至右，查找子串sub。找到返回索引，没找到抛出异常ValueError
- `rindex(sub[, start[, end]]) -> int`: 在指定的区间`[start, end)`，从左至右，查找子串sub。找到返回索引，没找到抛出异常ValueError
- `count(sub[, start[, end]]) -> int`: 在指定的区间`[start, end)`，从左至右，统计子串sub出现的次数


```python
s = 'reg.yyuap.local:81/yonbip/iuap-apdoc-finbd:20230417-7-39-pipeline-rt9fgi'
s.find('20230417-7-39'),s.find('20230417-7-99')
```




    (43, -1)




```python
s.index('20230417-7-39')
```




    43




```python
s.index('20230417-7-99')
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-106-8f81f9275929> in <module>
    ----> 1 s.index('20230417-7-99')
    

    ValueError: substring not found


### 字符串判断

- `endswith(suffix[, start[, end]]) -> bool`: 在指定的区间`[start, end)`，字符串是否是suffix结尾
- `startswith(prefix[, start[, end]]) -> bool`: 在指定的区间`[start, end)`，字符串是否是prefix开头


```python
'mysql.tar.gz'.endswith('.tar.gz')
```




    True



- `isalnum() -> bool`: 是否是字母和数字组成
- `isalpha()`: 是否是字母
- `isdecimal()`: 是否只包含十进制数字
- `isdigit()`: 是否全部数字(0~9)
- `isidentifier()`: 是不是字母和下划线开头，其他都是字母、数字、下划线
- `islower()`: 是否都是小写
- `isupper()`: 是否全部大写
- `isspace()`: 是否只包含空白字符

### 字符串格式化

- `printf-style formatting`
- `format函数格式`字符串语法——Python鼓励使用


```python
"I am %03d" % (20,), 'I like %s.' % 'Python', "I am %-5d" % (20,)
```




    ('I am 020', 'I like Python.', 'I am 20   ')




```python
"I'm {}, I am {} years old".format('tom', 29) # 位置参数
```




    "I'm tom, I am 29 years old"




```python
"{server} {1}:{0}".format(8888, '192.168.1.100', server='Web Server Info : ') # 关键字参数或命名参数
```




    'Web Server Info :  192.168.1.100:8888'



### 字符串对齐



```python
'{:20}'.format("test") ,'{:-<20}'.format("test")  # 左对齐
```




    ('test                ', 'test----------------')




```python
'{:^20}'.format("test"), '{:#^20}'.format("test") # 居中对齐
```




    ('        test        ', '########test########')




```python
'{:>20}'.format("test") , '{:*>20}'.format("test")  # 右对齐
```




    ('                test', '****************test')


