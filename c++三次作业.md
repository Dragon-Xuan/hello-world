# c++三次作业
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
# C++ 第二次作业

# 301.9.11  
1.vector <int> text;   
vector 为空，size为0，容器内没有元素   
2.vector <int> text(text1);  
  vector  <int> text = text1;  
两种方式等价，text初始化为text1的拷贝，两者类型必须相同，两者具有相同的容量和元素  
3.vector <int> text{1,2,3};  
  vector <int> text={1,2,3};  
两者等价，text初始化为初始化列表中的元素拷贝，列表中的元素类型必须与vector的元素类型相同  
4. vector <int> text(tx.begin(),tx.end());
  text初始化为迭代器tx.begin(),tx.end()指定范围内的元素的拷贝，范围内的元素类型要与vector类型相同  
5.vector <int> text(7);  
  text中包含7个元素，每个元素进行缺省的值初始化，即为0
6.vector <int> text(7,1);
 text中包含7个被初始化为1的元素  
# 309.9.20  
编写程序，从一个list<int>拷贝元素到两个deque中。值为偶数的所有元素都拷贝到一个deque中，而基数值元素拷贝到另一个deque中。
```
#include <iostream>
#include <vector>
#include <list>
#include <deque>
int banduan(int);
using namespace std;
int main()
{
	list <int> list1;
	deque <int> deque1;
	deque <int> deque2;
	list <int>:: iterator i;
	deque <int>::iterator j1, j2;
	int j;
	list1 = { 1,2,3,4,5 };
	cout << "list1 = { 1,2,3,4,5 }" << endl;
	for (i = list1.begin(); i != list1.end(); i++)
	{
		if (banduan(*i))
			deque1.push_back(*i);
		else
			deque2.push_back(*i);
	}
	cout << "deque1:" << endl;
	for (j1 = deque1.begin(); j1 != deque1.end(); j1++)
	{
		cout << *j1 << endl;
	}
	cout << "deque2:" << endl;
	for (j2 = deque2.begin(); j2 != deque2.end(); j2++)
	{
		cout << *j2 << endl;
	}
	return 0;
}
int banduan(int i)
{
	if (i % 2)
		return 1;
	else
		return 0;
}
```
# 315.9.29
假定vec包含25个元素，那么vec.resize(100)会做什么？，如果接下来调用vec.resize（10）会做什么？   
(1)会将75个值为0的int添加到vec的末尾。(2)从vec末尾删除90个元素。  

# 324.9.43
(1)会将75个值为0的int添加到vec的末尾。(2)从vec末尾删除90个元素。
编写一个函数，接受三个string参数s、oldVal和newVal。使用迭代器及insert和erase函数将s中所有的oldVal替换为newVal 。测试你的程序，用它替换通用的简写形式，如将"tho"替换为"though"，将"thru"替换为"through"。  
~~~
#include<iostream>
#include<string>
 
using namespace std;
 
void StrReplace( string&, const string&, const string& );
 
int main()
{
    const string oldV( "tho" );
    const string newV( "though");
    string str( "i love you tho i cant hold you" );
    string str2( "tho thru through");
 
    StrReplace( str, oldV, newV );
    cout << str << endl;
    StrReplace( str2, "thru", "" );
    cout << str2 << endl;
    return 0;
}
 
 
 
//题目要求用迭代器、及insert和erase函数完成操作
void StrReplace( string &s, const string &oldVal, const string &newVal )
{
    auto oldLen = oldVal.size();
    auto newLen = newVal.size();
    auto iter = s.begin();
 
    if( oldLen == 0 )  //如果要替换的字符串为空，则什么也不做。
        return;
    
    while( iter <= ( s.end() - oldLen ) ){
        if( *iter == oldVal[0] ){
            string tmp( iter, iter + oldLen );  //创建s中以oldVal首字母开头的oldLen长度的临时字符串。
            if( tmp == oldVal ){ //若s中有与oldVal相同的子字符串
                iter = s.erase( iter, iter + oldLen );
                for( auto it = newVal.rbegin(); it != newVal.rend(); ++it ) //根据插入的方式，应该用反向迭代器插入
                    iter = s.insert( iter, *it );
                iter += newLen;
            }
            else
                ++iter;
 
        }
        else
            ++iter;
    }
 
 
}
 
~~~
练习9.52:使用stack处理括号化的表达式。当你看到一个左括号，将其记录下来，当你在一个左括号之后看到一个右括号，从stack中pop对象，直至遇到左括号，将左括号也一起弹出栈。然后将一个值（括号内的运算结果）push到栈中，表示一个括号化的（子）表达式已经处理完毕，被其运算结果所替代。
~~~
#include<iostream>
#include<stack>
#include<string>
#include<stdexcept>
 
using namespace std;
 
enum obj_type{ LP, RP, ADD, SUB, VAL };
struct obj{
    obj( obj_type type, double val = 0 ) { t = type; v = val; }
    obj_type t;
    double v;
};
 
