# 结构体

## 1.什么是结构体
什么是结构体: 结构体是用户自定义的允许存储不同类型数据项的数据结构。(数组允许存储相同类型数据项的变量)。<br\>
例子:如果要存储一位同学的学号、姓名、身高、年龄、家庭地址信息，由于这些信息是不同的变量类型，不适合定义数组来存储，就可以定义结构体来存储。<br\>
使用起来相当简单，唯一要记住的就是”->“的使用场景即可。

### 1.1 结构体的定义和使用
```C++
#include <iostream>
#include <string>
using namespace std;

/*定义结构体*/
struct Student{
    // 成员
    int num;
    string name;
    double height;
};

/*定义一个函数，专门用来输出结构体变量数组*/
void print(Student a[],int n){
    for(int i=0;i < n; i++){
        cout << a[i].num << a[i].name << a[i].height << endl;
    }
}

int main(){
   Student a[100];
    int i,n;
    cin >> n;
    for(int i=0;i < n ;i++){
        cin >> a[i].num >> a[i].name >> a[i].height;
    }
    //调用函数，输出结构体数组中每个结构体的成员
    print(a,n);
	return 0;
}
```

### 1.2 结构体指针的使用
```C++
#include <iostream>
#include <string>
using namespace std;

/*定义结构体*/
struct Student{
    // 成员
    int num;
    string name;
    double height;
};

int main(){
    Student s;  // 定义结构体变量
    s.num = 1;
    s.name = "wang";
    s.height = 174.0;
    // s是结构体类型，因此使用成员变量：结构体名.成员名
    cout << s.num << " " << s.name << " " << s.height << endl;

    Student *p = &s;    //定义结构体指针
    // 定义结构体指针后(p是指针类型),使用成员变量:结构体指针->成员名
    cout << p->num << " " << p->name <<" "<< p->height << endl;
    // p是指针*p就又是取值，取到结构体了
    cout << (*p).num << " " << (*p).name << " " << (*p).height << endl;
    
	return 0;
}
```

## 1.3 实际例题
感受一提即可，有前面的编程思想做铺垫，会发现结构体是很好理解和使用的。
场景：期末考试排名:
```C++
#include <bits/stdc++.h>
using namespace std;

// 降序成级 
struct Student{
	int num;	// 编号 
	string name;	// 名字 
	int score;	// 成绩 
};
int main(){
	Student a[110];
	int n;	// 总共有几个学生 
	cin >> n;
	for(int i=0;i<n;i++){
		cin >> a[i].num >> a[i].name >> a[i].score;
	}
	
	// 冒泡算法
	for(int i=0;i<n-1;i++){
		for(int j=0;j<=n-i-1;j++){
			if(a[j].score < a[j+1].score){
				swap(a[j] , a[j+1]);
			}
		}
	}
	
	// 输出
	for(int i=0;i<n;i++){
		cout << a[i].num <<' '<< a[i].name <<' '<< a[i].score <<endl;
	} 
	 
	return 0;
}
```

上面还有需要考虑排序算法的思考成本，如果题目中要求必须手动写排序算法，可以用sort排序，简单明了：
```c++
#include <bits/stdc++.h>
using namespace std;

// 降序成级 
struct Student{
	int num;	// 编号 
	string name;	// 名字 
	int score;	// 成绩 
};

bool cmp(Student s1,Student s2){
	if(s1.score > s2.score){
		return true;
	}else{
		return false;
	}
}
int main(){
	Student a[110];
	int n;	// 总共有几个学生 
	cin >> n;
	for(int i=0;i<n;i++){
		cin >> a[i].num >> a[i].name >> a[i].score;
	}
	
	// sort排序 
	sort(a,a+n,cmp);
	
	// 输出
	for(int i=0;i<n;i++){
		cout << a[i].num <<' '<< a[i].name <<' '<< a[i].score <<endl;
	} 
	 
	return 0;
}
```