## 字典-dict

字典是**key-value键值对**的数据的集合，它**可变的**、**无序的**、**key不重复**的数据结构

### 字典的初始化

- `dict()` or `{}`: 空字典
- `dict(**kwargs)`:  使用name=value对初始化一个字典
- `dict(iterable, **kwarg)`: 使用可迭代对象和name=value对构造字典，不过可迭代对象的元素必须是一个二元结构
- `dict(mapping, **kwarg)`: 使用一个字典构建另一个字典
-  类方法`dict.fromkeys(iterable, value)`:
    - `dict.fromkeys(range(5))`
    - `d = dict.fromkeys(range(5),0)`
    
- `d = {'a':10, 'b':20, 'c':None, 'd':[1,2,3]}`: 直接定义


```python
dict(name="tom", age=18)
```




    {'name': 'tom', 'age': 18}




```python
dict([('name', 'tom'), ['age', 19]])
```




    {'name': 'tom', 'age': 19}




```python
s = {'a1': 10, 'a2': 20}
```


```python
dict.fromkeys(range(5), 'A')
```




    {0: 'A', 1: 'A', 2: 'A', 3: 'A', 4: 'A'}



### 字典元素的访问

- `d[key]`: 返回key对应的值value, key不存在抛出KeyError异常
- `get(key[, default])`: 返回key对应的值value, key不存在返回缺省值，如果没有设置缺省值就返回None
- `setdefault(key[, default])`: 返回key对应的值value, key不存在，添加kv对，value为default，并返回default，如果default没有设置，缺省为None


```python
d = {'a': 1, 'b': 2}
```


```python
d.get('a', 18), d.get('A', 20), d
```




    (1, 20, {'a': 1, 'b': 2})




```python
d.setdefault('a', 18), d.setdefault('A', 20), d
```




    (1, 20, {'a': 1, 'b': 2, 'A': 20})



### 字典元素的修改

- `d[key] = value`: 将key对应的值修改为value, key不存在添加新的kv对
- `update([other]) -> None`: 使用另一个字典的kv对更新本字典, key不存在，就添加;key存在，覆盖已经存在的key对应的值;就地修改


```python
d1 = {'a1': 1, 'a2': 2}; d2 = {'b1': 1, 'b2': 2 }
```


```python
d1.update(d2), d1
```




    (None, {'a1': 1, 'a2': 2, 'b1': 1, 'b2': 2})



### 字典元素的删除

- `pop(key[, default])`: key存在，移除它，并返回它的value;key不存在，返回给定的default; default未设置，key不存在则抛出KeyError异常
- `popitem()`: 移除并返回一个任意的键值对, 字典为empty，抛出KeyError异常
- `clear()`: 清空字典
- `del d[key]`: 返回None，key不存在抛出 KeyError


```python
d1 = {'a1': 1, 'a2': 2}
```


```python
d1.pop('a', 'A')
```




    'A'




```python
d1.popitem()
```




    ('a2', 2)




```python
del d1['a1']; 
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-56-1bafd33460f3> in <module>
    ----> 1 del d1['a1']; d1
    

    KeyError: 'a1'


### 字典的遍历

- `d.keys()`: 
- `d.value()`:
- `d.items()`:


```python
d = {'a': 1, 'b': 2, 'c': 3}
```


```python
d.keys(), type(d.keys()), 
```




    (dict_keys(['a', 'b', 'c']),
     dict_keys,
     dict_values([1, 2, 3]),
     dict_values,
     dict_items([('a', 1), ('b', 2), ('c', 3)]),
     dict_items)




```python
d.values(), type(d.values()) 
```




    (dict_values([1, 2, 3]), dict_values)




```python
d.items(), type(d.items())
```




    (dict_items([('a', 1), ('b', 2), ('c', 3)]), dict_items)




```python
for k, v in d.items():
    print(k, v)
```

    a 1
    b 2
    c 3
    

**字典遍历和移除**

字典在遍历的时候不能移除元素，为了移除元素，我们应该先遍历字典的key，取出所有的key构建为一个列表，然后根据列表对字典进行清理


```python
d = dict([('a', 1), ('b', 2), ('c', 3)]);d
```




    {'a': 1, 'b': 2, 'c': 3}




```python
key_list = []
for i in d.keys():
    key_list.append(i)
    
for k in key_list:
    if k == 'a':
        d.pop(k)

print(d)
```

    {'b': 2, 'c': 3}
    

## 默认字典-defaultdict

提供一个初始化函数，通过调用初始化函数来生成value 

- `collections.defaultdict([default_factory[, ...]])`
    - default_factory，缺省是None，它提供一个初始化函数, 当key不存在的时候，会调用这个工厂函数来生成key对应的value


```python
d = {}
for k in 'abcdef':
    for i in range(random.randint(1, 5)):
        if k not in d.keys():
            d[k] = []
        d[k].append(i)
print(d)
```

    {'a': [0, 1, 2, 3], 'b': [0, 1, 2, 3, 4], 'c': [0], 'd': [0, 1, 2, 3], 'e': [0, 1, 2], 'f': [0, 1, 2, 3]}
    


```python
from collections import defaultdict
import random

d1 = defaultdict(list)

for k in 'abcdef':
    for i in range(random.randint(1, 5)):
        d1[k].append(i)
print(d1)
```

    defaultdict(<class 'list'>, {'a': [0, 1, 2, 3], 'b': [0, 1, 2, 3, 4], 'c': [0, 1, 2, 3, 4], 'd': [0, 1, 2], 'e': [0, 1], 'f': [0, 1]})
    


```python
random.randint(1, 5)
```




    5



## 有序字典-OrderedDict

字典的key是无序的，可以使用OrderedDict记录顺序

有序字典可以记录元素插入的顺序，打印的时候也是按照这个顺序输出打印

3.6版本的Python的字典就是记录key插入的顺序（IPython不一定有效果）


```python
from collections import OrderedDict
import random

d = {'red': 1, 'yellow': 2, 'blue': 3, 'black': 5, 'gree': 6}
print(d)  # {'red': 1, 'yellow': 2, 'blue': 3, 'black': 5, 'gree': 6}

keys = list(d.keys())
print(keys) # ['red', 'yellow', 'blue', 'black', 'gree']

random.shuffle(keys)
print(keys) # ['gree', 'blue', 'red', 'yellow', 'black']

od = OrderedDict()
for key in keys:
    od[key] = d[key]
print(od) # OrderedDict([('gree', 6), ('blue', 3), ('red', 1), ('yellow', 2), ('black', 5)])

print(od.keys()) # odict_keys(['gree', 'blue', 'red', 'black', 'yellow'])
```