# 易错点

## 赋值上
一个常量
```C++
#include "iostream"
using namespace std;
// 若需定义常量，推荐const int maxn = 999; 这是预处理指令，在编译前进行文本替换代码中所有maxn会被直接替换为999
// 且要注意后面不能带";"，不然环境会将"999;"视作一个整体而报错
#define maxn 999
int add1[maxn];
int main(){

    return 0;
}
```

二维数组赋值
```C++
int currentPoint[2] = {0,0};    //只能在定义时用初始化列表，不能在后续赋值阶段使用这种语法
// 后面想对currentPoint赋值，得:
currentPoint[0] = i;  // 第一个元素赋值
currentPoint[1] = j;  // 第二个元素赋值