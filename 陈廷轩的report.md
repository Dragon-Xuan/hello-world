## 前期配置nebula
nebula 的前期配置按照手册上的操作上来，主要时下载依赖的时候耗时比较长，安装依赖解包的时候千万要耐心，不要打断进程，更不要ctrl+c，这会导致前功尽弃
总的来说，按照手册上的操作以及一些博客上的内容还能够完成。
## 上传时碰到的困难
git commit 时候失败
![Image text](https://github.com/ctx0509/hello-world/blob/master/image/TIM%E5%9B%BE%E7%89%8720191227015202.png?raw=true)
发现是文件的格式不对，在文件的开头添加copyright...后解决问题  
问题解决之后出现以下界面
![Image text](https://github.com/ctx0509/hello-world/blob/master/image/TIM%E5%9B%BE%E7%89%8720191227015218.png)
## 在使用git命令时
### 第一步：查看远程仓库和上游
```
git remote -v 
git remote rm orign
git remote add orign https://github.com/ctx0509/nebula.git
```

### 第二步：创建分支
```
git branch change//创建一个分支--change
git checkout change//切换到change分支
```
### 第三步：添加修改的文件到暂存区

```
git add .
git commit -m "first change"
```
### 第四步：上传代码
```
git push --set-upstream origin change
```

## 修改thread下的单元测试
![](https://github.com/ctx0509/hello-world/blob/master/image/image.png)
第一次试着使用了gtest下的断言的宏ASSERT_NE（）来判断线程是否拿到了相同的name

### 在thread_test下添加了一段TEST
```
+#include "iostream"
 #include "base/Base.h"
 #include <gtest/gtest.h>
 #include "thread/NamedThread.h"
-
+#include "vector"
 namespace nebula {
 namespace thread {

@@ -25,6 +25,20 @@ TEST(NamedThread, ThreadName) {
 TEST(NamedThread, ThreadID) {
     ASSERT_EQ(::getpid(), nebula::thread::gettid());
 }
+TEST(NameThread,test){
+   static int j=0;
+   std::vector <std::thread>t;
+   for (int i=0;i<10;i++)
+   {
+     std::thread mythread(j++);
+     t.push_back(std::move(mythread));
+   }

+   for (int i=0;i<10;i++)
+{
+   t[i].join();
+}
+     ASSERT_GE(j,10);
+}
```
使用多线程（没用锁）来测试
目前的测试还不成功，在make的时候出了问题
![](https://github.com/ctx0509/hello-world/blob/master/image/VWWN8ILF4Q%5D8S)
目前还在解决过程中
# 总结
第一次弄github,第一次在上面发代码，第一次学会使用git的命令，说实话，真的是万事开头难，以开始为了配置nebula环境也用了许久
花了很多时间，但是总是在做无用功，很难受，自己毫无方向，博客也不能即使解决我的问题，还好最后有老师来修车
，我这台破车总算开的起来了，果然如老师所说的那样，人生何处不掉坑啊，填完一个坑又进入另外一个坑，不过开源项目的好处
就是，网上资源多，解决方案多，虽然有很多不会的，但是查查博客，总还是能现学现卖的，这一个学期c++学下来，确实也是很艰难，书那么厚，
老师讲的也比较快，一个恍惚就懵逼了，但是确实老师很强，很好，传授的东西也挺有用的，至少让我们长了不少见识，这是好事，github算是
很大很知名的开源社区了，感谢老师带我入坑，至于爬不爬得出来，还得看自己的造化了，最后还是忍不住吐槽一下，c++是真的难啊。终归是基础太差，c，python，c++都不熟悉，全部都只是刚刚入门而已，数据结构也一样，一知半解，自己的学习态度上还有很大的问题，学习习惯上也有这巨大的不足。
