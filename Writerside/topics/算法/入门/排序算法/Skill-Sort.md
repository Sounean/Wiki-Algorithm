# 刷排序题技巧
<show-structure for="chapter,procedure" depth="2"/>

只要题目中没明确表明不能用sort函数，或者指明用某种算法去解题，其实所有排序题都能用c++/python中自带的库去解决。

## 一、C++ 
### 1.1sort()排序函数
#### 1.1.1使用方式 
基本语法：sort(begin,end,cmp)

其中三个参数:1.begin:指向待排数组的第一个元素的地址。
2.end:指向待排数组的最后一个元素的下一个位置的地址。
3.cmp:自定义参数。可写可不写(下文介绍具体用法)。

#### 1.1.2对整形数组从小到大排序 
sort函数最简单的实现即默认的从小到大的排序：

```C++
#include <iostream>
#include<algorithm>
using namespace std;
 
int main( )
{
	int arr[8]={49,38,65,97,76,13,27,49};
	sort(arr,arr+8);    // 如果第一个参数是数组开头，后一个是数组末尾其实还可以arr.begin(),arr.end()
	cout<<"排序之后的代码:";
	for(int i=0;i<8;i++)
	{
		cout<<arr[i]<<" ";
	}
	
	return 0;
}
```
{collapsible="true" collapsed-title="具体实现"}

运行结果:13 27 38 49 49 65 76 97

#### 1.1.3.对整形数组从大到小排序

这个时候就要用到cmp参数了，直接加上参数`greater<int>()`后即可实现。
即上文改成`sort(arr,arr+8,greater<int>())`;

#### 1.1.4.各种类型的自定义排序
这个时候就更要用上cmp函数了，就是利用他去确认一个排序的规律(即让cmp去指定相邻两个元素之间的大小关系):

利用字典序排序:
```C++
#include <iostream>
#include <algorithm>
using namespace std;
 
bool cmp(string x, string y) {                              
	return x  > y ;
}
string arr1[1001];
int main()
{
	int n;
	cin >> n;
	for (int i = 0; i < n; i++) {
		cin >> arr1[i];
	}
	sort(arr1, arr1 + n, cmp);
	for (int i = 0; i < n; i++) {
		cout << arr1[i];
	}
	return 0;
}
```
{collapsible="true" collapsed-title="具体实现"}

利用个位数大小排序:
```C++
#include <iostream>
#include <algorithm>
using namespace std;
 
bool cmp(int x, int y) {
	return x % 10 > y % 10;
}
 
int main() {
	int num[8] = { 49,38,65,97,76,13,27,49 };
	sort(num, num + 8, cmp);
	for (int i = 0; i < 8; i++) {
		cout << num[i] << " ";
	}
 
	return 0;
 
}
```
{collapsible="true" collapsed-title="具体实现"}

输出结果:49 49 38 97 27 76 65 13

结构体排序：
```C++
#include <iostream>
#include <algorithm>
using namespace std;
 
struct student{
	string name;
	int score;
};
 
bool cmp(student x, student y) {
	return x.score < y.score;
}
 
int main()
{
	int n;
	cin >> n;
	struct student s[n];
	for (int i = 0; i < n; i++) {
		cin >> s[i].name >> s[i].score;
	}
	sort(s, s + n, cmp);
	for (int i = 0; i < n; i++) {
		cout << s[i].name << " " << s[i].score << endl;
	}
 
	return 0;
}
```
{collapsible="true" collapsed-title="具体实现"}


### 1.2.next_permutation全排列函数
会按照字典序大小进行往后排列一个.

```C++
#include <iostream>
#include <algorithm>    // next_permutation所在的库

using namespace std;

int main(){

    int a[5] = {7,6,2,1,3};
    do{
        for (int i = 0; i < 5; ++i) {
            cout << a [i] << " ";
        }
        cout << endl;
    } while (next_permutation(a,a+5));
    
    return 0;
}
```
{collapsible="true" collapsed-title="具体实现"}

输出：
```C++
7 6 2 1 3
7 6 2 3 1
7 6 3 1 2
7 6 3 2 1
```

也可以对部分区域进行全排列，写法和sort差不多。

主要应用于需要枚举所有可能排列或按字典序生成下一排列的算法问题中。

