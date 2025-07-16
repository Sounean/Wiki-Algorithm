# python 转 c++

# Python 到 C++ 基础语法快速指南

## 变量类型对比

| Python       | C++           | 说明                          |
|--------------|---------------|-----------------------------|
| `x = 10`     | `int x = 10;` | 整数类型                     |
| `y = 3.14`   | `double y = 3.14;` | 浮点数（C++默认双精度）      |
| `s = "hello"`| `std::string s = "hello";` | 字符串（需要`#include <string>`）|
| `b = True`   | `bool b = true;` | 布尔值（C++为小写）          |
| 动态类型      | 静态类型        | C++必须声明变量类型          |

## 分支结构

python
```python
if x > 5:
    print("大于5")
elif x == 5:
    print("等于5")
else:
    print("小于5")
```

C++
```C++
#include <iostream>
using namespace std;

int main() {
    int x = 10;
    if (x > 5) {
        cout << "大于5" << endl;
    } 
    else if (x == 5) {
        cout << "等于5" << endl;
    }
    else {
        cout << "小于5" << endl;
    }
    return 0;
}
```
## 循环结构
```python
# Python
# For循环
for i in range(5):
    print(i)

# While循环
while x > 0:
    x -= 1
```

```C++
// C++
#include <iostream>
using namespace std;

int main() {
    // For循环
    for (int i = 0; i < 5; i++) {
        cout << i << endl;
    }

    // While循环
    int x = 5;
    while (x > 0) {
        x--;
    }
    return 0;
}
```

## 常用函数

| 操作         | Python        | C++                |
|--------------|---------------|--------------------|
| 输出         | `print()`     | `cout << `         |
| 输入         | `input()`     | `cin >> `          |
| 字符串长度   | `len()`       | `.length()`或`.size()` |
| 类型转换     | `int("123")`  | `std::stoi("123")` |
| 控制换行     | `\n`          | `endl`             |


## 自定义函数
```Python
# Python
def add(a, b):
    return a + b
```

```C++
// C++
#include <iostream>
using namespace std;

// 显式类型声明
int add(int a, int b) {
    return a + b;
}

// 使用auto推导返回类型 (C++14+)
auto multiply(double a, double b) {
    return a * b;
}

int main() {
    cout << add(3, 4) << endl; // 输出: 7
    cout << multiply(2.5, 4) << endl; // 输出: 10
    return 0;
}
```

## 数组容器
```Python
# Python列表
arr = [1, 2, 3]
arr.append(4)
print(arr[0])  # 访问元素
```

```C++
// C++数组 (固定大小)
#include <iostream>
using namespace std;

int main() {
    // 固定大小数组
    int arr[3] = {1, 2, 3};
    
    // 动态数组 - vector
    #include <vector>
    vector<int> vec = {1, 2, 3};
    vec.push_back(4);  // 添加元素
    
    // 访问元素
    cout << arr[0] << endl; // 输出: 1
    cout << vec[3] << endl; // 输出: 4
    
    // 遍历
    for (int num : vec) {
        cout << num << " "; // 输出: 1 2 3 4
    }
    return 0;
}
```

## 关键差异说明
```C++
​类型系统​：C++需显式声明变量类型，Python动态推断
​大括号​：C++使用{}替代Python缩进
​分号​：C++每条语句结尾需要;
​头文件​：C++功能需要包含头文件（如#include <iostream>）
​命名空间​：常用using namespace std;避免重复写std::
​内存管理​：C++需要手动管理内存（基础阶段可先用vector）
```
