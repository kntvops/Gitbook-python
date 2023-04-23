## 查看属性

- `__dir__`: 返回类或者对象的所有成员**名称列表**，`dir()`函数本质上调用的此方法。

    - 如果对象是模块： 返回的列表为模块的属性名合变量名
    - 如果对象是类对象，返回的列表为类的属性名及其祖先类的属性名
    - 如果类是实例：
        - 有 `__dir__` 方法，返回可叠戴对象的返回值
        - 没有`__dir__` 方法，返回实例的属性名、类的属性及其祖先类的属性名

- `locals()`: 返回当前作用域中的变量字典
- `globals()`: 返回当前模块全局变量的字典

## 魔术方法

### 实例化

- `__new__`: 实例化一个对象，该方法是静态方法，需要返回一个cls的实例，否则不会调用 `__init__` 方法
- `__init__`: 对 `__new__` 方法创建的实例进行初始化配置
- `__del__`: 当实例引用计数为0时，对实例对象做资源释放等清理操作

> 初始化一个实例，需要通过调用 `__new__` 方法进行实例创建，调用 `__init__`方法,完成创建。


```python
class A:
    def __new__(cls, *args, **kwargs):
        print(cls)
        print(args)
        print(kwargs)
        
        return super().__new__(cls) # 一般使用基类 object的__new__方法创建实例并且返回
        
    def __init__(self, name):
        
        self.name = name

a = A("tom")
print(a)
```

    <class '__main__.A'>
    ('tom',)
    {}
    <__main__.A object at 0x7ff3682cacc0>


### 可视化

- `__str__`: 直接调用(`print(a)`, `str(a)`, `format(a)`)实例优使用这个方法**获取实例字符串的表达**，如果没有定义，则调用`__repr__`方法，如果`__repr__`也没有定义，则直接返回对象的内存地址信息
- `__repr__`: 间接调用实例会使用这个方法**获取实例的字符串表达**,如果没有定义，则返回object的定义即显示内存地址信息
- `__bytes__`: 返回实例的bytes表达


```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return 'str: {}-{}'.format(self.name, self.age)
    
    def __repr__(self):
        return 'repr: {}-{}'.format(self.name, self.age)
    def __bytes__(self):
        return 'bytes: {}-{}'.format(self.name, self.age).encode()
tom = Person('tom', 28)
```


```python
print(tom), print(str(tom)), print("{}".format(tom))
```

    str: tom-28
    str: tom-28
    str: tom-28





    (None, None, None)




```python
print([tom]), print((tom,)), print({tom})
```

    [repr: tom-28]
    (repr: tom-28,)
    {repr: tom-28}





    (None, None, None)




```python
print(bytes(tom))
```

    b'bytes: tom-28'


- `__eq__`: 判断两个实例对象内容是否相等，如果定义了这个方法，不提供`__hash__`方法，那么实例是不可hash的
- `__hash__`: 如果定义了此方法，则该类实例是可hash的

> 判断两个对象是否可以去重，首先不能仅通过`__hash__`判断其hash值是否一样，还要通过`__eq__`对其内容进行对比


```python
class A:
    def __init__(self, name):
        self.name = name
    def __repr__(self):
        return self.name
```


```python
hash(A('a'))
```




    -9223363244142149183




```python
class A:
    def __init__(self, name):
        self.name = name
        
    def __eq__(self,other):
        return self.name == other.name
    
    def __repr__(self):
        return self.name
```


```python
hash(A('a')) 
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-55-2cf1a0e02051> in <module>()
    ----> 1 hash(A('a'))
    

    TypeError: unhashable type: 'A'



```python
import collections
isinstance(A('a'), collections.Hashable) # 不可hash对象一定为False
```




    False




```python
class A:
    def __init__(self, name):
        self.name = name
        
    def __eq__(self,other):
        return self.name == other.name
    
    def __repr__(self):
        return "instance {}".format(self.name)
    
    def __hash__(self):
        return 1
```


```python
import collections
isinstance(A('a'), collections.Hashable)
```




    True




```python
a=A('a');b=A('b'); hash(a), hash(b); print({a, b})  # 为什么hash值一样，集合没有去重呢？
```

    {instance a, instance b}



```python
class A:
    def __init__(self, name):
        self.name = name
        
    def __eq__(self,other):
        return True
    
    def __repr__(self):
        return "instance {}".format(self.name)
    
    def __hash__(self):
        return 1
```


```python
a=A('a');b=A('b'); hash(a), hash(b); print({a, b}) # 因为实例a跟实例b不仅hash值一样，而且 __eq__ 返回的内容也一样， 所以集合去重了
```

    {instance a}


- `__bool__`: 对象调用这个函数返回布尔值，没有定义此函数就找`__len__()`,返回长度，非0为真，如果`__len__`，也没有定义，那么所有实例都返回真
- `__len__`: 返回对象的长度


```python
class A: pass
```


```python
print(bool(A)), print(bool(A()))
```

    True
    True





    (None, None)




```python
class A:
    def __bool__(self):
        return False