性能限制：时间复杂度，单次调用O(n),全排列O(n!);<br/>
适用规模:n<=10 (10! = 3.6*$10^6$ 在竞赛算法题中可以接受)

题：P1706



<warning>
未排序的序列（如 {2, 1, 3}）会从当前状态生成排列，导致遗漏最小排列。就像上方，没经过sort排，造成一开始就是以76213开头而不是12367开头.
</warning>

<warning>
next_permutation 会跳过重复排列（因按字典序生成），无需额外去重。
</warning>

总结与题型关联表:

| 问题类型         | 典型例题                                       | 核心操作                 | 难度   |
|------------------|--------------------------------------------|--------------------------|--------|
| 全排列生成       | 输出1~n的所有排列([题1](P1706.md)，[题2](ABC201.md)) | 枚举并打印排列           | 入门   |
| 数字谜题（带分数）| 蓝桥杯带分数([题1](LCouSuanShi.md),[题2](LDaiFenShu.md))       | 分割排列验证算式         | 中等   |
| 乘积等式         | 7254 = 39 × 186                            | 分割数字验证乘积         | 中等   |
| 序列性质验证     | ABC201A等差数列                                | 验证排列是否满足条件     | 简单   |

[还有一种自定义规则的，和sort那种差不多的cmp函数定义](Poj1256.md)

前期训练最好先用常用dfs函数去解决，下附上dfs解决全排列的思路:
```C++
void dfs(int num,int last)
{
    if(num == n + 1){
        for(int i = 1; i <= n; ++i)cout<<ans[i]<<" ";
        return;
    }
    for(int i = 1; i <= n; ++i){
        if(used[i]) continue;
        used[i] = 1;
        ans[num] = i;
        dfs(num + 1, i);
        used[i] = 0;
    }
}
```
{collapsible="true" collapsed-title="dfs解决全排列"}

有了next_permutation函数了，还学啥dfs这种的？还累？<br/>
答：next_permutation函数代码简洁高效、自动处理重复元素且时间复杂度可控（单次调用 next_permutation 为O(n)，全排列为 O(n! × n)，与 DFS 的
O(n!) 同阶）；<br/>
但是！1.无法灵活剪枝(next_permutation 必须生成完整排列，无法在生成中途终止无效分支；而dfs可在递归中提前剪枝：
典型场景有效括号组合、满足特定约束的排列)

## 二、Python

### 2.1.sort函数

在 Python 中，运算符重载（Operator Overloading） 允许我们为自定义对象定义运算符的行为。例如，我们可以重载 + 让它支持两个对象相加，而不是仅限于内置数据类型（如 int、str）。

#### 2.1.1.基本概念
Python 允许重载的大部分运算符都是通过 特殊方法（Magic Methods / Dunder Methods） 实现的。这些方法以 __ 开头和结尾，例如：
```Python
__add__：重载 +
__sub__：重载 -
__mul__：重载 *
__truediv__：重载 /
__floordiv__：重载 //
__mod__：重载 %
__pow__：重载 **
__eq__：重载 ==
__lt__：重载 <
__le__：重载 <=
__gt__：重载 >
__ge__：重载 >=
__str__：重载 str()
__repr__：重载 repr()
```
#### 2.1.2.各类符号重载例子
#### 重载 + 号 (__add__)

假设我们有一个 Point 类表示二维坐标点，我们希望 + 号支持两个 Point 对象相加：

```Python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        """重载 + 号，实现点的坐标相加"""
        if isinstance(other, Point):
            return Point(self.x + other.x, self.y + other.y)
        raise TypeError("Unsupported operand type for +")

    def __repr__(self):
        """返回可读的字符串"""
        return f"Point({self.x}, {self.y})"

# 测试
p1 = Point(3, 5)
p2 = Point(2, 4)
p3 = p1 + p2  # 等价于 p1.__add__(p2)

print(p3)  # 输出：Point(5, 9)
```
{collapsible="true" collapsed-title="具体实现"}

####  重载 - 号（__sub__）

```Python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __sub__(self, other):
        """重载 - 号，实现点的坐标相减"""
        if isinstance(other, Point):
            return Point(self.x - other.x, self.y - other.y)
        raise TypeError("Unsupported operand type for -")

    def __repr__(self):
        return f"Point({self.x}, {self.y})"

# 测试
p1 = Point(10, 8)
p2 = Point(3, 4)
p3 = p1 - p2  # 等价于 p1.__sub__(p2)

print(p3)  # 输出：Point(7, 4)
```
{collapsible="true" collapsed-title="具体实现"}