inline void skipws( string &exp, size_t &p )
{
    p = exp.find_first_not_of( " ", p );
}
inline void new_val( stack<obj> &so, double v )
{
    if( so.empty() || so.top().t == LP ) {
        so.push( obj( VAL, v ) );
    }
    else if( so.top().t == ADD || so.top().t == SUB ){
        obj_type type = so.top().t;
        so.pop();
        if( type == ADD )
            v += so.top().v;
        else
            v = so.top().v - v;
        so.pop();
        so.push( obj( VAL, v ) );
    }
    else
        throw invalid_argument( "缺少运算符" );
}
 
 
int main()
{
    stack<obj> so;
    string exp;
    size_t p = 0, q;
    double v;
 
    cout << "请输入表达式：" << endl;
    getline( cin, exp );
 
    while( p < exp.size() ){
        skipws( exp, p );
        if( exp[p] == '(' ){
            so.push( obj( LP ) );
            ++p;
        }
        else if( exp[p] == '+' || exp[p] == '-' ){
            if( so.empty() || so.top().t != VAL )
                throw invalid_argument( "缺少运算数" );
            if( exp[p] == '+' )
                so.push( obj( ADD ) );
            else
                so.push( obj( SUB ) );
            ++p;
        }
        else if( exp[p] == ')' ){
            ++p;
            if( so.empty() )
                throw invalid_argument( "未匹配右括号" );
            if( so.top().t == LP )
                throw invalid_argument( "空括号" );
            if( so.top().t == VAL ){
                v = so.top().v;
                so.pop();
                if( so.empty() || so.top().t != LP )
                    throw invalid_argument( "未匹配右括号" );
                so.pop();
                new_val( so, v );
            }
            else
                throw invalid_argument( "缺少运算数" );
        }
        else{
            v = stod( exp.substr( p ), &q ); //q保存第一个非数值字符的下标
            p += q;
            new_val( so, v );
        }
 
    }
    if( so.size() != 1 || so.top().t != VAL )
        throw invalid_argument( "非法表达式" );
 
    cout << so.top().v << endl;
 
    return 0;
}
~~~
练习10.3：用accumulate求一个vector<int>中的元素之和
~~~
#include "pch.h"
#include <iostream>
#include <vector>
#include <algorithm>
#include <numeric>

using namespace std;
int main()
{

	vector<int> data;
	int i = 0;
	int sum = 0;
	cout << "please input some data:" << endl;
	while (cin >> i)
		data.push_back(i);
	cout << "data is:";
	for (const auto &i : data)
		cout << i << " ";
	cout << endl;

	sum = accumulate(data.begin(), data.end(), 0);
	cout << "sum of data :" << sum << endl;


	return 0;
}
~~~
练习10.15:编写一个lambda，捕获它所在函数的int，并接受一个int 的参数。 lambda应该返回捕获的int 和 int参数的和。
~~~
#include<iostream>
 
using namespace std;
 
void add( int a );
 
int main()
{
    add( 1 );
    return 0;
}
 
void add( int a )
{
    auto sum = [ a ]( int b ) -> int { return a+b ; };
    cout << sum( 1 ) << endl;
}
~~~
练习10.34：使用reverse_iterator逆序打印一个vector
```
#include<iostream>
#include<iterator>
#include<vector>
 
using namespace std;
 
int main()
{
    vector<int> ivec{ 1, 2, 3, 4, 5, 6, 7, 8, 9 };
    for( auto r_iter = ivec.crbegin(); r_iter != ivec.crend(); ++r_iter )
        cout << *r_iter << " ";
    cout << endl;
 
    return 0;

}
```
练习10.42：用list代替vector重新实现10.2.3节中取出重复单词的程序。
```
#include<iostream>
#include<list>
#include<fstream>
#include<iterator>
#include<string>
 
using namespace std;
 
int main()
{
    ifstream fin;
    fin.open( "T10_9_data.txt" );
    if( !fin ){
        cerr << "打开文件失败！";
        return -1;
    }
    istream_iterator<string> in( fin );
    istream_iterator<string> eof;
    ostream_iterator<string> out( cout, " " );
    list<string> lst( in, eof );
    fin.close();
    cout << "list原有数据为：" << endl;
    for( const auto &s : lst )
        out = s;
    cout << endl;
 
    lst.sort();
    lst.unique();
    cout << "删除重复元素之后..." << endl;
    for( const auto &s : lst )
        out = s;
    cout << endl;
 
    return 0;
}
```
练习11.12：编写程序，读入string和int的序列，将每个string和int存入一个pair中，pair保存在一个vector中。
```
#include<iostream>  
#include<string>  
#include<fstream>
#include<list>
#include<vector> 
#include<map>  
#include<set>
#include<cctype>
#include<algorithm>
#include<utility>
using namespace std;
 
int main(int argc, char**argv)  
{ 
	vector<pair<string,int>> vec1(12);
	ifstream in1("1.txt");
	string str;
	size_t i = 0;
	while (in1>>str)
	{
		vec1[i].first = str;
		++i;
	}
	ifstream in2("2.txt");
	int val;
	size_t j = 0;
	while (in2>>val)
	{
		vec1[j].second = val;
		++j;
	}
 
	vector<pair<string,int>>::iterator it1 = vec1.begin();
	cout<<"vector中元素为："<<endl;
	for (it1; it1 != vec1.end(); ++it1)
	{
		cout<<it1->first<<" "<<it1->second<<endl;
	}
 
	return 0;  
}  
```
练习11.17：假定c是一个string的multiset，v是一个string的vector，解释下面的调用。指出每个调用是否合法。

set的迭代器是const的。因此只允许访问set中的元素，而不能改变set。

所以前两个调用非法。

后两个调用合法  


练习13.12：在下面的代码片段中会发生几次析构函数的调用？
bool fcn( const Sales_data *trans, Sales_data accum )

{

Sales_data item1( *trans ), item2( accum );

return item1.isbn() != item2.isbn();

}



三次析构函数的调用。

函数结束时：

局部变量item1,item2的生命期结束，被销毁，Sales_data的析构函数被调用。

参数accum的生命期结束，被销毁，调用Sales_data的析构函数。 

练习13.18：定义一个Employee类，它包含雇员的姓名和唯一的雇员证号。为这个类定义默认构造函数，以及接受一个表示雇员姓名的string的构造函数。每个构造函数应该通过递增一个static数据成员来生成一个唯一的证号。  
```
#ifndef EMPLOYEE_H_INCLUDED
#define EMPLOYEE_H_INCLUDED
 
class Employee{
private:
    static int Seq;
public:
    //默认构造函数
    Employee(): EmployeeNo( Seq++ ) { }
    //接受一个string的构造函数
    Employee( const string &s ): Name(s), EmployeeNo(Seq++) { }
    //拷贝构造函数
    Employee( const Employee &ep ) { Name = ep.Name; EmployeeNo = Seq++; }
    //拷贝赋值运算符
    Employee& operator=( const Employee &ep ) { Name = ep.Name; return *this; }
private:
    string Name;
    int EmployeeNo;
};
 
int Employee::Seq = 0;
 
#endif // EMPLOYEE_H_INCLUDED
```
练习13.46：什么类型的引用可以绑定到下面的初始化器上？

