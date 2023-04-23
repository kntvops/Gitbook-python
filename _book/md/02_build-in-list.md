
## 列表

列表是一个有序，可索引的，可变的，线性结构，列表中的个体称为元素，元素可以是任意对象

### 列表的初始化

- `list()`: 创建一个空列表
- `lst =  []`
- `lst = [1, 2, 3, 4, 5]`
- `lst = list(itertable)`

### 列表的访问

列表通过索引进行访问，索引也称作下标。例如： `lst[3]`

- 正索引：从左至右，从0开始，为列表中的每个元素编号
- 负索引：从右至左，从 `-1` 开始

正负索引都不能超界，否则会引发 `IndexError`

### 列表的查询

- `index(value,[start,[stop]])`：通过值找索引，匹配到第一个值则返回索引，匹配不到则报错 `ValueError`,时间复杂度为 `O(1)`
- `count(value)`：统计列表中元素的个数，时间复杂度为 `O(1)`
- `len()`：返回列表的长度

### 列表元素修改

- `list[index] = value`：索引不能超界

### 列表元素增加、插入

- `append(object) -> None`：尾部追加，就地修改，返回 None,时间复杂度是`O(1)`
- `insert(index, object) -> None`：在指定的索引index处插入元素object，就地修改，时间复杂度是O(n)，索引超界面（上界）尾部追加，下界头部追加
- `extend(iteratable) -> None`：将可迭代对象的元素追加进来，返回None，就地修改
- `+`： 连接操作，将两个列表连接起来，产生新列表，本质上调用的是__add__()方法，例如：`list(range(3)) + list(range(3)) => [0, 1, 2, 0, 1, 2]`
- `*`：重复操作，将本列表元素重复n次，返回新的列表，例如：`list(range(2))*3 => [0, 1, 0, 1, 0, 1]`

### 元素的删除

- `remove(value) -> None`：从左至右查找第一个匹配value的值，移除该元素，返回None。就地修改，时间复杂度为 `o(1)`
- `pop([index]) -> item`：从指定位置弹出索引，不指定则弹出最后一个元素
- `clear() -> None`：清空所有元素

### 列表反转，排序

- `reverse() -> None`：将列表元素反转，返回None，就地修改
- `sort(key=None, reverse=False) -> None`：对列表元素进行排序，就地修改，默认升序
- `in`：判断对象是否在列表中

### 列表的复制

- `copy() -> List`：浅复制，影子拷贝，只复制引用

```python
In [1]: lst = [1, [1, 2, 3], 2, 3]

In [2]: newlst = lst.copy()

In [3]: newlst
Out[3]: [1, [1, 2, 3], 2, 3]

In [4]: newlst[1][0] = 'a'

In [5]: newlst
Out[5]: [1, ['a', 2, 3], 2, 3]

In [6]: lst     # newlst的变化引起lst也跟着变化
Out[6]: [1, ['a', 2, 3], 2, 3]
```

- deepcopy：深拷贝

```python

In [1]: import copy

In [2]: lst = [1, [1, 2, 3], 2, 3]

In [3]: newlst = copy.deepcopy(lst)

In [4]: newlst
Out[4]: [1, [1, 2, 3], 2, 3]

In [5]: newlst[1][0] = 'a'

In [6]: newlst
Out[6]: [1, ['a', 2, 3], 2, 3]

In [7]: lst   # newlst的变化不会引起lst跟着变化
Out[7]: [1, [1, 2, 3], 2, 3]
```

### 列表的切片

切片是指通过索引区间访问线性结构的一段数据

- `sequence[start:stop]` 表示返回`[start, stop)`区间的子序列
    - 支持负索引
    - start为0，可以省略
    - stop为末尾，可以省略
    - 超过上界（右边界），就取到末尾；超过下界（左边界），取到开头
    - start一定要在stop的左边

- `[:]` 表示从头至尾，全部元素被取出，等效于copy()方法
- `[start:stop:step]`: 步长切片
    - step为步长，可以正、负整数，默认是1
    - step要和start:stop同向，否则返回空序列


```python
lst = ['a', 'b', 'c', 'd', 'e', 'f']
```


```python
for i,v in enumerate(lst):
    print(i,v)
```

    0 a
    1 b
    2 c
    3 d
    4 e
    5 f
    


```python
lst[:]
```




    ['a', 'b', 'c', 'd', 'e', 'f']




```python
lst[1:3]
```




    ['b', 'c']




```python
lst[-3:-1]
```




    ['d', 'e']




```python
lst[::2]
```




    ['a', 'c', 'e']




