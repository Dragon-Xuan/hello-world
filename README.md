C++作业*（国庆节）
#2.23（p51）

答：若指针拥有一个合法值，则能将它用在条件表达式中。使用非法指针作为条件或者参与比较都会报错。
#2.24

答：viod可用于存放任意类型数据的地址；而long只能用于存放long类型的数据。
#2.25(p53)

a).ip为int类型的指针，i为int类型，r为指针i的引用；
b).i为int类型，ip为int类型指针；
c).ip为int类型指针，ip2为int类型。
#2.35（p62）const 对象必须初始化

整型常量-i、j2；整型常量引用-k、k2；整型-j；整型指针-p；

#验证程序：

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

#3.4（p81）

判断字符串大小： 代码：

#include <iostream>
#include <string>

using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
    string a, b;
    cout << "请输入a和b的值:" << endl;
    while(cin >> s1 >> s2)
    {
    if (s1==s2)
      cout << "a与b相等!" << endl;
    else if(a > b)
      cout << "字符串a比b长 ": << a << endl;
    else 
      cout << "字符串a比b短": << b << endl;
    }
    return 0;
 }

判断字符串等长：

代码：

#include <iostream>
#include <string>

using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
    string s1, s2;
    while (cin >> s1 >> s2)
    {
        if (s1.size() == s2.size())
        cout << "s1与s2等长"<<endl;
        cout << "是 "<<endl;
        else if(s1.size() > s2.size())
        cout << "s1要长 : " << s1 << endl;
        else 
        cout << "s2要长 : " << s2 << endl;
    }
    return 0;
}

#3.5(p81)

#连接字符串并输出 代码：

#include <iostream>

using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
    string s1, s2，s;
    s=s1;
    while (cin >> s2)
    {
        s += s2;
    }
    cout << s << endl;
    return 0;
}

#空格分隔多字符串： 代码：

#include <iostream>
#include <string>

using std::string;
using std::cin;
using std::cout;
using std::endl;

int main()
{
    string s1, s2;
    while (cin >> s2)
    s1 +=  " " + s2;
    cout << s1 << endl;
    return 0;
 } 

3.20（p94）

#代码一：

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

#代码二：

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

#3.23（p99）

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

#6.20（p188）

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

6.19(p193)

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
7.27（p249）

代码：

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

7.49（p266）

(a).临时变量作用，调用后，丢弃s的值，i.combine()的结果保存到combine的返回值中；
(b).调用后，s发生改变，i.combine（）结果给返回值；
(c).s是const Sales_data&的，调用后，s值不发生改变,i.combine()的结果给返回值。
7.58（p272）

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