int &&r1 = f();

int &r2 = vi[0];

int &r3 = r1;

int &&r4 = vi[0] *练习13.49：为你的StrVec、String和Message类添加一个移动构造函数和一个移动赋值运算符。  
```
#ifndef STRVEC_H_INCLUDED
#define STRVEC_H_INCLUDED
 
//类 vector类分配策略的简化实现
#include<memory>
#include<utility>
#include<initializer_list>
#include<algorithm>
 
using namespace std;
 
class StrVec{
public:
    //默认构造函数
    StrVec():
        elements( nullptr ), first_free( nullptr ), cap( nullptr ) { }
 
    //其他构造函数
    StrVec( initializer_list<string>& );
    //拷贝构造函数
    StrVec( const StrVec& );
    //析构函数
    ~StrVec();
    //拷贝赋值运算符
    StrVec& operator=( const StrVec& );
    //移动构造函数
    StrVec( StrVec &&sv ) noexcept :
        elements( sv.elements ), first_free( sv.first_free ), cap( sv.cap ) { }
 
    //移动赋值运算符
    StrVec& operator=( StrVec &&sv ) noexcept;
 
    void push_back( const string& );
    size_t size() const { return first_free - elements; }
    size_t capacity() const { return cap - elements; }
    void resize( size_t n );
    void reserve( size_t n );
    string* begin() const { return elements; }
    string* end() const { return first_free; }
 
private:
 
    //数据成员
    static allocator<string> alloc;
 
    string *elements;
    string *first_free;
    string *cap;
 
    //工具函数
    void chk_n_alloc();
    pair<string*, string*>
        alloc_n_copy( const string*, const string* );
    void free();
    void reallocate();
    void reallocate( size_t n );
 
};
//静态成员类外定义
allocator<string> StrVec::alloc;
 
inline
StrVec::StrVec( initializer_list<string> &ls ){
    auto newdata = alloc_n_copy( ls.begin(), ls.end() );
 
    elements = newdata.first;
    first_free = cap = newdata.second;
}
 
 
//如果没有空间，则调用reallocate分配更多内存。
inline void StrVec::chk_n_alloc( void ){
    if( size() == capacity() )
        reallocate();
}
 
 
//分配内存，并拷贝一个给定范围中的元素
pair<string*, string*>
        StrVec::alloc_n_copy( const string *b, const string *e )
{
    auto data = alloc.allocate( e - b );
 
    return { data, uninitialized_copy( b, e, data ) };
}
 
//会销毁构造的元素并释放内存
 
/*
void StrVec::free(){
    //不能传递给deallocate一个空指针
    if( elements ){//逆序销毁旧元素
        for( auto p = first_free; p != elements;  ) //for循环的第三个表达式为空。
            alloc.destroy( --p );
        alloc.deallocate( elements, cap - elements );
    }
}
*/
//用for_each和lambda重写free
void StrVec::free(){
    for_each( elements, first_free, []( const string &s ) { alloc.destroy( &s ); } );
    alloc.deallocate( elements, cap - elements );
}
 
 
StrVec::StrVec( const StrVec &sv ){
    auto newdata = alloc_n_copy( sv.begin(), sv.end() );
    elements = newdata.first;
    first_free = cap = newdata.second;
}
 
 
StrVec::~StrVec(){
    free();
}
 
StrVec& StrVec::operator=( const StrVec &sv ){
    auto newdata = alloc_n_copy( sv.begin(), sv.end() );
    free();
    elements = newdata.first;
    first_free = cap = newdata.second;
 
    return *this;
}
 
StrVec& StrVec::operator=( StrVec &&sv ) noexcept{
    if( this != &sv ){
        free();
        elements = sv.elements;
        first_free = sv.first_free;
        cap = sv.cap;
        //将rhs置于可析构的状态
        sv.elements = sv.first_free = sv.cap = nullptr;
    }
    return *this;
}
 
 
void StrVec::push_back( const string &s ){
    chk_n_alloc();
 
    alloc.construct( first_free++, s );
}
 
 
void StrVec::reallocate(){
    auto newcapacity = ( size()? 2 * size() : 1 );
 
    auto newdata = alloc.allocate( newcapacity );
 
    auto dest = newdata;
    auto elem = elements;
 
    for( size_t i = 0; i != size(); ++i )
        alloc.construct( dest++, std::move( *elem++ ) );
    free();
 
    elements = newdata;
    first_free = dest;
    cap = elements + newcapacity;
}
 
void StrVec::reallocate( size_t n ){
    auto newdata = alloc.allocate( n );
    auto dest = newdata;
    auto elem = elements;
 
    for( size_t i = 0; i != size(); ++i )
        alloc.construct( dest++, std::move( *elem++ ) );
    free();
 
    elements = newdata;
    first_free = dest;
    cap = newdata + n;
}
 
void StrVec::resize( size_t n ){
    if( n > size() ){
        while( size() < n )
            push_back( "" );
    }
    else if( n < size() ){
        while( size() > n )
            alloc.destroy( --first_free );
    }
}
 
void StrVec::reserve( size_t n ){
    if( n > capacity() )
        reallocate( n );
}
 
#endif // STRVEC_H_INCLUDED
```
练习14.3：string和vector都定义了重载的==以比较各自的对象，假设svec1和svec2是存放string的vector，确定在下面的表达式中分别使用了哪个版本的==？

(a) "cobble" == "stone"

直接比较的是字符串首元素的地址。内置版本的==



(b)svec1[0] == svec2[0]

调用的是string的重载的==运算符



(c)svec1 == svec2

调用了vector的重载的==运算符



(d)svec1[0] == "stone"

调用了string的重载的==运算符。字面字符常量被转换为string

