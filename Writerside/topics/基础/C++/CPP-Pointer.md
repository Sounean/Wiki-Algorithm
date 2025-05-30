# 指针

## 1. 什么是指针
指针(Pointer):`变量的地址`，通过它能找到以它为地址的内存单元;<br/>
我们只需要能区分1.什么是地址(指针)，2.什么是地址指向的值， 就能应对所有指针相关的知识点。

### 1.1 如何通过指针修改变量的值
```C++
#include <iostream>
using namespace std;
int main(){
    //整数变量
    int x=10;
    //定义指针(整数指针)，指向x的地址
    // p是int*类型(整数指针类型)
    //&表示取变量的地址
    int *p=&x;
    cout<<p<<endl;
    //p是地址，*p不是，*p表示p指向的地址对应的值
    cout<<*p<<endl;

    //通过指针，修改变量的值
    // p指向的值，自增2
    *p= *p + 2;//相当于 x=x+2
    cout<<x<<endl;
    cout<<p<<""<<*p<<endl;
    
    return 0;
}

输出结果:
0x8f515ff844
10
12
0x8f515ff84412
```

为什么用int *p,而不是int* p?<br/>
首先，用int* p的这种写法的也有，Google C++ 风格指南推荐使用 `int* p` 这种写法，其他编程规范则可能更推荐`int *p`的写法；<br/>
其次，在C++中，int *p 和 int* p 的写法都是合法的，且语义相同，都表示 p 是一个指向 int 类型的指针，所以不是说不用int* p是因为这个写法有问题.<br/>

那为什么更推荐用int *p,因为有如下场景:
```C++
int *p, q;  // p 是指针，q 是普通 int 变量
```
如果写成int* p的话，就是int* p,q；会让第一直觉是认为p和q均为指向int型变量的指针类型，那就大错特错了。<br/>

### 1.2 指针和普通变量的不同
```C++
#include <iostream>
using namespace std;
int main(){
    int x=10;
    //值拷贝，将x的值拷贝给了y
    int y = x;
    y = y + 2;
    cout<<x<<endl;

    //将x的地址拷贝给p
    int *p = &x;
    *p = *p + 2;
    cout<<x<<endl;
    
    return 0;
}

输出结果:
10
12
```
通过以上了解拷贝值和拷贝地址的区别.

### 1.3 &和*的嵌套使用
这一小节能熟练，看到代码自己能推出来值，那就说明地址和值这块儿没毛病了,也是以后工作编程中最最常用的一个小节.
```C++
#include <iostream>
using namespace std;
int main(){
    int x = 10;
    int *p = &x;
    cout<<p<<endl;
    cout<<*p<<endl;
    cout<<&(*p)<<endl;
    cout<<*&(*p)<<endl;
    
    return 0;
}

输出结果:
0x84815ffda4
10
0x84815ffda4
10
```

### 1.4 *p++和(*p)++的区别

## 2. 指针作用


## 3.数组指针
一句话：数组就是指针

