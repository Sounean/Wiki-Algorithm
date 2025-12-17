# 素数和合数

## 定义

素数:又称质数，是指在大于1的自然数中，除了1和它本身以外不再有其他因数<br/>
合数：除了1和它本身，还有其他正因数的大于1的正整数<br/>
规定：1既不是素数也不是合数<br/>

不要看素数和合数的定义好像刚好相反，就推断自然数(自然中用来数数的，非负整数)中除了素数就是合数。准确的说法是自然数除了素数和合数还有1和0.<br/>
然后一句经典的来了“合数都是由质数相乘得来的”.<br/>
这句话粗看是一句废话，合数本身的定义就是说是要除了1和自身还得要有其他公因数，那不就等价这句话了么。<br/>
但其实不是废话，而是一个重要的数学定理：`虽然合数的定义确实包含"有除了1和自身以外的因数"这一性质，但"合数都是由质数相乘而来的"这句话实际上表达了一个更深刻、更精确的数学结论：任何一个大于1的整数，要么是质数，要么可以唯一地分解为质因数的乘积（不考虑顺序）。`<br/>
这个定理的价值在于：<br/>
唯一性：质因数分解是唯一的（除了因数的排列顺序不同）<br/>
构造性：给出了合数的具体构造方式<br/>
应用性：是数论、密码学等领域的基础<br/>
所以这句话不是简单的同义反复，而是揭示了自然数内在的深刻结构。

![df9ada7bd4294aa0a629ed6ab8c0228e.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMySBpQmxAcTdaUxygsA1JP9yYW_HhSwACLSkAAljPEVaJRoMgXwEV_zYE.png)

## 经典例题:找素数

![588395e887974950bd03b685f6267fb0.png](https://img.remit.ee/api/file/BQACAgUAAyEGAASHRsPbAAEMyUJpQmy0kEt_mgvFpZQAAaPYp-Uh4KsAAlIpAAJYzxFWz-jfeyke9c42BA.png)

## 找素数：解法1：暴力解法

直接遍历2 — n的范围的数判断是否满足除了一和它本身外没有数能整除
```C++
//判断是否为质数 
bool Prime_number(int n){
	for(int j=2;j<i;j++){
		if(i%j==0) return false;//有其他因数返回假 
	} 
	return true;
}
 
//统计范围素数个数
int find_number_Prime(int n,int m){ //n和m的为范围 n>=2 m<10e9
	//暴力解法
	int num=0;//统计个数 
	for(int i=n;i<=m;i++){
		//判断是否为质数
		if(Prime_number(i)) num++;
		
	} 
	return num;
}
```
开始优化：由于除2外的偶数都不是质数，所以我们可以排除偶数，只计算奇数    ---> 因为这样肯定也包含了一个2，已经满足成为合数了<br/>
而且当 数>num/2 时  相除的结果为1.几，为小数，可以不用判断这部分因数   --->一个数的因子不可能同时大于num/2<br/>
所有有两个优化的空间<br/>
(实际上第二点应该是到num的算术平方根即可，不会有因为同时大于这个值)
```C++
//判断是否为质数 
bool Prime_number(int n){
	for(int j=2;j<i/2;j++){ //优化1：因数判断的范围 
		if(i%j==0) return false; 
	} 
	return true;
}
//统计范围素数个数
int find_number_Prime(int n,int m){ //n和m的为范围 n>=2 m<10e9
	//暴力解法
	int num=0;//统计个数 
	int n1=n;
	if(n1==2){ //特殊处理2这个值 
		num++;n1++;
	} 
	for(int i=n1;i<=m;i+=2){ //优化2使用奇数进行判断 
		//判断是否为质数
		if(Prime_number(i)) num++;
	} 
	return num;
}
```


## 找素数：解法2：埃氏筛法
将已经筛选出的质数的倍数全部剔除，即可留下质数<br/>
由于合数都是其小于本身的质数倍数<br/>
当判断到质数是，将（范围内）的倍数都可以排除掉<br/>
需要创建一个 bool 类型数组 判断它是否被剔除<br/>
埃氏筛法模板：<br/>
```C++
//埃氏筛法模板
const int num=10001;
int data[num]={};//数组存储数据
bool N[num]={false};//用来标记是不是素数 
int k=0;//用来存储素数的位置 
void find_prime_number1(int n)
{
	N[1]=true;//1不是素数
	for(int i=2;i<=n;i++)
	{
		if(!N[i]){
            data[++k]=i;//是素数 存储数据
		    for(int j=2*i;j<=N;j+=i) N[i]=true;//把i的倍数都剔除
		} 
	} 
} 
//时间复杂度：0(nlogn)   空间复杂度 O(N)
```

埃氏筛法解题:<br/>
```C++
//埃氏筛法 统计素数个数 
int find_number_Prime(int n,int m){
	int num=0;//统计个数 
	bool  b[m+10]={false};//判断是否被剔除
    b[0]=b[1]=true;//0 1 不是素数
	//从2开始剔除 
	for(int i=2;i<=m;i++){
        if(!b[i]){
	        for(int j=2*i;j<=m;j+=i)b[j]=true;//将倍数剔除 
        }
	} 
	//剔除完后统计个数
	for(int i=n;i<=m;i++){
		if(!b[i]) num++;
	} 
	return num;
}
```



