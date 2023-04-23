## 递归函数

函数直接或者间接调用自身就是递归
- 递归一定要由边界条件
    - 条件不满足，继续递归
    - 条件满足，递归返回


```python
def fib(n):
    if n<2:
        return 1
    else:
        return fib(n-1)+fib(n-2)
```


```python
for i in range(10):
    print(fib(i),end=',')
```

    1,1,2,3,5,8,13,21,34,55,

## 匿名函数

匿名函数即没有名字的函数， python借助 `lambda` 表达式构建匿名函数, 例如： `lambda x:x**2`， 在高阶函数传时，使用匿名函数可以简化代码
- 参数列表不需要小括号
- 冒号是用来分割参数列表和表达式的
- 不需要return语句，表达式就是匿名函数的返回值
- lambda 表达式只能在写在一行，所以称为单行函数


```python
(lambda x:x+5)(5)
```




    10




```python
f = lambda x,y: x+y
```


```python
f(4, 5)
```




    9



## 高阶函数

只要满足以下两个条件之一的函数，都称为高阶函数
- 接受一个或者多个函数作为参数
- 输出一个函数


```python
def counter(base):
    def inc(step=1):
        nonlocal base
        base += step
        return base
    return inc
```


```python
counter(1)()
```




    2



### 自定义sort函数

仿照内建函数sorted，请自行实现一个sort函数（不使用内建函数），能够为列表元素排序


```python
def mysort(iterable):
    ret = []
    for x in iterable:
        for i, y in enumerate(ret):
            if x<y:
                ret.insert(i,x)
                break
        else:
            ret.append(x)
    return ret
```


```python
mysort([2,5,3,4,1,8,9,6,7])
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
def mysort(iterable, reverse=False):
    ret = []
    for x in iterable:
        for i, y in enumerate(ret):
            com = x>y if  reverse else x<y
            if com:
                ret.insert(i,x)
                break
        else:
            ret.append(x)
    return ret
```


```python
mysort([2,5,3,4,1,8,9,6,7])
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
mysort([2,5,3,4,1,8,9,6,7], reverse=True )
```




    [9, 8, 7, 6, 5, 4, 3, 2, 1]