```


```python
print(bool(A)), print(bool(A()))
```

    True
    False





    (None, None)




```python
class A:
    def __len__(self):
        return 0
```


```python
print(bool(A)), print(bool(A()))
```

    True
    False





    (None, None)




```python
class A:
    def __len__(self):
        return 1
```


```python
print(bool(A)), print(bool(A()))
```

    True
    True





    (None, None)



### 运算符重载

| 运算符 | 特殊方法 | 含义 |
| --- | --- | --- |
| `<` `<=` `==` `>` `>=` `!=`| `__lt__` `__le__` `__eq__` `__gt__` `__ge__` `__ne__`| 比较运算符 |
| `+` `-` `*` `/` `%` `//` `**` `divmod` | `__add__` `__sub__` `__mul__ ` `__truediv__` </br>`__mod__` `__floordiv__` `__pow__` `__fivmod__` | 算术运算符 |
| `+=` `-=` `*=` `/=` `%=` `//=` `**=`| `__iadd__` `__isub__` `__imul__ ` `__itruediv__` <br> `__imod__` `__ifloordiv__` `__ipow__` |  `__ixx__` 方法一般用来修改自身，如果没有定义则会调用 `__xx__` | 

完成 Point 类设计，实现判断点相等的办法，并且完成向量的加法。

- A(x1, y1)
- B(x2, y2)
- A+B = (x1+x2, y1+y2)
- A-B = (x1-x2, y1-y2)


```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        
    def __eq__(self, other):
        # return (self.x, self.y) == (other.x, other.y)
        return self.x == other.x and self.y == other.y
    
    def __add__(self, other): # p1+p2 # 返回一个新的实例
        return Point(self.x+other.x, self.y+other.y)
    
    def __repr__(self):
        return '<Point: {},{} [{}]>'.format(self.x, self.y, id(self))
```


```python
p1 = Point(2, 5); id(p1)
```




    140683402024832




```python
p2 = Point(3, 4)
```


```python
print(p1 + p2) # 返回一个新实例
```

    <Point: 5,9 [140683401539368]>



```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        
    def __eq__(self, other):
        # return (self.x, self.y) == (other.x, other.y)
        return self.x == other.x and self.y == other.y
    
    def __add__(self, other): # p1+p2 # 返回一个新的实例
        return Point(self.x+other.x, self.y+other.y)
    
    def __repr__(self):
        return '<Point: {},{} [{}]>'.format(self.x, self.y, id(self))
    
    def add(self, other):
        return self+other # 会调用 __add__ 链式编程
```


```python
p1 = Point(2, 5); id(p1)
```




    140683401313696




```python
p2 = Point(3, 4)
```


```python
p1.add(p2)
```




    <Point: 5,9 [140683401312800]>




```python
p1.add(p2).add(Point(3,3)) # 链式编程
```




    <Point: 8,12 [140683401468616]>




```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        
    def __eq__(self, other):
        # return (self.x, self.y) == (other.x, other.y)
        return self.x == other.x and self.y == other.y
    
    def __iadd__(self, other): # p1+=p2 # 不会返回新的实例，修改实例
        self.x = self.x+other.x
        self.y = self.y+other.y
        return self
    
    def __repr__(self):
        return '<Point: {},{} [{}]>'.format(self.x, self.y, id(self))
```


```python
p1 = Point(2, 5); id(p1)
```




    140683402480608




```python
p2 = Point(3, 4)
```


```python
p1 += p2;p1 
```




    <Point: 5,9 [140683402480608]>



**`@functools.total_ordering` 装饰器**

对于比较大小的必须实现的方法，`__lt__` `__le__` `__eq__` `__gt__` `__ge__` `__ne__`，如果全部写完则太麻烦了，通过这个装饰器，我们只需要实现`__eq__`和其它方法中的任意一个就可以实现全部的比较方法了，但是这个装饰器可能会带来性能问题，所以建议慎用词装饰器。


```python
from functools import total_ordering

@total_ordering
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
    def __eq__(self, other):
        return self.age == other.age
    def __gt__(self,other):
        return self.age > other.age
```


```python
tom = Person('tom', 20);jerry = Person('jerry', 16)
```


```python
print(tom > jerry),print(tom < jerry), print(tom >= jerry), print(tom <= jerry)
```

    True
    False
    True
    False





    (None, None, None, None)



### 容器相关的方法

- `__len__`:
- `__iter__`:
- `__containers__`:
- `__getitem__`:
- `__setitem__`:
- `__missing__`:

