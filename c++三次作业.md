# c++三次作业，在三个分支中
# c++第一次作业
练习2.23：给定指针p，你能知道它是否指向了一个合法的对象吗?如果能，叙述判断的思路；如果不能，也请说明原因。  

应该不能判断指针p是否指向了一个合法的对象，因为如果指针p没有被初始化，p存放的是一个随机的地址，这是一件极其危险的事情，再者，如果p没有被合法的初始化，恶意存放了一个地址，也是危险的。所以，需要程序员自己清楚指针是否被合法使用。

 

练习2.24 在下面这段代码中为什么p合法而 lp非法？  

int i = 42; void *p = &i; long *lp =&i;  

void *是一种特殊的指针类型，可以用于存放任意对象的地址。第三个两者类型不一，当然报错，和赋值不一样，指针要求两边类型严格一致  


练习 2.25:试说明下列变量的类型和值。  
(a)int* p1,i,&r=i ;    p1是指向int类型的对象的指针，其值不确定，i是int类型的变量，r是int类型的引用，r是i的另一个名字  
(b)Int i,*ip =0;    i是int型的变量，ip是指向int型的空指针  
(c)Int* ip,ip2;     ip是指向int型的指针，其值不确定，ip2是int型的变量  


练习2.35  

i是int常量；  
j是int变量；  
k是i的引用；  
p是指向常量的指针；  
j2是int常量；  
k2是i的引用；  

3.4
```
#include "pch.h"
#include <iostream>
#include <string>
using std::string;
using std:: cin;
using std:: cout;
using std::endl;
int main()
{
	string s1;
	string s2;
	cout << "please input a string"<<endl;
	cin >> s1;
	//cout << endl;
	cout << "please input another string"<<endl;
	cin >> s2;
	if (s1 == s2)
		cout << "they are same";
	else
		cout << "they are diffierent";


	return 0;
}
```
```
#include "pch.h"
#include <iostream>
#include <string>
using std::string;
using std:: cin;
using std:: cout;
using std::endl;
int main()
{
	string s1;
	string s2;
	
	cout << "please input a string"<<endl;
	cin >> s1;
	auto len1 = s1.size();
	//cout << endl;
	cout << "please input another string"<<endl;
	cin >> s2;
	auto len2 = s2.size();
	if (len1 == len2)
		cout << "等长"<<endl<<"长度是："<<len1;
	else
	{
		cout << "不等长"<<endl;
		if (len1 < len2)
			len1 = len2;
		cout << "较长的长度是：" << s1;
	}


	return 0;
}
```
3.5
```
#include<iostream>
#include<string>
 
using namespace std;
 
 
int main()
{
    string tmpString,longString;
 
    cout << "请输入多个字符串：" << endl;
    if( cin >> longString )  //读入第一个字符串
    {
        while( cin >> tmpString )
            longString += tmpString;
        cout << "连接而成的大字符串：" << longString << endl;
    }
 
    else
    {
        cout << "输入有误" << endl;
        return -1;
    }
    return 0;
}
```
```
#include<iostream>
#include<string>
 
using namespace std;
 
 
int main()
{
    string tmpString,longString;
 
    cout << "请输入多个字符串：" << endl;
    if( cin >> longString )  //读入第一个字符串
    {
        while( cin >> tmpString )
        {
            longString += " ";
            longString += tmpString;
        }
        cout << "连接而成的大字符串：" << longString << endl;
    }
 
    else
    {
        cout << "输入有误" << endl;
        return -1;
    }
    return 0;
}
```
3.20
```
#include<iostream>
#include<vector>
 
using namespace std;
 
int main()
{
    cout << "请输入一组整数：" << endl;
 
    vector<int> ivec;
    int ival = 0;
    decltype ( ivec.size() ) len = 0;
 
    while( cin >> ival )
        ivec.push_back( ival );
    len = ivec.size();
 
    cout << "容器的数据为：" << endl;
    for( const auto &i : ivec )
        cout << i << " ";
    cout << endl;
 
    cout << "每对相邻整数的和为：" << endl;
    for( decltype( len ) i = 0; i != len - 1; ++i )
        cout << ivec[ i ] + ivec[ i + 1 ] << " ";
    cout << endl;
 
    cout << "相对元素的和(比如第3和倒数第三个元素的和)为：" << endl;
 
    for( decltype( len ) i = 0; i <= len - 1; ++i, --len )
        cout << ivec[ i ] + ivec[ len -1 ] << " ";
    cout << endl;
 
    return 0;
}
```

