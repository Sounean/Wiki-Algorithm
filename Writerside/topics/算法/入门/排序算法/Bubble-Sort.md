# 3.冒泡算法

明白了选择排序，我们可以将“从头找到尾”的逻辑改成“从最后面出发，相邻的两两相比，如果谁更大/小，就换到前面”，这样一趟下来也能找到最大/小的。

如果就到这一步的话，其实冒泡和选择没有太大区别，但是！如果其中的某一趟比较后，发现并没有挪动任何卡片，其实就可以中止排序行为了，因为在那个时候
，其实牌序已经被拍好！

冒泡排序重点是两两比较和交互，这一点要搞清。而如果你能很快的反应过来"我要从大排到小和从小排到大只需要修改哪个符号",就说明已经完全懂了。


C++版本:（从前往后比）
```C++
#include <iostream>
using namespace std;
 
void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n-1; i++) {        // 外层循环控制排序的轮数
        for (int j = 0; j < n-i-1; j++) {  // 内层循环进行相邻元素比较和交换
            if (arr[j] > arr[j+1]) {
                // 交换两个元素的位置
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
 
int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr)/sizeof(arr[0]);
    bubbleSort(arr, n);
    // 打印排序后的数组
    for (int i=0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
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

## 复杂度分析

![img.png](../../../../images/排序算法/img2.png)

- 空间复杂度 O(1) -->原地排序