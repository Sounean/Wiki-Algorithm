# 选择排序算法

```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n - 1):
        # 假设当前位置的元素为最小值
        min_index = i
        for j in range(i + 1, n):
            # 在剩余部分中寻找最小值的索引
            if arr[j] < arr[min_index]:
                min_index = j
                # 将当前位置的元素与最小值进行交换
        if min_index != i:
            arr[i], arr[min_index] = arr[min_index], arr[i]


# 测试代码
numbers = [4, 2, 6, 1, 3]
selection_sort(numbers)
print(numbers)  
# 输出：[1, 2, 3, 4, 6]
```


Start typing here...