#### 重载 \* 号（__mul__）
```Python
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __mul__(self, scalar):
        """重载 * 号，使向量支持数乘"""
        if isinstance(scalar, (int, float)):
            return Vector(self.x * scalar, self.y * scalar)
        raise TypeError("Multiplication only supports int or float")

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

# 测试
v1 = Vector(3, 4)
v2 = v1 * 2  # 等价于 v1.__mul__(2)

print(v2)  # 输出：Vector(6, 8)
```
{collapsible="true" collapsed-title="具体实现"}

####  重载比较运算符（==, <, > 等）
```Python
class Student:
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def __eq__(self, other):
        """重载 == 号"""
        return self.score == other.score

    def __lt__(self, other):
        """重载 < 号"""
        return self.score < other.score

    def __gt__(self, other):
        """重载 > 号"""
        return self.score > other.score

    def __repr__(self):
        return f"Student({self.name}, {self.score})"

# 测试
s1 = Student("Alice", 90)
s2 = Student("Bob", 85)
s3 = Student("Charlie", 90)

print(s1 == s3)  # True
print(s1 > s2)   # True
print(s2 < s3)   # True
```
{collapsible="true" collapsed-title="具体实现"}

#### 题目实战
python中有sort函数，可以默认让int数组从大到小排；我们可以通过对>号的运算符重载，使其不单单能对int数组进行排序。

假如有一个小团体，他们每个人都有名字和年龄，请让你根据他们的年龄从小大进行排序：

```Python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def __gt__(self, other):
        # 定义比较规则：按照年龄从大到小排序
        return self.age > other.age
    
    def __repr__(self):
        # 用于打印对象信息
        return f"Person(name='{self.name}', age={self.age})"
# 创建Person对象列表
people = [
    Person("Alice", 25),
    Person("Bob", 20),
    Person("Charlie", 30),
    Person("David", 22)
]
# 使用sort方法进行排序
people.sort()
# 打印排序后的结果
print("按照年龄从大到小排序：")
for person in people:
    print(person)
# 如果你想按照年龄从小到大排序，可以使用reverse参数
people.sort(reverse=True)
print("
按照年龄从小到大排序：")
for person in people:
    print(person)
```
{collapsible="true" collapsed-title="具体实现"}

现在如果又有一个需求，每个学生有语文、数学和英语的成绩；我想实现：1.谁数学成级最高谁排前面，2.数学成绩一样时，语文谁高谁排前面，3.语文再一样时，英语谁高谁排前面
```Python
class Student:
    def __init__(self,name,chinese,math,english):
        self.name = name
        self.chinese = chinese
        self.math = math
        self.english = english

    def __gt__(self, other):
        if self.math!=other.math:
            return self.math > other.math
        elif self.chinese!=self.chinese:
            return self.chinese > other.chinese
        elif self.english!=self.english:
            return self.english>other.english

    def printSelf(self):
        print(self.name,":",self.chinese,",",self.math,",",self.chinese)

students = [
    Student("Jack" , 100 ,99 ,99 ),
    Student("John" , 100,98,0),
    Student("William" , 97,96,95),
    Student("David" , 96,100,95)
]

students.sort(reverse=True)

for i in students:
    i.printSelf()
```
{collapsible="true" collapsed-title="具体实现"}

输出：
```Python
David : 96 , 100 , 96
Jack : 100 , 99 , 100
John : 100 , 98 , 100
William : 97 , 96 , 97
```

### 2.2.permutations函数
```Python
from itertools import permutations

# 生成所有排列
for perm in permutations([1, 2, 3]):
    print(perm)
# 输出：  按照从大到小的顺序输出，但是要记住先对他进行排序了
# (1, 2, 3)
# (1, 3, 2)
# (2, 1, 3)
# (2, 3, 1)
# (3, 1, 2)
# (3, 2, 1)

# 生成长度为2的排列
for perm in permutations([1, 2, 3], 2):
    print(perm)
# 输出：
# (1, 2)
# (1, 3)
# (2, 1)
# (2, 3)
# (3, 1)
# (3, 2)
```
{collapsible="true" collapsed-title="具体实现"}

早点学西嘎嘎得了，这里的函数，西嘎噶的更方便.



