# 3.冒泡算法

明白了选择排序，我们可以将“从头找到尾”的逻辑改成“从最后面出发，相邻的两两相比，如果谁更大/小，就换到前面”，这样一趟下来也能找到最大/小的。

如果就到这一步的话，其实冒泡和选择没有太大区别，但是！如果其中的某一趟比较后，发现并没有挪动任何卡片，其实就可以中止排序行为了，因为在那个时候
，其实牌序已经被拍好！

冒泡排序重点是两两比较和交互，这一点要搞清。而如果你能很快的反应过来"我要从大排到小和从小排到大只需要修改哪个符号",就说明已经完全懂了。


C++版本:（从后往前比）
```C++
void bubbleSort(int data[], int len)
{
    for(int i = len - 1; i >= 0; i--) # 1.本质只需要len-1次循环即可（因为确认了len-1个的大小后，最后一个的大小其实也被确认下来了）
    {
        int flag = 0;  // flag用来判断是否执行了数据交换的操作
        for (int j = 0; j < i; j++)   # 2.内循环的比较次数
        {
            if (data[j + 1] < data[j])
            {
                int tmp;
                tmp = data[j];
                data[j] = data[j + 1];
                data[j + 1] = tmp;
                flag++;    // 如果执行过数据交换，则flag不为0
            }
        }
        
        /*
           当执行完一次扫描就判断是否执行过数据交换，如果没有执行过数据
           交换，则表示此时数列已经是排好序的，不需要打印中间排序的结果。
        */
        if (flag == 0)
            break;
	}
}
```

Python版本:(从前往后比)
```Python
def bubble_sort_optimized(arr):
    n = len(arr)
    for i in range(n-1):   # 1.本质只需要n-1次循环即可（因为确认了n-1个的大小后，最后一个的大小其实也被确认下来了）
        swapped = False
        for j in range(n-i-1):  # 2.内循环的比较次数
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
                swapped = True
        if not swapped:
            break
    return arr


arr = [15, 169, 2000, 1000, 87, 34, 990]
print('待排序的数组为：', arr)
print('从小到大排序后结果为：', bubble_sort_optimized(arr))
```