练习14.20：为你的Sales_data类定义加法和复合赋值运算符。
```
istream& Sales_data::operator>>( istream &is, Sales_data &rhs ){
    is >> rhs.bookNo;
    is >> rhs.units_sold;
    is >> rhs.selling_price;
    is >> rhs.sales_price;
    if( is && !selling_price )
        discount = sales_price / selling_price;
    else
        rhs = Sales_data();
    return is;
}
 
ostream& Sales_data::operator<<( ostream &os, const Sales_data &rhs ){
    os << rhs.bookNo << " "
        << rhs.units_sold << " "
        << rhs.selling_price << " "
        << rhs.sales_price << " "
        << rhs.discount; //不添加换行，换行自行添加，增加操作的灵活性。
    
    return os;
}
 
Sales_data& Sales_data::operator+=( const Sales_data &rhs ){
//同一本书的零售价应该是相同的，所以selling_price应该相同。
    sales_price = ( sales_price * units_sold + rhs.sales_price * rhs.units_sold )
                / ( units_sold + rhs.units_sold );
    units_sold += rhs.units_sold;
    if( selling_price != 0 )
        discount = sales_price / selling_price;
        
    return *this;
}
 
Sales_data Sales_data::operator+( const Sales_data &lhs, const Sales_data &rhs ){        
//默认认为两个Sales_data对象的bookNo相同
    Sales_data tmp( lhs );
    tmp += rhs;
    
    return tmp;
}
```
练习15.12：有必要将一个成员函数同时声明成override和final吗？
如果希望编译器帮助我们检查是否覆盖了相应的虚函数，同时，禁止派生的类覆盖该函数，那么就有必要同时声明成override和final。而且这样能使得我们的意图更加清晰。  

练习15.16：改写你在15.2.2节练习中编写的数量受限的折扣策略，令其继承Disc_quote
```
class Limited_quote: public Disc_quote{
public:
    Limited_quote() = default;
    Limited_quote( const std::string &bk, double pr, std::size_t qty, double disc ):
        Disc_quote( bk, pr, qty, disc ) { }
    
    double net_price( std::size_t n ) const override{
        if( n <= quantity )
            return n * ( 1 - discount ) * price;
        else
            return quantity * ( 1 - discount ) * price + ( n - quantity ) * price;
    }
};
```
练习15.30：编写你自己的Basket类，用它计算上一个练习中交易记录的总价格。

```
#ifndef BASKET_H_INCLUDED
#define BASKET_H_INCLUDED
 
#include<memory>
#include<iostream>
#include<set>
#include"Quote.h"
 
using namespace std;
 
class Basket{
public:
    void add_item( const Quote& );
    void add_item( Quote&& );
 
    double total_receipt( ostream& ) const;
private:
    static bool compare( const shared_ptr<Quote> &lhs , const shared_ptr<Quote> &rhs )
        { return lhs->isbn() < rhs->isbn(); }
    multiset<shared_ptr<Quote>, decltype(compare)*> items{ compare };
};
 
 
void Basket::add_item( const Quote &sale ){
    items.insert( shared_ptr<Quote> ( sale.clone() ) );
}
/*
void Basket::add_item( Quote &&sale ){
    items.insert( shared_ptr<Quote> ( std::move( sale ).clone() ) );
}
*/
double Basket::total_receipt( ostream &os ) const{
    double sum = 0.0;
    for( auto iter = items.cbegin(); iter != items.cend(); iter = items.upper_bound( *iter ) )
        sum += print_total( os, **iter, items.count( *iter ) );
    os << "Total sale: " << sum << endl;
 
    return sum;
}
#endif // BASKET_H_INCLUDED
```

练习8.4：编写函数，以读模式打开一个文件，将其内容读入到一个string的vector中，将每一行作为一个独立的元素存在于vector中。  
```
#include<iostream>
#include<fstream>
#include<vector>
#include<string>
 
using namespace std;
 
int main()
{
    ifstream fin;
    string line;
    vector<string> svec;
    fin.open( "a.txt" );
    if( fin ){//是否成功打开。
        while( !fin.eof() ){ //直到文件末尾
            getline( fin, line );
            svec.push_back( line );
        }
    }
    else{
        cerr << "打开文件失败！" << endl;
        return -1;
    }
	    fin.close();
    for( const auto &lin : svec )
        cout << lin << endl;
 
    return 0;
}
```
练习8.7：修改上一节的书店程序，将结果保存到一个文件中。请将输出文件名作为第二个参数传递给main函数  
```
#include<iostream>
#include<fstream>
#include"Sales_data.h"
 
using namespace std;
 
int main( int argc, char *argv[] )
{
    ifstream fin;
    ofstream fout;
    if( argc != 3 ){
        cerr << "请正确输入命令行参数" << endl;
        return -1;
    }
    fin.open( argv[1] );
    fout.open( argv[2] );//隐含设置为输出和截断
    if( !fin ){//是否成功打开
        cerr << "打开文件失败！" << endl;
        return -1;
    }
    Sales_data total;
    if( fin >> total ){
        Sales_data trans;
        while( fin >> trans ){
            if( total.isbn() == trans.isbn() )
                total += trans;
            else{
                fout << total << endl;
                total = trans;
            }
        }
        fout << total << endl;
    }
    else{
        cerr << "No data!?" << endl;
        return -1;
    }
    fin.close();
    fout.close();
    return 0;
}
```
练习8.9：使用你为8.1.2节第一个练习所编写的函数打印一个istringstream对象的内容。  
```
#include<iostream>
#include<sstream>
#include<stdexcept>
using namespace std;
 
istream& Func( istream &is );
 
int main()
{
    string str( "C++ Primer 5th" );
    istringstream sin( str );
    if( sin )
        Func( sin );
    else{
        cerr << "字符串流出现错误" << endl;
    }
    return 0;
}
 
 
istream& Func( istream &is )
{
    string s;
    while( is >> s ){
        if( is.bad() )
            throw runtime_error( "IO流已崩溃。" );
        if( is.fail() ){
            cerr << "IO操作失败，请重试" << endl;
            is.clear();
            is.ignore( 100, '\n');//读取并抛弃。直到读取100个或者遇到'\n'为止。用来清除上一次输入对下一次输入的影响。
            continue;
        }
        cout << s << endl;
    }
    is.clear();//返回流之前，对其进行复位。
    return is;
}
```

