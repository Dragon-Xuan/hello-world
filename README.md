C++作业*（国庆节）
# 2.23
问：给定指针p，你能知道它是否指向了一个合法的对象吗?如果能，叙述判断的思路；如果不能，也请说明原因。
答：应该不能判断指针p是否指向了一个合法的对象，因为如果指针p没有被初始化，p存放的是一个随机的地址，如果p没有被合法的初始化，恶意存放了一个地址，随意访问会很危险的
# 2.24
问：在下面这段代码中为什么p合法而 lp非法？
int i = 42; void *p = &i; long *lp =&i;
答：viod可用于存放任意类型数据的地址；而long只能用于存放long类型的数据。
# 2.25(p53)
问：试说明下列变量的类型和值。
(a)int* p1,i,&r=i ;    p1是指向int类型的对象的指针，其值不确定，i是int类型的变量，r是int类型的引用，r是i的另一个名字
(b)Int i,*ip =0;    i是int型的变量，ip是指向int型的空指针
(c)Int* ip,ip2;     ip是指向int型的指针，其值不确定，ip2是int型的变量
# 2.35（p62）const 对象必须初始化
i是int常量；
j是int变量；
k是i的引用；
p是指向常量的指针；
j2是int常量；
k2是i的引用；

# 验证程序：

const int i = 42;i为常量
auto j = i;//j为整形
j = 0; //j为整型

const auto &k = i; 
// k = 0; //失败，k为整型常量的引用，不可修改

auto *p = &i;
// *p = 0; //失败，p为指向i的整型指针，i不可修改

const auto j2 = i, &k2 = i; 
// j2 = 0; //失败，j2为整型常量，不可修改
// k2 = 0; //失败，k2为、整型常量i的引用, 不可修改

# 3.4（p81）

判断字符串大小： 代码：
'''
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
'''
判断字符串长度代码：
'''
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
'''
# 3.5(p81)

#连接字符串并输出 代码：
'''
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
'''
#空格分隔多字符串： 代码：
'''
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

'''
# 3.20
#代码一：
'''
#include <iostream>
#include <vector>
#include <string>

using namespace std;

int main()
{
    int v1;
    vector<int> ivec;
    while (cin >> v1)
        ivec.push_back(v1);

    for (decltype(ivec.size()) i = 0; i != ivec.size()-1; ++i)
       {
          //for(decltype(ivec.size()) j = i; j!=ivec.size()-1;++j)
          //{
            auto sum = ivec[i] + ivec[i+1];
            cout << sum << " "; 
          //}
       }
       cout << endl;
    return 0;
}
'''
#代码二：
'''
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int main()
{
    int v1;
    vector<int> ivec;
    while (cin >> v1)
        ivec.push_back(v1);

    for (decltype(ivec.size()) i = 0; i != ivec.size(); ++i)
        {
        auto sum = ivec[i] + ivec[ivec.size()-1-i];
        cout << sum << " "; 
        }
        cout << endl;
    return 0;
}
'''
# 3.23（p99）
'''
#include <iostream>
#include <vector>
#include<cctype>
using namespace std;
int main()
{
	vector<int>ivec(10,1);//定义容器ivec
	int ival;
	cout<<"请输入10个整数："<<endl;
	for(vector<int>::iterator iter = ivec.begin();iter<ivec.end();++iter)//使用迭代器访问vector中的元素
	{
	   cout<<(*iter)*2<<endl;
	}
	   if(ivec.size()==0)//如果容器为空，则输入No element! 并退出
	{
	   cout<<"No element!"<<endl;
	   return -1;
	}
	return 0;
}
'''
# 6.20（p188）
'''
void exchange(int *q,int *p)
{
  int t;
  t=*p;
  *p=*q;
  *q=t;
}
int n,m;
cin>>n>>m;
exchange(&n,&m);
cout<<"n="<<n<<"m="<<m;
'''
# 6.19(p193)

(b)合理；
(a)不合理:括号中参数只有一个，而调用时却出现两个数值；
(c)不合理:参数类型为double，而调用时却为整型；
(d)不合理:参数第三项为int，调用时却为浮点型；
6.39（p210）

(a)：第二条声明是为计算两个整型常量。不合法，因为无法和第一条进行区分；
(b)：第二条声明为得到double类型的get()函数。不合法，因为不能使用不同的返回值类型对函数进行重载；
(c)：重置一个double类型的变量。合法。
7.16（p241）

1.在类的定义中对于访问说明符出现的位置和次数没有限定；
2.///
3.定义在public说明符之后-构造函数和一部分成员函数，public成员定义类的接口；
4.定义在private说明符之后的成员可以被类的成员函数访问，但不能被使用该类的代码访问，private部分隐藏类的实现细节。
# 7.27（p249）

代码：
'''
#include <iostream>
#include <string>

using namespace std;

class Screen{
public:
    typedef std::string::size_type pos;
    Screen() = default;
    Screen(pos ht,pos wd, char c) : height(ht),width(wd),contents(ht*wd,c){}
    char get() const
    {
        return contents[cursor];
    }
    inline char get(pos ht, pos wd) const;
    Screen &move(pos r, pos c);
    Screen &set(char);
    Screen &set(pos,pos,char); 
    Screen &display(std::ostream &os)
    {
        do_display(os);
        return *this;
    }
    const Screen &display(std::ostream &os) const
    {
        do_display(os);
        return *this;
    }
private:
    pos cursor = 0;
    pos height = 0, width = 0;
    std::string contents;   

    void do_display(std::ostream &os) const
    {
        os << contents;
    }
}; 

inline Screen& Screen::move(pos r, pos c)
{
    pos row = r * width;
    cursor = row + c;
    return *this;
}

char Screen::get(pos r, pos c) const
{
    pos row = r * width;
    return contents[row + c];
}

inline Screen &Screen::set(char c)
{
    contents[cursor] = c;
    return *this;
}

inline Screen &Screen::set(pos r, pos col, char ch)
{
    contents[r*width + col] = ch;
    return *this;
}

int main()
{
    Screen s1(20,20,'F');
    cout << s1.get(2,3) << endl;

    Screen myScreen(5,5,'X');
    myScreen.move(4,0).set('#').display(cout);
    cout << "\n";
    myScreen.display(cout);
    cout << "\n";  
    return 0;
}
'''
# 7.49（p266）

(a).临时变量作用，调用后，丢弃s的值，i.combine()的结果保存到combine的返回值中；
(b).调用后，s发生改变，i.combine（）结果给返回值；
(c).s是const Sales_data&的，调用后，s值不发生改变,i.combine()的结果给返回值。
# 7.58（p272）
'''
//example.h
class Example{
public:
    static double rate = 6.5;//错误 改正static double rate；
static const int vecSize = 20;
static vector<double> vec(vecSize);//❌-改为static vector<double> vec；

};

//example.C
#include “example.h”
Double Example::rate;//❌-改为Example::rate;
Vector<double> Example::vec;//❌-改为Example::vec;	
'''
在类的内部，rate和vec的初始化是错误的，因为除了静态常量成员之外，其他静态成员不能在类的内部初始化。另外，example.c文件的两条语句也是错误的，在这里必须给出静态成员的初始值
