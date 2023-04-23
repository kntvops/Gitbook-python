## 元组

元组是一个有序的，**不可变**的，用小括号表示的对象

元组是只读的，所以增、改、删方法都没有

### 元组的定义

- `tuple()`：空元组
- `tuple(iterable)`: 由可迭代对象组成的元组
- `(1, )`: 一个元素的元组，逗号`,`不可省略

### 元组元素访问

元组也是通过索引访问：`tuple(index)`, 正负索引不可以超界，否则引发异常 `IndexError`

### 元组查询

- `index(value,[start,[stop]])`: 通过值value，从指定区间查找列表内的元素是否匹配,返回匹配到的第一个索引，匹配不到抛出异常 `常ValueError`,`O(n)`
- `count(value)`: 返回列表中匹配value的次数, `O(n)`
- `len(tuple)`: 返回元素的个数

## 命名元组-namedtuple

Python集合中的命名元组类namedTuples为元组中的每个位置赋予意义，并增强代码的可读性和描述性。它们可以在任何使用常规元组的地方使用，且增加了通过名称而不是位置索引方式访问字段的能力。其来自Python内置模块 `collections`

```
In [1]:  from collections import namedtuple

In [2]:  Students = namedtuple('Students', ['id', 'name', 'score'])

In [3]:  S_1 = Students('001', 'tom', '98')

In [4]:  S_2 = Students('002', 'jerry', '68')

In [5]:  print(S_1)
Students(id='001', name='tom', score='98')

In [6]:  print(S_2[1])
jerry

In [7]:  print(S_2.name)
jerry
```