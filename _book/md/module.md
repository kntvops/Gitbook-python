## 随机数模块 - random 模块

- `randint(a, b)`: 返回[a, b]之间的整数
- `choice(seq)`: 从非空序列的元素中随机挑选一个元素
- `randrange ([start,] stop [,step])`: 从指定范围内，按指定基数递增的集合中获取一个随机数,缺省值为1。
- `random.shuffle(list) ->None`: 就地打乱列表元素
- `sample(population, k)`: 从样本空间或总体（序列或者集合类型）中随机取出k个不同的元素，不可重复
- `choices(population, k)`: 从样本空间或总体（序列或者集合类型）中随机取出k个不同的元素，可重复

```
In [1]: import random

In [2]: random.randint(10, 30)
Out[2]: 25

In [3]: random.choice(range(10))
Out[3]: 1

In [4]: random.randrange(1,8,4)
Out[4]: 5

In [5]: lst = [1, 2, 3, 4, 5, 6]

In [6]: random.shuffle(lst)

In [7]: lst
Out[7]: [6, 4, 5, 1, 3, 2]

In [8]: random.sample(lst, 4)
Out[8]: [2, 6, 4, 1]

In [12]: lst
Out[12]: [0, 1, 2, 3, 4]

In [13]: random.choices(lst, k=4) # 
Out[13]: [4, 3, 1, 3]
```

## 时间模块-datetime

- 类方法
    - `today()`: 返回本地时区当前时间的datetime对象
    - `now(tz=None)`: 返回当前时间的datetime对象，时间到微秒，如果tz为None，返回和today()一样
    - `utcnow()`: 没有时区的当前时间
    - `fromtimestamp(timestamp, tz=None)`: 从一个时间戳返回一个datetime对象
- datetime对象
    - `timestamp()`: 返回一个到微秒的时间戳, 时间戳：格林威治时间1970年1月1日0点到现在的秒数
    - 构造方法 `datetime.datetime(2016, 12, 6, 16, 29, 43, 79043)`
    - `year`、`month`、`day`、`hour`、`minute`、`second`、`microsecond`: 取datetime对象的年月日时分秒及微秒
    - `weekday()`: 返回星期的天，周一0，周日6
    - `isoweekday()`: 返回星期的天，周一1，周日7
    - `date()`: 返回日期date对象
    - `time()`: 返回时间time对象
    - `replace()`: 修改并返回新的时间
    - `isocalendar()`: 返回一个三元组(年，周数，周的天)
- 日期格式化
    - 类方法 `strptime(date_string, format)` :返回datetime对象
    - 对象方法 `strftime(format)`: 返回字符串, 字符串format函数格式化
- timedelta对象
    - timedelta = datetime1 - datetime2


```python
import datetime
```


```python
datetime.datetime.now(), type(datetime.datetime.now())
```




    (datetime.datetime(2023, 4, 21, 15, 2, 23, 404598), datetime.datetime)




```python
dt = datetime.datetime.strptime("21/11/06 16:30", "%d/%m/%y %H:%M");dt
```




    datetime.datetime(2006, 11, 21, 16, 30)




```python
dt.strftime("%Y-%m-%d %H:%M:%S"), type(dt.strftime("%Y-%m-%d %H:%M:%S"))
```




    ('2006-11-21 16:30:00', str)




```python
print("{0:%Y}/{0:%m}/{0:%d} {0:%H}::{0:%M}::{0:%S}".format(dt))
```

    2006/11/21 16::30::00
    


```python
import time
import datetime

start = datetime.datetime.now()

time.sleep(6)

delta = (datetime.datetime.now()-start).total_seconds()

print(delta, type(delta))
```

    6.008981 <class 'float'>
    