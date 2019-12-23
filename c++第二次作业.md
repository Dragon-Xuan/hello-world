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