练习16.11：下面List的定义是错误的。应如何修正它。

template <typename elemType> class ListItem;

template <typename elemType> class List{

public:

//黑色删除线 代表的是 可以删除的地方

List<elemType>();

List<elemType> ( const List<elemType> &);

List<elemType>& operator=( const List<elemType> & );

~List();

//红色代表修改的地方。

void insert( ListItem<elemType> *ptr, elemType value );

private:

ListItem *front, *end;

ListItem<elemType> *front, *end;

//模板的名字不是一个类型。实例化成具体的类才是一个类型。

};

练习16.12：编写你自己版本的Blob和BlobPtr模板，包含书中未定义的多个const成员。

```

 
#include<vector>
#include<memory>
#include<initializer_list>
#include<stdexcept>
#include<iterator>
 
//模板前置声明
 
template<typename> class Blob;
 
template <typename T>
bool operator==( const Blob<T>&, const Blob<T>& );
 
template <typename> class BlobPtr;
 
template <typename T> class Blob{
    //友元声明
    friend class BlobPtr<T>;
    friend bool operator==<T>( const Blob<T>&, const Blob<T>& );
public:
    typedef typename std::vector<T>::size_type size_type;
    //构造函数
    Blob():
        data( std::make_shared<std::vector<T>>() ) { }
    Blob( std::initializer_list<T> lst ):
        data( std::make_shared<std::vector<T>>( lst ) ) { }
    template <typename It>
    Blob( It b, It e ):
        data( std::make_shared<std::vector<T>>( b, e ) ) { }
 
    Blob( T *p, size_t n ):
        data( std::make_shared<std::vector<T>>( p, p + n ) ) { }
 
 
    //公共接口
    bool empty() const { return data->empty(); }
    size_type size() const { return data->size(); }
 
    //先搁置
    BlobPtr<T> begin() { return BlobPtr<T>( *this, 0 ); }
    BlobPtr<T> end() { return BlobPtr<T>( *this, data->size() ); }
 
    T& front();
    T& back();
    const T& front() const;
    const T& back() const;
 
    T& at( size_type );
    const T& at( size_type ) const;
 
    void push_back( const T &val ) { data->push_back( val ); }
    void push_back( T &&val ) { data->push_back( std::move( val ) ); }
 
    void pop_back();
 
    //重载运算符
    T& operator[]( size_type i );
    const T& operator[]( size_type i ) const;
private:
    //数据成员
    std::shared_ptr<std::vector<T>> data;
    //辅助函数
    void check( size_type, const std::string& ) const;
};
 
template <typename T>
void Blob<T>::check( size_type n, const std::string &msg ) const{
    if( n >= size() )
        throw std::out_of_range( msg );
}
 
template <typename T>
T& Blob<T>::front() {
    check( 0, "front on empty Blob" );
    return data->front();
}
 
template <typename T>
const T& Blob<T>::front() const{
    check( 0, "front on empty Blob" );
    return data->front();
}
 
template <typename T>
T& Blob<T>::back() {
    check( 0, "back on empty Blob" );
    return data->back();
}
 
template <typename T>
const T& Blob<T>::back() const{
    check( 0, "back on empty Blob" );
    return data->back();
}
 
template <typename T>
void Blob<T>::pop_back(){
    check( 0, "pop_back on empty Blob" );
    data->pop_back();
}
 
template <typename T>
T& Blob<T>::at( size_type i ){
    check( i, "subscript out of range" );
    return ( *data )[ i ];
}
 
template <typename T>
const T& Blob<T>::at( size_type i ) const{
    check( i, "subscript out of range" );
    return ( *data )[ i ];
}
 
template <typename T>
T& Blob<T>::operator[]( size_type i ){
    check( i, "subscript out of range" );
    return ( *data )[ i ];
}
 
template <typename T>
const T& Blob<T>::operator[]( size_type i ) const{
    check( i, "subscript out of range" );
    return ( *data )[ i ];
}
 
 
//友元运算符定义
template <typename T>
bool operator==( const Blob<T> &lhs, const Blob<T> &rhs ){
    if( lhs.size() != rhs.size() )
        return false;
    for( size_t i = 0; i != lhs.size(); ++i )
        if( lhs[i] != rhs[i] )
            return false;
    return true;
}
 
template <typename T>
    bool operator==( const BlobPtr<T>&, const BlobPtr<T>& );
 
template <typename T> class BlobPtr{
    friend bool operator==<T>( const BlobPtr<T>&, const BlobPtr<T>& );
public:
    BlobPtr():
        curr( 0 ) { }
    BlobPtr( Blob<T> &a, std::size_t sz = 0 ):
        wptr( a.data ), curr( sz ) { }
 
    //公共接口
    T& operator[]( std::size_t i ){
        auto ret = check( i, "subscript out of range" );
        return ( *ret )[ i ];
    }
 
    const T& operator[]( std::size_t i ) const{
        auto ret = check( i, "subscript out of range" );
        return ( *ret )[ i ];
    }
 
    T& operator*() const{
        auto ret = check( curr, "dereference past end" );
        return ( *ret )[ curr ];
    }
 
    T* operator->() const{
        return & this->operator*();
    }
 
 
    BlobPtr& operator++();
    BlobPtr& operator--();
 
    BlobPtr operator++(int);
    BlobPtr operator--(int);
private:
    //数据成员
    std::weak_ptr<std::vector<T>> wptr;
    std::size_t curr;
    //辅助函数
    std::shared_ptr<std::vector<T>> check( std::size_t, const std::string& ) const;
};
 
template <typename T>
bool operator==( const BlobPtr<T> &lhs, const BlobPtr<T> &rhs )
{
    return lhs.wptr.lock().get() == rhs.wptr.lock().get() && lhs.curr == rhs.curr;
}
 
template <typename T>
bool operator!=( const BlobPtr<T> &lhs, const BlobPtr<T> &rhs )
{
    return !( lhs == rhs );
}
 
template <typename T>
std::shared_ptr<std::vector<T>>
BlobPtr<T>::check( std::size_t i, const std::string &msg ) const
{
    auto ret = wptr.lock();
    if( !ret )
        throw std::runtime_error( "unbound BlobPtr" );
    if( i >= ret->size() )
        throw std::out_of_range( msg );
    return ret;
}
 
template <typename T>
BlobPtr<T>& BlobPtr<T>::operator++(){
    check( curr, "increment past end" );
    ++curr;
    return *this;
}
 
template <typename T>
BlobPtr<T>& BlobPtr<T>::operator--(){
    --curr;
    check( curr, "decrement past begin" );
    return *this;
}
 
template <typename T>
BlobPtr<T> BlobPtr<T>::operator++(int){
    auto ret = *this;
    ++*this;
    return ret;
}
 
template <typename T>
BlobPtr<T> BlobPtr<T>::operator--(int){
    auto ret = *this;
    --*this;
    return ret;
}
 

```
练习16.19：编写函数，接受一个容器的引用，打印容器中的元素。使用容器的size_type和size成员来控制打印元素的循环。

