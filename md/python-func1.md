## 函数

函数：由若干语句组成的语句块、函数名称、参数列表构成的完成一定功能的代码块，它是组织代码的最小单元

函数的作用：
- 结构化编程对代码的最基本封装，一般安装一定功能组织代码
- 封装的目的为了复用，减少代码冗余
- 代码更加简洁美观，可读易懂

### 函数定义，调用

```
def 函数名(参数列表):
   函数体
   [return 返回值]
```

- 函数名： 命名要求同标识符
- `return`： 函数没有return语句，默认返回 `None`
- 参数列表成为形式参数，只是一致符号表达，简称形参
- 函数调用： 函数通过函数名调用，传入参数成为实参：`函数名(实参)`


```python
def add(x, y):
    return x+y
result = add(4,6)
print(result)
```

    10
    

### 函数的参数

参数调用时传入的参数要与定义的参数个数相匹配
- 位置参数：按照参数定义顺序传入实参
- 关键字参数： 使用形参kv对的方式传入，不依赖参数定义的顺序，**位置参数必须在关键字之前传入**

参数列表的一般顺序为：普通参数`>` 缺省参数 `>` 可变位置参数 `>` keyword-only参数 `>` 可变关键字参数

### 函数参数默认值

定义时，在形参后面跟上一个值,主要用于简化函数的调用

```
def add(x,y=5): # y有参数默认值
   return x+y 
```

### 可变参数` (*args)`

在形参前加`*`, 表示该形参是一个可变参数，可以接收多个实参，args 收集参数为tuple


```python
def add(*args):
    sum = 0
    print(args)
    for i in args:
        sum+=i
    return (sum)
```


```python
add(1,2), add(1,2,3)
```

    (1, 2)
    (1, 2, 3)
    




    (3, 6)



### 可变关键字参数

形参前使用`**`,表示可以接收多个关键字参数，kwargs 收集参数组成一个字典


```python
def showkw(**kwargs):
    print(kwargs)
    for k,v in kwargs.items():
        print('{}=>{}'.format(k,v))
```


```python
showkw(a=1, b=2,c=3)
```

    {'a': 1, 'b': 2, 'c': 3}
    a=>1
    b=>2
    c=>3
    

### 混合参数

普通参数放在参数列表最前面，其次是可变位置参数，最后是可变关键字参数


```python
def sum(a, b, *args, **kwargs):
    print(args)
    print(kwargs)
    return (a+b)
```


```python
sum(1,2,3,4,5,x=10,y=20)
```

    (3, 4, 5)
    {'x': 10, 'y': 20}
    




    3



### keyword-only 参数

如果在一个星号`*`参数后，或者在一个可变位置参数后，出现一个普通参数，则这个普通参数是keyword-only参数


```python
def fn(*args, z):
    print(args, z)
```


```python
fn(1,2,3)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-85-6cde7c64455f> in <module>
    ----> 1 fn(1,2,3)
    

    TypeError: fn() missing 1 required keyword-only argument: 'z'



```python
fn(1,2,3,z=10)
```

    (1, 2, 3) 10
    


```python
def fn(*,x,y): # x,y 为keyword-only 参数
    print(x,y)
```


```python
fn(x=5,y=6)
```

    5 6
    

### 参数解构

给函数提供实参的时候，可以在集合类型前使用 `*` 或者 `**` 的方式将集合类型解开，取出所有的元素作为函数的实参


```python
def add(x, y):
    return x+y
```


```python
t = [2, 5];add(*t)
```




    7




```python
add(**{'x': 3, 'y':5})
```




    8



## 函数的返回值

python 函数使用 `return` 返回"返回值"，用于结束函数调用，返回值
- 所有的函数都有返回值，如果没有return语句，隐式调用 `return None`
- 一个函数可以存在多个 return 语句，但是只有一条被执行
- 函数如果执行了return语句，函数就会返回
- 函数不能同时返回多个值，看似返回多个值，其实被隐式封装成一个元组



```python
def showlst(a,b,c):
    return a,b,c
```


```python
showlst(1,2,3)
```




    (1, 2, 3)



## 函数作用域

一个标识符的可见范围，就是标识符的作用域，一般常说变量的作用域

- **全局作用域**：在整个程序运行环境可见
- **局部作用域**：在函数内部、类内可见


```python
# 外层变量作用域在内层作用域可见
def outer():
    o = 65
    def inner():
        print('inner {}'.format(o))
    print('outer {}'.format(o))
    inner()
```

outer()

**global关键字**

使用global关键字，会将函数或者类内的变量提升为全局变量，这种方法比较危险，破坏了函数的封装性，建议慎用

请思考以下为什么下面的代码会报错呢？


```python
x = 5
def fn():
    x+=1
    print(x)
```


```python
fn()
```


    ---------------------------------------------------------------------------

    UnboundLocalError                         Traceback (most recent call last)

    <ipython-input-109-e1d0f67027b9> in <module>
    ----> 1 fn()
    

    <ipython-input-108-4d42275130d4> in fn()
          1 x = 5
          2 def fn():
    ----> 3     x+=1
          4     print(x)
    

    UnboundLocalError: local variable 'x' referenced before assignment


上面代码报错的原因在于python是动态语言，先引用在赋值，而fn中 `x` 还未完成赋值，就被右边拿来做加1操作了，为了解决这个问题，需要引入global，将fn函数内的x提供为全局变量就不会报错了


```python
x = 5
def fn():
    global x
    x+=1
    print(x)
```


```python
fn()
```

    6
    

**nonlocal关键字**：

将变量标记为不再本地作用域的定义，而在上一级的某一级局部作用域，但不能是全局作用域的定义


```python
def counter():
    count = 0
    def inner():
        nonlocal count # 这里实现了闭包
        count +=1
        return count
    return inner
```


```python
counter()()
```




    1



## 函数作用域解析原则-LEGB

- `Local`：本地作用域
- `Enclosing`: 闭包嵌套函数的外部函数
- `Global`： 全局作用域
- `Build-in`: 内建变量
