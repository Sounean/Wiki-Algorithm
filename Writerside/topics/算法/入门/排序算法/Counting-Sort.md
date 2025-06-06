# 1.计数排序

假设生活中有那么一个场景：你们要春游，在临行前，你需要操场上乱哄哄的学生们，怎么弄最方便呢？

你在操场讲台前，先划分了一块区域， 用白色粉笔灰在地上按照从左往右的顺序，写上“一年级、二年级....六年级”，<br/>
然后你去一个个叫学生，让他们过来，自己按照前面写的序号排列成一列列，等排完了，就排序好了。

下面这种方法还省了点空间，其实可以不省，写的更简单
## py写法
```Python
def counting_sort(nums):
    """
    计数排序：计数元素出现的次数并将数据重组
    时间复杂度：O(n+k),k为数据范围的长度
    空间复杂度：O(n+k)
    """
    n = len(nums)
    max_value, min_value = max(nums), min(nums)
    range_value = max_value - min_value + 1  # 数据范围的长度

    count = [0] * range_value  # 计数数组，存储每个元素出现的次数
    output = []  # 输出数组，存储排序后的结果

    # 统计元素出现的次数，num - min_value是为了将所有数值偏移到从0开始的位置
    for num in nums:
        count[num - min_value] += 1

    # 正常输出，count代表列表中元素所代表的数字出现了几次
    for i in range(len(count)):
        for j in range(count[i]):
            output.append(i + min_value)


    return output

sortList = counting_sort([5,2,1,6,8,9])
print(sortList)
```