```
#include<iostream>
#include<vector>
#include<list>
 
template <typename container>
void print( std::ostream &os, const container &con ){
    auto iter = con.begin();
    for( typename container::size_type i = 0; i != con.size(); ++i, ++iter )
        os << *( iter ) << " ";
    os << std::endl;
}
 
using namespace std;
 
int main()
{
    vector<int> ivec( { 0, 1, 2, 3, 4, 5, 6, 7 } );
    list<string> lst = { "i", "wanna", "feel" };
 
    print( cout, ivec );
    print( cout, lst );
    return 0;
}
```

练习16.62：定义你自己版本的hash<Sales_data>,并定义一个Sales_data对象的unordered_multiset。将多条交易记录保存到容器中，并打印其内容

```

 
#include<iostream>
class Sales_data{
    //友元函数
    friend struct std::hash<Sales_data>;
    friend std::istream& operator >> ( std::istream&, Sales_data& );
    friend std::ostream& operator << ( std::ostream&, const Sales_data& );
    friend bool operator < ( const Sales_data&, const Sales_data& );
    friend bool operator == ( const Sales_data&, const Sales_data& );
    friend Sales_data add( Sales_data &rhs, Sales_data &lhs );
    friend std::istream& read( std::istream& in, Sales_data &item );
    friend std::ostream& print( std::ostream &out, const Sales_data &rhs );
 
    public:  //构造函数
 /*       Sales_data( const std::string &book, const unsigned units, const double sellingprice, const double saleprice ) :
            bookNo( book ), units_sold( units ), selling_price( sellingprice ), sale_price( saleprice )
            {
                if( selling_price )
                    discount = sale_price / selling_price;
                std::cout << "四个参数的构造函数的函数体" << std::endl;
            }
*/
        //委托构造函数:
 /*       Sales_data(): Sales_data( "", 0, 0, 0 ) { std::cout << "无参数的构造函数的函数体" << std::endl; }
        Sales_data( const std::string &s ) : Sales_data( s, 0, 0, 0 ) { std::cout << "接受字符串的构造函数的函数体" << std::endl; };
        Sales_data( std::istream &is ) : Sales_data() { read( is, *this ); std::cout << "接受输入流的构造函数的函数体" << std::endl; }
*/
        Sales_data() = default;
        Sales_data( const std::string &book ): bookNo( book ) { }
        Sales_data( const std::string &book, const unsigned units, const double sellingprice, const double saleprice );
        Sales_data( std::istream &is ) { is >> *this; }
 
    public:
        Sales_data& operator += ( const Sales_data& );
        std::string isbn() const { return bookNo; }
        Sales_data& combine( const Sales_data &rhs );
 
    private:
        std::string bookNo;
        unsigned units_sold = 0;
        double selling_price = 0.0;
        double sale_price = 0.0;
        double discount = 0.0;
};
 
 
inline bool compareIsbn( const Sales_data&lhs, const Sales_data&rhs )
{
    return lhs.isbn() == rhs.isbn();
}
 
Sales_data operator + ( const Sales_data&, const Sales_data& );//声明
 
//友元函数定义
inline bool operator == ( const Sales_data &lhs, const Sales_data &rhs )
{
    return lhs.units_sold == rhs.units_sold && lhs.sale_price == rhs.sale_price &&
            lhs.isbn() == rhs.isbn();
}
 
inline bool  operator != ( const Sales_data &lhs, const Sales_data &rhs )
{
    return !( lhs == rhs );
}
 
inline bool operator<( const Sales_data &lhs, const Sales_data &rhs )
{
    return lhs.bookNo < rhs.bookNo;
}
 
inline Sales_data add( Sales_data &rhs, Sales_data &lhs )
{
    Sales_data sum = rhs;
    sum.combine( lhs );
    return sum;
}
inline std::ostream& print( std::ostream &out, const Sales_data &rhs )
{
    out << rhs.bookNo << " " << rhs.units_sold << " " << rhs.selling_price << " "
        << rhs.sale_price << " " << rhs.discount;
    return out;
}
 
inline std::istream& read( std::istream& in, Sales_data &item )
{
 
 
    in >> item.bookNo >> item.units_sold >> item.selling_price >> item.sale_price;
    return in;
}
 
//构造函数
Sales_data::Sales_data( const std::string &book, unsigned units, double sellingprice, double saleprice )
{
    bookNo = book;
    units_sold = units;
    selling_price = sellingprice;
    sale_price = saleprice;
    if( selling_price != 0 )
        discount = sale_price / selling_price;
}
 
 
 
//成员函数
Sales_data& Sales_data::operator += ( const Sales_data &rhs )
{
    sale_price = ( rhs.sale_price * rhs.units_sold + sale_price * units_sold )
                /( rhs.units_sold + units_sold );
    selling_price = ( rhs.selling_price * rhs.units_sold + selling_price * units_sold )
                /( rhs.units_sold + units_sold );
    units_sold += rhs.units_sold;
 
    if( sale_price != 0 )
        discount = sale_price / selling_price;
 
    return *this;
}
 
 
Sales_data operator + ( const Sales_data &lhs, const Sales_data &rhs )
{
    Sales_data tmp( lhs );
    tmp += rhs;
 
    return tmp;
}
 
 
std::istream& operator >> ( std::istream &in, Sales_data &s )
{
    in >> s.bookNo >> s.units_sold >> s.selling_price >> s.sale_price;
 
    if( in && s.selling_price != 0 )
        s.discount = s.sale_price / s.selling_price;
    else
        s = Sales_data();
 
    return in;
}
 
 
std::ostream& operator << ( std::ostream &out, const Sales_data &s )
{
    out << s.isbn() << " " << s.units_sold << " "
        << s.selling_price << " " << s.sale_price << " " << s.discount;
 
    return out;
}
 
Sales_data& Sales_data::combine( const Sales_data &rhs )
{
    units_sold += rhs.units_sold;
    sale_price = ( units_sold * sale_price + rhs.units_sold * rhs.sale_price )
                / ( units_sold + rhs.units_sold );
    if( selling_price != 0 )
        discount = sale_price / selling_price;
 
    return *this;
}
 
namespace std{
    template <> struct hash<Sales_data>{
        typedef size_t result_type;
        typedef Sales_data argument_type;
 
        size_t operator()( const Sales_data & s ) const;
    };
 
    size_t hash<Sales_data>::operator() ( const Sales_data &s ) const{
        return hash<string>()( s.bookNo ) ^
            hash<unsigned>() ( s.units_sold ) ^
            hash<double>() ( s.selling_price ) ^
            hash<double>() ( s.sale_price );
    }
}
 

```

