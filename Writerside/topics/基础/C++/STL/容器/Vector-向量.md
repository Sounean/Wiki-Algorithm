# Vector(向量)

## 1.什么是向量
向量(vector)是一个顺序容器(Sequence Container)，它能够存放各种类型的对象。
可以简单的认为，向量是一个能够存放任意类型的动态数组(元素个数可变)。

思考： 数组能用的他都能用，数组不能用的，像数组的大小一开始就要被确定，向量能改边，这表示向量能随意增加删除元素，完全不用顾虑。
这么一看完全比数组好啊？数组还不能动态，他能动态，那还要数组干啥？<br/>
原因：因为性能考虑：虽然vector提供了更多的功能，但由于需要处理动态内存分配和大小调整的问题，可能会带来一些额外的开销。然而，在大多数应用场景下，这种差异是可以忽略不计的。

那什么时候用数组什么时候用向量？<br/>
选择数组还是vector取决于具体的需求。如果你知道数据集的大小不会变化，并且希望获得最佳性能，可以选择数组。相反，如果你需要一个能够根据需要增长或缩小的数据结构，
或者想要利用STL提供的丰富功能，那么vector将是更好的选择。在现代C++编程实践中，除非有特定的理由要使用内置数组，否则推荐使用vector或其他标准库容器，
因为它们提供了更好的灵活性和安全性。

## 2.vector的常见函数
函数名	描述<br/>
size()	返回vector中元素的数量。<br/>
empty()	判断vector是否为空（无元素），返回布尔值。<br/>
swap() 交换两个同类型向量的数据.<br/>

push_back(元素)	在vector的末尾添加一个元素。<br/>
insert(pos, val)	在指定位置pos插入一个值为val的新元素。<br/>

pop_back()	移除vector末尾的一个元素。<br/>
erase(pos)	移除位于pos位置的单个元素或范围内的元素。<br/>
clear()	清空vector中的所有元素，使其变为空,size()变成0。<br/>

at(index)	访问vector中指定位置的元素，并提供边界检查（如果索引越界会抛出异常）。<br/>
向量.[i] 取向量下标为i的元素<br/>
front()	返回取向量第一个元素。<br/>
back()	返回取向量最后一个元素。<br/>

begin()	返回指向vector首元素的迭代器。<br/>
rbegin() 反向迭代器，指向最后一个元素.<br/>
end()	返回指向vector末尾之后位置的迭代器。<br/>
resize(new_size)	改变vector的大小到new_size，如果新的大小更大，则用默认值填充新位置；如果更小，则截断多余的元素。<br/>

对应于数组，要注意:向量的大小是可变的，开始时向量为空，随着不断插入元素，向量自动申请空间，容量变大。<br/>
注意学会使用:sort()、reverse()等函数对vector进行排序、逆序等操作

## 3.常见的原始实例

### 3.1. vector的存储和遍历
根据不同的使用场景，有4种vector的常见方法：<br/>
(1)vector():创建一个空 vector<br/>
(2)vector(n):创建一个元素个数为n的 vector<br/>
(3)vector(n,t):创建一个元素个数为n且值为t的 vector<br/>
(4)vector(begin,end):复制[begin,end)区间内另一个数组的元素到 vector中

```C++
#include <bits/stdc++.h>
using namespace std;

void print(vector<int> v){
	// 遍历vector中的元素
	for(int i=0;i<v.size();i++){
		cout << v[i] << endl;
	} 
	cout << endl;
}

int main(){
	// 定义方法1：定义vector存储int类型的变量
	vector<int> v;
	
	cout << v.size() << endl;
	/*
	// 注意：常见错误，vector<int>v定义一个空vector，不可以用下标0和1来访问元素 
		v[0] = 10;
		v[1] = 20;
	*/
	cout << v.size() <<	endl; 
	// 添加元素进vector 
	v.push_back(10);
	v.push_back(20);
	v.push_back(30);
	cout << v.size() << endl; 
	print(v);
	
	// 定义方法2:定义一个长度为5的vector，默认值为0
	vector<int> v2(5);
	// 定义方法3:义一个长度为5的vector，默认值为80
	vector<int> v3(5,80); 
	int a[] = {10,20,30,40,50};
	// 定义方法4:使用数组初始化vector
//	sizeof();	// 计算变量占用字节数
	sizeof(a)/sizeof(int);	// 计算数组实际长度
	cout <<  sizeof(a)/sizeof(int)  << endl;
	vector<int> v4(a,a+sizeof(a)/sizeof(int));
	v4.push_back(10);
	print(v);
	 
	return 0;
}
```



