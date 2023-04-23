## 封装和解构

- 封装：将多个值使用逗号分隔，组合在一起，本质上是返回元组


```python
t1 = (1,2); t2 = 1, 2; type(t1), type(t2)
```




    (tuple, tuple)



- 解构：把线性结构的元素解开，并顺序的赋给其它变量，左边接纳的变量数要和右边解开的元素个数一致
    - 使用 `*变量名` 接收，但不能单独使用, 被 `*变量名` 收集后组成一个列表
    - `_`: 丢弃变量，如果不关心一个变量，就可以定义改变量的名字为`_`


```python
lst = [3, 5]; x, y = lst; print(x, y)
```

    3 5
    


```python
a, b = {'A': 100, 'B': 200}; print(a, b) # 非线性解构也可以结构
```

    A B
    


```python
lst = ['a', 'b', 'c', 'd']; head, *mid, tail = lst; print(head, mid, tail, sep='\n') # mid为一个列表
```

    a
    ['b', 'c']
    d
    


```python

```




    'a'




```python
lst = [1, 2, 3, 4, 5]; x, *_, y = lst; print(x,y) # 丢弃变量
```

    1 5
    


