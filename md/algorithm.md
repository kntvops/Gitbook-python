## 冒泡法

冒泡法为交换排序，两两比较，交换位置，如同水一样咕嘟往上冒。

```python 
# 算法1
# nums = [1, 9, 8, 5, 6, 7, 4, 3, 2]
nums = [1, 2, 3, 4 ,5,6, 7, 9, 8]
length = len(nums)

count_swap = 0 
count  = 0  
for i in range(length): 
    for j in range(length-i-1):
        count += 1
        if nums[j] > nums[j+1]:
            nums[j], nums[j+1] = nums[j+1], nums[j]
            count_swap += 1

print(nums, count,count_swap)     
```   
```python
# 算法2：使用打标记的方式，提前跳出交换
# nums = [1, 9, 8, 5, 6, 7, 4, 3, 2]
nums = [1, 2, 3, 4 ,5,6, 7, 9, 8]
length = len(nums)

count_swap = 0 
count  = 0  


for i in range(length): 
    flag = False
    for j in range(length-i-1):
        count += 1
        if nums[j] > nums[j+1]:
            nums[j], nums[j+1] = nums[j+1], nums[j]
            count_swap += 1
            flag = True
    if not flag:
        break

print(nums, count,count_swap)         
``` 

## 选择排序

两两比较大小，找出极值（极大值或极小值）被放置在固定的位置，这个固定位置一般指的是某一端
-  时间复杂度O(n2)
- 减少了交换次数，提高了效率，性能略好于冒泡法

```

```

## 插入排序