# 2.选择排序算法

和生活中打扑克一样，下方是模拟一个打扑克新手排列牌的情况：

拿到手后，从前往后找，找出最大的，抽出来，放到最前面第一位，然后再在剩下 的牌堆中去找他里面最大的，再抽出来排到最前面第二位，直到卡片排完，就排列完了。

在移动的途中，我们就可以发现每次我们去抽牌放到牌头位子时，左边的有顺序的扑克就会越来越多，右侧无序的就越来越少；
等到都变有序的，我们就排列完了。

非常简单，你需要在脑子里中有个印象，你修改何处，能实现将原来的"从小变大"变成"从大变小"就说明掌握了。

##  python写法
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

## C++写法
下述只写了模拟“找最小值”放到指定位置的过程
```C++
.
```