3.23
```
#include<iostream>
#include<vector>
#include<ctime>
#include<cstdlib>


using namespace std;

int main()
{
vector<int> ivec( 10 );
srand( ( unsigned ) time( NULL ) );
for( auto &i : ivec )
i = rand() % 1000;
cout << "随机生成的10个数是：" << endl;
for( auto it = ivec.begin(); it != ivec.end(); ++it )
cout << *it << " ";
cout << endl;

cout << "利用迭代器对每个数加倍后的输出：" << endl;
for( auto it = ivec.begin(); it != ivec.end(); ++it )
{
*it = *it * 2;
cout << *it << " ";
}
cout << endl;

return 0;
}
```
6.10
```
#include "pch.h"
#include <iostream>
#include <string>
using std::string;
using std:: cin;
using std:: cout;
using std::endl;
void change(int*a, int*b)
{
	int *c;
	c = a;
	a = b;
	b = c;
	cout << *a <<" "<< *b;
	
}
int main()
{
	int m,n;
	cin >> m>>n;
	change(&m, &n);
	return 0;
}
```
6.19  
(a)：函数只有一个参数，传入两个不合法  
(b)：合法  
(c)：合法  
(d)：合法  

6.39  
(a)   
第二条是计算两个常量整型的数。  
不合法，第二条无法和第一条进行区分。  
(b)  
获得double类型的get()  
不合法，不能使用不同的返回值类型对函数进行重载。  
(c)   
重置一个double类型的数。  
合法。  
  

7.16  
在类的定义中，可以包含0个或者多个访问说明符，并且对于某个访问说明符能出现多少次以及可能出现在哪里都没有严格规定。每个访问说明符指定接下来的成员的访问级别，有效范围直到出现下一个访问说明符或者到达类的结尾为止。  

一般来说，作为接口的一部分，构造函数和一部分成员函数应该定义在public说明符之后，而数据成员作为实现部分的函数则应该跟在private说明符之后。  

7.27  
```
class Screen
{
private:
	unsigned height = 0, width = 0;
	unsigned cursor = 0;
	string contents;
public:
	Screen() = default;
	Screen(unsigned ht, unsigned wd) : height(ht), width(wd), contents(ht * wd, ' ') { }
	Screen(unsigned ht, unsigned wd, char c) : height(ht), width(wd), contents(ht * wd, c) { }
 
public:
	Screen& move(unsigned r, unsigned c)
	{
		cursor = r * width + c;
		return *this;
	}
 
	Screen& set(char ch)
	{
		contents[cursor] = ch;
		return *this;
	}
 
	Screen& set(unsigned r, unsigned c, char c)
	{
		contents[r * width + c] = ch;
		return *this;
	}
 
	Screen& display()
	{
		cout << contents;
		return *this;
	}
};
```
练习7.49：对于combine函数的三种不同声明，当我们调用i.combine(s)时分别发生什么情况？其中i是一个Sales_data，而s是一个string对象？  

(a) Sales_data &combine(Sales_data);  

(b)Sales_data &combine(Sales_data&);  

(c)Sales_data &combine(const Sales_data&) const;  

第一个正确，编译器首先用给定的string对象s自动创建一个Sales_data对象，然后这个新生成的临时对象传给combine的形参，函数正确执行并返回结果。  

第二个错误。无法编译通过，因为combine函数的参数是一个非常量引用，而s是一个string对象，编译器用s自动创建一个Sales_data临时对象，但是这个新生成的临时对象无法传递给combine所需的非常量引用。  

第三个错误，无法编译通过，因为把combine声明成了常量成员函数，所以该函数无法修改数据成员的值。  

7.58  
在类的内部，rate和vec的初始化是错误的，因为除了静态常量成员之外，其他静态成员不能在类的内部初始化。另外，example.c文件的两条语句也是错误的，在这里必须给出静态成员的初始值  