练习12.1：在此代码的结尾，b1和b2各包含多少个元素？

StrBlob b1;

{

StrBlob b2 = { "a", "an", "the" };

b1 = b2;

b2.push_back( "about" );

}

b1有4个元素。

b2被销毁。但是元素底层元素并没有被销毁。


练习12.10：下面的代码调用了第413页中定义的process函数，解释此调用是否正确。如果不正确，应如何修改？

shared_ptr<int> p( new int(42) );

process( shared_ptr<int>(p) );

此调用是正确的。

  参数位置的shared_ptr<int>(p)，会创建一个临时的shared_ptr赋予process的参数ptr，引用计数值加1，当调用所在的表达式结束时，这个临时变量就会被销毁，引用计数减1。同时将值拷贝给ptr，计数值加1。但函数结束后ptr被销毁，引用计数减1。

最终p的引用计数还是1。内存不会被释放。

练习12.15：重写第一题的程序，用lambda代替end_connection函数。
```
#include<iostream>
#include<memory>
 
using namespace std;
 
struct destination{ };//表示我们正在连接什么
struct connection{ };//使用连接所需的信息
 
connection connect( destination* );//打开连接
void disconnect( connection );//关闭给定的连接
 
void f( destination& );
void f1( destination & );
 
//void end_connection( connection *p );
 
 
int main()
{
    destination d;
    f1( d );
    f( d );
 
    return 0;
}
/*
void end_connection( connection *p )
{
    disconnect( *p );
}
*/
connection connect( destination *pd )
{
    cout << "打开连接" << endl;
    return connection();
}
void disconnect( connection c )
{
    cout << "连接关闭" << endl;
}
 
void f( destination &d )
{
    //获得一个连接
    connection c = connect( &d );
    cout << "用shared_ptr管理connect" << endl;
    shared_ptr<connection> sp( &c, []( connection *p ){ disconnect( *p ); } );
    /* 获得连接后的操作 */
    //忘记调用disconnect
    //当f退出时，不管是正常退出还是异常退出，connection都会被正确关闭。
}
 
void f1( destination &d )
{
    cout << "直接管理connect" << endl;
    connection c = connect( &d );
    //忘记调用disconnect
    cout << endl;
}
```
练习12.17：下面的unique_ptr声明中，哪些是合法的，哪些可能导致后续的程序错误？解释每个错误的问题在哪里。

int ix = 1024, *pi = &ix, *pi2 = new int(2048);

typedef unique_ptr<int> IntP;

(a) IntP p0(ix);

不合法。当我们定义一个unique_ptr时，需要将其绑定到一个new返回的指针上。

(b)IntP p1(pi);

不合法。不是new返回的指针。

合法。但是逻辑上是错误的。它用一个普通的int变量的地址初始化p1，p1销毁时会释放此内存，其行为是未定义的。

(c)IntP p2(pi2);

合法。

(d)IntP p3( &ix );

合法。但是同以上(b)的问题。

(e)IntP p4( new int(2048) );

合法。

(f)IntP p5( p2.get() );

合法。但是有问题。会造成两个unique_ptr指向相同的内存地址。当其中一个unique_ptr被销毁时（或者被reset释放对象时），该内存被释放，另一个unique_ptr会变成空悬指针。



练习12.18：shared_ptr为什么没有release成员。

unique_ptr不能赋值和拷贝，而release成员是用来转移对象的所有权的。

 shared_ptr可以通过简单的赋值和拷贝转移实现共享所有权。

