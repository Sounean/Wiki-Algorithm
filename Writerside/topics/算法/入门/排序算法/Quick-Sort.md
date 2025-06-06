# 5.快速排序

<note>竞赛最普遍使用的</note>

前面几种基础算法，对于数据量小的情况完全够用了。也是必须要看到字眼里面不需要推理就能将核心代码大致讲出来的。

从这里开始，变得复杂了，存在一定门槛，更加抽象，需要理解。对于数据量大的数据集，效率也更高。

以要从小到大为例子，他的思路是先在无序的列表中找一个“标兵”，我们最后的趋势肯定是要让标兵左边的都比他小，右边的都比他大才算是比原先的有序些了，
所以我们从无序列表的最左侧开始，一直找到标兵左边不停找出比标兵大的，不符合的；最右侧也是，从无序列表的最右侧开始，一直找到标兵右边不停找出比标兵小的，不符合的；
然后将这两个不符合的进行交换.

## python写法
```Python

class QuickSort:

    def quick_sort(self, nums):
        """
        快速排序：每次都要选择一个基准，将数组分为两部分，一部分都比基准小，一部分都比基准大
        时间复杂度：平均情况:O(nlogn),最坏情况(选取的基准总是最小或最大元素):O(n^2),最好情况：O(nlogn)
        空间复杂度：O(nlogn),递归调用栈的空间
        """
        return self.quick_sort_helper(nums, 0, len(nums) - 1)

    def quick_sort_helper(self, nums, first, last):
        """ 快速排序辅助函数 """
        if first < last:
            pivot = nums[first]

            i, j = first + 1, last
            while True:
                while i <= j and nums[i] <= pivot:
                    i += 1
                while i <= j and nums[i] >= pivot:
                    j -= 1
                if i <= j:
                    nums[i], nums[j] = nums[j], nums[i]
                else:
                    break
            nums[first], nums[j] = nums[j], nums[first]

            self.quick_sort_helper(nums, first, j - 1)
            self.quick_sort_helper(nums, j + 1, last)
        return nums
```