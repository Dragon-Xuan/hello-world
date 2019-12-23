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










































