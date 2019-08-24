## C++_Lesson 

### Float number expression

- 下面这个网站讲的比较详细，复制完请。

  https://blog.csdn.net/jvandc/article/details/81176294#11-浮点数在计算机中的表示

### enum

- C++的一个派生数据类型，使用方法：

  ```C++
  enum<类型名>{<枚举常量表>}
  //编译系统会给常量表中每个值分配一个整数值，默认加一
  //另外常量表中只能够是标识符，不能够是字符或者整型常量
  ```

  具体这个网站https://www.runoob.com/w3cnote/cpp-enum-intro.html

### Auto,Typedef,sizeof

- **Auto** 是C++ 11新规定一个能够自动探测变量类型的关键字

  ```C++
  int a=10;
  auto b = a;
  这个时候b类型就是int
  ```

  当然其实一般不这么使用auto，今天我写的时候发现可以很好的用于循环，比如我们想遍历一个map

  ```C++
  //常规操作
  map<int,int> p;
  map<int,int>::iterator it;
  	for(it = p.begin(); it != p.end(); it++){}
  //如果使用auto
  for(auto item:p){}
  ```

- **Typdef：**定义关键字，应该不难理解
- **sizeof:**  注意这是个operator,不是function，计算变量或者数据类型的字节大小，1byte = 8 bit。当sizeof 计算字符串的时候，会把字符串最后的\0 计算进去（注意和strlen的区别，strlen是一个函数，这两个区别还是比较大的。）

### Operator Order and Operateor

- 运算符优先级和各种运算符

  https://www.runoob.com/cplusplus/cpp-operators.html





