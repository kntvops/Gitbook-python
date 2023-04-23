## 集合-set

- set 是**可变的**、**无序的**、**不重复**的元素的集合
- set 内的元素都是**可hash**的

线性结构的查询时间复杂度是O(n)，即随着数据规模的增大而增加耗时, set、dict等结构，内部使用hash值作为key，**时间复杂度可以做到O(1)**，查询时间和数据规模无关

### 集合初始化

- `set()`: new empty set object
- `set(iterable)`: new set object


```python
set(), set(range(5))
```




    (set(), {0, 1, 2, 3, 4}, dict)




```python
{}, type({}) # {} 为字典
```




    ({}, dict)




```python
{(1,2), (3,)}
```




    {(1, 2), (3,)}




```python
{(1,2), (3,), [2]} # 列表不可hash
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-58-9048cc38f9c7> in <module>
    ----> 1 {(1,2), (3,), [2]} # 列表不可hash
    

    TypeError: unhashable type: 'list'


## set 操作

- `add(elem)`: 增加一个元素到set中, 如果元素存在，什么都不做
- `update(*others)`: 合并其他元素到set集合中来,参数others必须是可迭代对象,就地修改
- `remove(elem)`: 从set中移除一个元素;元素不存在，抛出KeyError异常。为什么是KeyError？
- `discard(elem)`: 从set中移除一个元素, 元素不存在，什么都不做
- `pop() -> item`: 移除并返回任意的元素, 空集返回KeyError异常
- `clear()`: 移除所有元素


```python
s = {1,2,3}
```


```python
s.add('a'); s 
```




    {1, 2, 3, 'a'}




```python
s.update(range(5)); s
```




    {0, 1, 2, 3, 4, 'a'}




```python
s.remove(4); s  
```




    {0, 1, 2, 3, 'a'}




```python
s.discard(2); s
```




    {0, 1, 3, 'a'}




```python
s.pop()
```




    0




```python
s.clear()
```


```python
s.pop()
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-72-c88c8c48122b> in <module>
    ----> 1 s.pop()
    

    KeyError: 'pop from an empty set'


### 集合操作

- 全集： 所有元素的集合。例如实数集，所有实数组成的集合就是全集
- 子集subset和超集superset: 一个集合A所有元素都在另一个集合B内，A是B的子集，B是A的超集
- 真子集和真超集: A是B的子集，且A不等于B，A就是B的真子集，B是A的真超集
    - `issubset(other)` or `<=`:  判断当前集合是否是另一个集合的子集
    - `set1 < set2`: 判断set1是否是set2的真子集
    - `issuperset(other)` ort `>=`: 判断当前集合是否是other的超集
    - `set1 > set2`: 判断set1是否是set的真超集
    - `isdisjoint(other)`: 当前集合和另一个集合没有交集, 没有交集，返回True
- 并集: 将两个集合A和B的所有的元素合并到一起，组成的集合称作集合A与集合B的并集
    - `union(*others)` or `|`: 返回和多个集合合并后的新的集合
    - `update(*others)` or `|=`: 和多个集合合并，就地修改
- 交集: 集合A和B，由所有属于A且属于B的元素组成的集合
    - `intersection(*others)` or `&`: 返回和多个集合的交集
    - `intersection_update(*others)` or `&=`: 获取和多个集合的交集，并就地修改
- 差集：集合A和B，由所有属于A且不属于B的元素组成的集合
    - `difference(*others)` or `-`:  返回和多个集合的差集
    - `difference_update(*others)` or `-=`: 获取和多个集合的差集并就地修改
- 对称差集: 集合A和B，由所有不属于A和B的交集元素组成的集合，记作（A-B）∪（B-A）
    - `symmetric_differece(other)` or `^`: 返回和另一个集合的差集
    - `symmetric_differece_update(other)` or `^=`: 获取和另一个集合的差集并就地修改

