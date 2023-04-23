## 列表解析List Comprehension

列表解析式是一种语法糖

- 编译器会优化，不会因为简写而影响效率，反而因优化提高了效率
- 减少程序员工作量，减少出错
- 简化了代码，但可读性增强

`[返回值 for 元素 in 可迭代对象 if 条件]`: 使用中括号[]，内部是for循环，if条件语句可选


```python
# [返回值 for 元素 in 可迭代对象 if 条件],  使用中括号[]，内部是for循环，if条件语句可选
[x for x in range(10) if x%2==0]
```




    [0, 2, 4, 6, 8]



`[expr for item in iterable if cond1 if cond2]` ：同时满足多个条件


```python
# lst = []
# for x in range(20):
#     if x%2==0:
#         if x%3==0:
#             lst.append(x)
# print(lst)

[x for x in  range(20) if x%2==0  if x%3==0] # 等价 [x for x in  range(20) if x%2==0 and x%3==0]
```




    [0, 6, 12, 18]



`[expr for i in iterable1 for j in iterable2 ]`: 对多个可迭代对象中的元素进行操作


```python
# lst = []
# for x in range(3):
#     for y in range(3):
#         lst.append(x+y)
# print(lst)

[x+y for x in range(3) for y in range(3)]
```




    [0, 1, 2, 1, 2, 3, 2, 3, 4]




```python
[(x, y) for x in range(3) for y in range(3)]
```




    [(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]




```python
[[x, y] for x in range(3) for y in range(3)]
```




    [[0, 0], [0, 1], [0, 2], [1, 0], [1, 1], [1, 2], [2, 0], [2, 1], [2, 2]]



## 生成器表达式Generator expression

列表解析式的中括号换成小括号,则返回一个生成器，生成器表达式是按需计算（或称**惰性求值**、**延迟计算**），需要的时候才计算值

生成器得元素可以迭代，迭代完以后，不能回头，否则会报错 `StopIteration`

- `(返回值 for 元素 in 可迭代对象 if 条件)`



```python
 ("{:04}".format(i) for i in range(1,5))
```




    <generator object <genexpr> at 0x0000022A009ABE60>




```python
g =  ("{:04}".format(i) for i in range(1,5))
```


```python
next(g)
```




    '0001'




```python
next(g)
```




    '0002'




```python
for x in g:
    print(x)
```

    0003
    0004
    


```python
next(g)
```


    ---------------------------------------------------------------------------

    StopIteration                             Traceback (most recent call last)

    <ipython-input-61-e734f8aca5ac> in <module>
    ----> 1 next(g)
    

    StopIteration: 


## 集合解析式

列表解析式的中括号换成大括号`{}`,则立即返回一个集合解析式

- `{返回值 for 元素 in 可迭代对象 if 条件}`


```python
 {(x,x+1) for x in range(10)}， 
```




    {(0, 1),
     (1, 2),
     (2, 3),
     (3, 4),
     (4, 5),
     (5, 6),
     (6, 7),
     (7, 8),
     (8, 9),
     (9, 10)}



## 字典解析式

列表解析式的中括号换成大括号{}，使用key:value形式
    
- `{返回值 for 元素 in 可迭代对象 if 条件}`


```python
{str(x):x+1 for x in range(5)}
```




    {'0': 1, '1': 2, '2': 3, '3': 4, '4': 5}




```python
{x:y for x in 'abc' for y in [18, 20, 30]}
```