练习12.19：定义你自己版本的StrBlobPtr，更新StrBlob类，加入恰当的friend声明及begin和end成员。
```
#ifndef STRBLOB_H_INCLUDED
#define STRBLOB_H_INCLUDED
#include<vector>
#include<string>
#include<stdexcept>
#include<initializer_list>
#include<memory>
 
using namespace std;
 
class StrBlobPtr;//友元类外部声明。
 
class StrBlob{
public:
    //友元类声明
    friend class StrBlobPtr;
    //构造函数
    StrBlob();
    StrBlob( initializer_list<string> il );
    //容器大小访问
    vector<string>::size_type size() const { return data->size(); }
    bool empty() const { return data->empty(); }
    //添加和删除元素
    void push_back( const std::string &str ) { data->push_back( str ); }
    void pop_back();
    //元素访问
    string& front();
    const string& front() const;
    string& back();
    const string& back() const;
    //返回指向首元素和尾元素的StrBlobPtr
    StrBlobPtr begin();
    StrBlobPtr end();
 
private:
    std::shared_ptr<std::vector<std::string>> data;
    void check( vector<string>::size_type i, const std::string &msg ) const ;
 
};
 
 
inline StrBlob::StrBlob(): data( make_shared<vector<string>>() ) { }
inline StrBlob::StrBlob(initializer_list<string> il): data( make_shared<vector<string>> (il) ) { }
 
 
inline void StrBlob::check( vector<string>::size_type i, const std::string &msg ) const
{
    if( i >= data->size() )
        throw out_of_range( msg );
}
 
inline void StrBlob::pop_back()
{
    check( 0, "pop_back on empty StrBlob" );
    data->pop_back();
}
 
inline string& StrBlob::front()
{
    check( 0, "front on empty StrBlob" );
    return data->front();
}
 
inline const string& StrBlob::front() const
{
    check( 0, "front on empty StrBlob");
    return data->front();
}
 
inline string& StrBlob::back()
{
    check( 0, "back on empty StrBlob" );
    return data->back();
}
 
inline const string& StrBlob::back() const
{
    check( 0, "back on empty StrBlob" );
    return data->back();
}
 
 
 
//StrBlobPtr类
 
class StrBlobPtr{
    friend bool eq( const StrBlobPtr&, const StrBlobPtr& );
public:
    StrBlobPtr():curr(0) { }
    StrBlobPtr( StrBlob &a, size_t sz = 0 ): wptr( a.data ), curr( sz ) { }
 
    string& deref() const;//解引用
    StrBlobPtr& Incr();//前缀递增
 
private:
    shared_ptr<vector<string>> check( size_t, const string& ) const;
    weak_ptr<vector<string>> wptr;
    size_t curr;
};
 
inline shared_ptr<vector<string>> StrBlobPtr::check( size_t i, const string &msg ) const
{
    auto ret = wptr.lock();
    if( !ret )
        throw runtime_error( "unbound StrBlobPtr" );
    if( i >= ret->size() )
        throw out_of_range( msg );
    return ret;
}
 
inline string& StrBlobPtr::deref() const
{
    auto sp = check( curr, "dereference pass end" );
 
    return (*sp)[ curr ];
}
 
inline StrBlobPtr& StrBlobPtr::Incr()
{
    auto sp = check( curr, "increment past end of StrBlobPtr" );
 
    ++curr;
 
    return *this;
}
 
 
inline StrBlobPtr StrBlob::begin()
{
    return StrBlobPtr( *this );
}
 
inline StrBlobPtr StrBlob::end()
{
    auto ret = StrBlobPtr( *this, data->size() );
    return ret;
}
 
 
inline bool eq( const StrBlobPtr &lhs, const StrBlobPtr &rhs )
{
    auto l = lhs.wptr.lock(), r = rhs.wptr.lock();
    if( l == r )
        return ( !r || lhs.curr == rhs.curr );
    else
        return false;
}
 
inline bool uneq( const StrBlobPtr &lhs, const StrBlobPtr &rhs )
{
    return !eq( lhs, rhs );
}
 
#endif // STRBLOB_H_INCLUDED
```

练习12.30：定义你自己版本的TextQuery和QueryResult类，并执行12.3.1节中的runRequery函数

```
#ifndef TEXTQUERY_H_INCLUDED
#define TEXTQUERY_H_INCLUDED
 
#include<vector>
#include<fstream>
#include<memory>
#include<sstream>
#include<string>
#include<map>
#include<set>
 
using namespace std;
 
class QueryResult; //前向声明
 
class TextQuery{
public:
    //类型别名
    typedef vector<string>::size_type line_no;
    //构造函数。
    TextQuery( ifstream& );
    QueryResult query( const string& ) const;
private:
    shared_ptr<vector<string>> file;
    map<string, shared_ptr<set<line_no>>> wordMap;
 
};
 
//构造函数定义。读取文件按行存入vector，并且建立单词与行号映射。
TextQuery::TextQuery( ifstream &fin ): file( new vector<string> )
{
    string line;
    //为了使得行号从1开始对应。我把vector的位置0先设为空串。
    file->push_back( "" );
    while( getline( fin, line ) ){
        file->push_back( line );
        unsigned lineN = file->size() - 1; //lineN用来保存行号。
        istringstream sin( line );
        string word;
        while( sin >> word ){
            auto &lines = wordMap[ word ]; //lines是一个shared_ptr
            if( !lines )
                lines.reset(  new set<line_no> ); //如果lines为空指针（set没有元素）,分配一个新的set
            lines->insert( lineN );
        }
    }
}
 
 
class QueryResult{
    friend ostream& print( ostream&, const QueryResult& );
public:
    QueryResult( const string& str, shared_ptr<set<TextQuery::line_no>> l,
                shared_ptr<vector<string>> f ): sought( str ), lines( l ), file( f ) { }
private:
    string sought;
    shared_ptr<set<TextQuery::line_no>> lines;
    shared_ptr<vector<string>> file;
 
};
 
QueryResult TextQuery::query( const string &s ) const
{
    static shared_ptr<set<line_no>> nodata( new set<line_no> );
 
    auto loc = wordMap.find( s );
    if( loc == wordMap.end() )
        return QueryResult( s, nodata, file );
    else
        return QueryResult( s, loc->second, file );
}
 
ostream& print( ostream &os, const QueryResult &qr )
{
    os << qr.sought << " occurs " << qr.lines->size()
        << ( ( qr.lines->size() > 1 ) ? " times" : " time" )
        << endl;
    for( auto num : *( qr.lines ) )
        os << "\t(line " << num << ") " <<  *( qr.file->begin() + num ) << endl;
    return os;
}
 
#endif // TEXTQUERY_H_INCLUDED
```










































