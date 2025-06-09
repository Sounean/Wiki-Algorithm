# 2.字符串详解

<warning>其中字符串的常用函数需要花时间记忆</warning>

## 一、字符串基础知识
1.是什么是string?<br/> 
答:string是C++的STL(Standard Template Library 即标准模板库)提供的字符串类，用于`处理字符串相关`的问题。<br/>

2.string和char s[]区别? <br/>
答:(1)字符数组本质上还是数组，因此长度固定;string可以理解为长度不限的字符;<br/>
(2)字符数组的系统定义的函数过少,导致操作不方便;string 集成大量的系统函数,方便操作;<br/>
(3)字符数组由于本质是数组，因此不能进行比较运算以及+运算;string可以直接做比较和+运算;<br/>

## 二、string基础知识
(1)getline(cin,s):读入一个字符串(直到换行)，可以含空格；<br/>
(2)cin:读入一个字符串，不能含空格;<br/>
<warning>注:如果用while循环，如while(cin >> s)的话，必须得用ctrl+z或者ctrl+d来停止循环。</warning>

(3)s.size():求字符串s的长度; <br/>
(4)s[下标i]:获取字符串的某个下标对应的字符;<br/>
(5)掌握 string 的+的用法，注意string使用下标常见的错误:<br/>
仅定义string s1;的话，s1是一个长度为0的字符串！！s1[0],s1[1]都会报错;<br/>
(6)定义并初始化string类型后，该变量的某一位都是char类型;<br/>
(7)题目中让进行字符的大小比较，其实就是比较字符的ASC2码表的编号大小

## 三、字符串的常见函数
查找和截取：<br/>
字符串.find(子串):查找子字符串第一次出现的下标，没有返回string::npos(注意判断其为一1);<br/>
字符串.find(子串，x):在字符串的下标x之后，查找子串出现的位子;<br/>
字符串.substr(开始位置i，子串长度len):截取子字符串，当len>字符串长度的时候，只取剩余的;<br/>
子字串.substr(开始位置i):截取子字符串，从下标为i开始截取到最后;<br/>

删除、插入和替换：<br/>
erase(开始下标i，删除长度len):删除字符串第i个下标开始的 len 个字符;<br/>
erase(开始下标i):删除字符串第i个下标开始往后的所有字符;<br/>
insert(插入下标，插入字符串s):在字符串下标为i的位置插入一个字符串s;<br/>
replace(i,len,str):从下标为i开始，替换len 个字符为 str;<br/>

判断/转换:<br/>
字符类型判断函数:(非string函数)<br/>
isalpha(c):判断c是否为字母<br/>
isdigit(c):判断是否为数字<br/>
islowcr(c):判断是否为小写<br/>
isupper(c):判断是否为大写<br/>
说明：返回非0表示真，返回0表示假；<br/>

字符类型转换函数:(非string函数)<br/>
tolower():字符转小写<br/>
toupper(c):字符转大写<br/>
说明：返回int;<br/>

字符类型转换函数:(非string函数)<br/>
tolower(c):字符转小写<br/>
toupper(c):字符转大写<br/>
说明：返回int;<br/>

排序和倒序函数:(非string函数)<br/>
sort(起始地址,结束地址+1):数组升序排序<br/>
reverse(起始地址,结束地址+1):数组逆序<br/>

获取头尾指针:<br/>
s.begin():获取字符串s的头位置(指针)<br/>
s.end():获取字符串s的尾位置(最后一个字符后面的位置)(指针)<br/>

类型转换函数:<br/>
stoi(s):将字符串s转换为对应的整数<br/>
stoll(s):将字符串s转换为对应的long long<br/>
stof(s):将字符串s转换为对应的float<br/>
to_string(int n):将整数n转换为字符串<br/>
to_string(double a):将 double 型的a转为字符串，转换成的字符串小数点后有

# 四、字符串常见错误
假设有那么一个场景：我先输入一个整数n，然后再输入n个字符串，我如下述代码去写，会有问题：
```C++
#include <string>
#include <iostream>
using namespace std;
int main(){
    int n = 0;
    string str = "";
    cin >> n;
    for (int i = 0; i < n; ++i) {
        getline(cin,str);
    }
    return 0;
}
```
假设我n输入的是4,然后会发现，再往下只能再输入4-1,即3行，程序就结束了。再怎么debug发现都只能输入3行，这是因为:
```C++
1.用户首先使用 cin >> n; 读取整数n4。
2.然后进入循环，循环n次（即4次），每次循环中getline(cin,str);读取字符串
```
问题可能在于：在读取n之后，输入缓冲区中残留了一个换行符（用户输入4后按下的回车键）。当第一次调用getline时，它读取到的是这个换行符，因此得到一个空行，
然后紧接着的第二个getline读取第一行实际内容，这样循环两次，实际上只读取了3行输入（包括第一次的空行和后续3行），而不是预期的4行。

即，当混合使用cin>>和getline时，cin>>会留下换行符在缓冲区，而getline会立即读取到这个换行符，导致读取空行。

解决方案：在cin>>n之后，使用cin.ignore()清除缓冲区中的换行符，然后后面的getline就能正常读取下一行。
```C++
#include <string>
#include <iostream>
using namespace std;
int main(){
    int n = 0;
    string str = "";
    cin >> n;
    cin.ignore();
    for (int i = 0; i < n; ++i) {
        getline(cin,str);
    }
    return 0;
}
```





