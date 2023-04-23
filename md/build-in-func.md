## 内建函数

- `id(obj)`: 返回对象的唯一标识，CPython返回内存地址


```python
a = 'A';id(a)
```




    2901761080600



- `hash()`: 返回一个对象的哈希值


```python
a = 'A'; hash(a), type(hash(a))
```




    (5516771245369437470, int)



 - `type()`: 返回对象的类型

类型转换
- float() 
- int() 
- bin() 
- hex() 
- oct() 
- bool() 
- list() 
- tuple() 
- dict() 
- set() 
- complex() 
- bytes() 
- bytearray()

- `input([prompt])`: 接收用户输入，返回一个字符串

- `print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)`:  打印输出，默认使用空格分割、换行结尾，输出到控制台

- `len(s)`: 返回一个集合类型的元素个数

-  `isinstance(obj, class_or_tuple)`: 判断对象obj是否属于某种类型或者元组中列出的某个类型


```python
 isinstance(True, int), isinstance('a', str), isinstance('0', str),  isinstance(1, bool)
```




    (True, True, True, False)



- `issubclass(cls, class_or_tuple)`: 判断类型cls是否是某种类型的子类或元组中列出的某个类型的子类


```python
issubclass(bool, int)
```




    True



- `abs(x)`: 绝对值
- `max()`: 最大值
- `min()`: 最小值
- `round(x)`:  四舍六入五取偶


```python
round(-0.5), round(2.5),round(2.4),round(2.6)
```




    (0, 2, 2, 3)



- `pow(x , y)`:  x**y
- `divmod(x, y)`: tuple (x//y, x%y)


```python
divmod(7, 3) , 7//3, 7%3
```




    ((2, 1), 2, 1)



- `chr(i)`:  给一个一定范围的整数返回对应的字符


```python
chr(97)
```




    'a'



- `ord(c)`:  返回字符对应的整数


```python
ord('A')
```




    65



- `sorted(iterable[, key][, reverse])`: 返回一个新的列表，默认升序,reverse是反转
- `reversed(seq)`: 返回一个翻转元素的迭代器
- `enumerate(seq, start=0)`: 迭代一个序列，返回索引数字和元素构成的二元组
- `iter(iterable)`: iter将一个可迭代对象封装成一个迭代器

- `zip(*iterables)`: 拉链函数, 像拉链一样，把多个可迭代对象合并在一起，返回一个迭代器,将每次从不同对象中取到的元素合并成一个元组


```python
list(zip(range(3),range(2))) # 木桶原理
```




    [(0, 0), (1, 1)]




```python
dict(zip(range(3),range(3)))
```




    {0: 0, 1: 1, 2: 2}




```python
{str(x):y for x,y in zip(range(3),range(3))}
```




    {'0': 0, '1': 1, '2': 2}


