## bytes、bytearray

python3 引入两个新类型
- `bytes`： **不可变**字节序列
- `bytearray`： **可变**字节数组

**编码和解码**

- `str-> bytes`: 编码,字符串按照不同的字符集编码encode返回字节序列bytes
    - `encode(encoding='utf-8', errors='strict') -> bytes`
- `bytes -> str`: 解码，字节序列按照不同的字符集解码decode返回字符串
    - `bytes.decode(encoding="utf-8", errors="strict") -> str`
    - `bytearray.decode(encoding="utf-8", errors="strict") -> str`


```python
'abc'.encode(encoding='utf-8'), b'abc'.decode(encoding='utf-8')
```




    (b'abc', 'abc')



**需要熟练记忆ASCII码表**

- `\x00`： C语言中的字符串结束符
- `\x09`: tab制表符
- `\x0d0a`: `\r\n` 换行符
- `\0x30` ~ `\0x39`: 字符0~9
- `\0x41`: A, 65
- `\0x61`: a 97


```python
'a'.encode().hex(),  '\t'.encode().hex(), '\r'.encode().hex(), '\n'.encode().hex(), ('0').encode().hex()
```




    ('61', '09', '0d', '0a', '30')



### bytes定义

- `bytes()`: 空bytes
- `bytes(int)`: 指定字节的bytes，被0填充
- `bytes(iterable_of_ints)`: 返回`bytes [0,255]`的int组成的可迭代对象
- `bytes(string, encoding[, errors])`: bytes 等价于string.encode()
- `bytes(bytes_or_buffer)`: `immutable copy of bytes_or_buffer` 从一个字节序列或者buffer复制出一个新的不可变的bytes对象
- 使用b前缀定义
   - 只允许基本ASCII使用字符形式:`b'abc9'`
   - 使用16进制表示:`b"\x41\x61"`
   
### bytes操作

bytes的操作方法和字符串类似，只不过bytes的方法，输入的是bytes，输出的也是bytes



```python
b'abcdef'.replace(b'ab', b'AB')
```




    b'ABcdef'



`bytes.fromhex(string)`: string必须是2个字符的16进制的形式，'6162 6a 6b'，空格将被忽略


```python
'abc'.encode().hex(), bytes.fromhex('616263')
```




    ('616263', b'abc')



### bytearray定义

- `bytearray()`: 空bytearray
- `bytearray(int)`: 指定字节的bytearray，被0填充
- `bytearray(iterable_of_ints)`:  `bytearray [0,255]`的int组成的可迭代对象
- `bytearray(string, encoding[, errors])`: bytearray 近似string.encode()，不过返回可变对象
- `bytearray(bytes_or_buffer)`: 从一个字节序列或者buffer复制出一个新的可变的bytearray对象

>  注意，b前缀定义的类型是bytes类型


```python
bytearray(), bytearray(8), bytearray([1,2,3]),  bytearray('abc', encoding='utf-8')
```




    (bytearray(b''),
     bytearray(b'\x00\x00\x00\x00\x00\x00\x00\x00'),
     bytearray(b'\x01\x02\x03'),
     bytearray(b'abc'))



### bytearray 操作

bytearray 与 bytes的类型的方法类似


```python
bytearray(b'abcdef').replace(b'ab', b'AB'), bytearray.fromhex('abc'.encode().hex()), 'abc'.encode().hex()
```




    (bytearray(b'ABcdef'), bytearray(b'abc'), '616263')



- `append(int)`: 尾部追加一个元素
- `insert(index, int)`: 在指定索引位置插入元素
- `extend(iterable_of_ints)`: 将一个可迭代的整数集合追加到当前bytearray
- `pop(index=-1)`: 从指定索引上移除元素，默认从尾部移除
- `remove(value)`: 找到第一个value移除，找不到抛ValueError异常
> 注意：上述方法若需要使用int类型，值在`[0, 255]`

- `clear()`: 清空bytearray
- `reverse()`: 翻转bytearray，就地修改

