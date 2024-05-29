# 智能指针

## 为什么要用智能指针  
C++中引入智能指针主要是为了解决手动管理内存时繁琐和容易出错的问题. 在不用智能指针的C++操作中new分配的内容如果未能及时使用delete释放掉则会出现**野指针, 重复释放, 内存泄漏**等问题. 为什么更好的管理内存, C++增加了智能指针.

## 智能指针都有什么？分别介绍一下  
- auto_ptr: 在C++11后已被弃用; CPP官网中描述如下.
> **Note**: This class template is deprecated as of C++11. unique_ptr is a new facility with a similar functionality, but with improved security (no fake copy assignments), added features (***deleters***) and support for arrays. See unique_ptr for additional information.
- shared_ptr: 使用**引用计数**机制, **shared_ptr可以跟踪有多少个指针引用同一块内存**, 当最后一个指针不再引用该内存时会自动释放掉该内存.
> 详情参考: https://cplusplus.com/reference/memory/shared_ptr/
- unique_ptr: **独占所有权的智能指针, unique_ptr可以确保任何时刻只有一个指针拥有该内存**, 它禁止了复制和赋值的操作, 确保了内存的独占性, 当该指针超出作用域或被显示的释放时, 它会自动释放该内存.
> unique_ptr是一个独享所有权的智能指针, 它提供了严格意义上的所有权, 包括: 
1、拥有它指向的对象
2、无法进行复制构造和复制赋值操作, 即两个指针无法指向同一个对象, 但是可以进行移动构造和移动赋值操作
3、指向某个对象的指针, 当它被删除释放的时候, 它所指向的对象也会被释放掉
- weak_ptr: **weak_ptr用来解决shared_ptr相互引用导致的死锁问题**, 如果两个shared_ptr相互引用, 那么这两个指针的引用计数永远不会置0. weak_ptr是对对象的一种弱引用, 不会增加对象的引用计数, 和shared_ptr可以相互转化, shared_ptr可以直接赋值给它, weak_ptr可以调用lock函数来直获取shared_ptr. 
> 全名为weak shared pointer

