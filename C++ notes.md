# C++

[TOC]

## 从C到C++

### 引用

- 类型名&引用名 = 某变量名：

   int & r = n; // r 引用了n， r的类型是int

- 引用只能引用变量

- C++ 中使用引用可以简化交换的函数

   ```c++
   void swap(int&a,int&b)
   {
   int tmp;
   tmp=a;a=b;b=tmp;
   }
   int n1,n2;
   swap(n,n2);
   ```

- const int & r = n

   不能够通过常引用改变其修改的内容，即如果对r赋值会报错

### const 关键字

- const int *p = &n;

   不可通过常量指针修改其指向的内容

   *p = 5; // wrong

   n=4;// ok

   p = &m;// ok 

- 不能够把常量指针赋值给非常量指针，反过来可以。因为有安全因素，赋值后你可以通过将常量指针赋值给非常量指针来改变常量指针指向的内容。（强制转换可以（int *）)

### 动态内存分配

- P = new T:  T是任意的类型名，P是类型为T*的指针

   ```c++
   int*p = new int
   ```

- 使用new分配，使用delete运算符释放空间。 数组的delete需要加中括号 delete [] p 

### 内联函数

- ```C++
   inline int Max(int a, int b)
   {
   if(a>b) return a;
   else return b;
   }
   ```

### 函数重载

- 一个或多个函数，名字相同，函数的个数和参数类型不同，叫做函数的重载

## 类和对象基础

### 类、类成员与函数

- 类有类成员和类函数

- 

   ```c++
   int CRectangle :: Area(){
   return w*h;
   }
   ```

   ：： 说明该函数是前面类的成员函数

- 缺损值默认为private，对于私有成员变量，不可以通过类外的函数来访问，只能够通过成员函数来进行访问

### 构造函数

- 构造函数主要用于自动初始化

- ```c++
  class Complex{
  public:
    Complex(double r, int b=0)
  };
  Complex::Complex(double r, double i)
  {
     ...
  }
  ```

### 复制构造函数

- 只有一个参数，即对同类对象的引用

- x:: x(const X&) 参数必须是引用

- 用处： 用一个对象初始化同类的另外一个函数

  例如： complex c2(c1) 等价于 complex c2 = c1; (初始化语句)

  当某个函数的参数是对象，需要使用复制构造函数进行初始化

  当某个函数的返回值是对象，则函数返回时，A的赋值构造函数会被调用
  
  

### 类型转换构造函数

- 构造函数只有一个变量，常常用于转换变量类型，例如将一个int类型转换成一个对象

- 析构函数是当对象消亡的时候使用 ~fuction(), 在对象作为函数返回值返回后也会被调用

## 类和对象的提高

### this 指针

- 作用是指向成员函数所作用的对象，点的前面那个
- 静态成员函数不可以使用this指针

### static

- 就一份，为所有对象共享（sizeof不会计算静态成员变量）
- 普通成员函数必须具体作用某个对象，但是静态函数不需要具体作用于某个对象
- 使用前需要在外面进行一次初始化

- 在静态成员函数当中，不能够访问非静态成员变量，也不能调用非静态成员函数

### 成员对象和封闭类

- 成员对象和封闭类：包含成员对象的类叫封闭类

  即任何生成仍和的封闭类对象的语句，一定要注意里面成员对象的初始化问题。

- 封闭类创建时，成员对象的构造函数先起作用，类消亡的时候。封闭类的构析函数先起作用

### 常引用的用法

- 使用对象作为函数参数的时候需要调用对象的复制构造函数，很没有效率，因此我们可以使用对象的常引用作为参数：

  ```c++
  class Sample{
  ...
  }
  void PrinfOBJ(const Sample&o){
  ...
  }
  ```

  

### 友元

- 友元函数：一个类的友元函数可以访问该类的私有成员

  ```c++
  class B{
   public:
       void function();
  };
  class A{
       friend void B::function();
  };
  ```

- 友元类： 即该友元类中的所有成员函数都可以访问别人的私有成员。友元类之间的关系不能传递，不能继承

## 运算符重载

### 基本概念

- 同一个运算符作用于不同对象意义不同

- 重载形式——返回值类型 operator 运算符（形参表）{}

  ```c++
  class Complex{
  public:
     Complex operatpr -(const Complex &c);
  }
  Complex operator +(const Complex &a, const Complex&b){
     return ...
  }
  Complex Complex::operator -(const Complex & c){
     return ...
  }
  ```

  重载为成员函数，参数个数为运算符目数减一（因为该函数需要有一个作用的对象）

  重载为普通函数，参数个数为运算符目数
### 赋值运算符

- 赋值运算符只能够重载为成员函数 

  ```C++
  String & operator = (const int _data)
  {
    cout<<"this is ..."<<endl;
    data = _data;
    return *this;
  }
  ```

  说明两点，该返回值是一个对象本身的引用，因为一般时用于初始化另外一个同class的对象

  其次，返回的是*this，对于这个的理解，this是一个指向对象本身的指针，如果函数需要返回对象本身，那么使用 *this 是可以的

  另外写一个有关于字符串的类的class作为参考

  ```c++
  class String{
   private:
     char*str;
   public:
     String():str(new char[1]){str[0]=0;}
      const char * c_str() {return str;};
      String & operator = (const char *s){
          delete [] str;
          str = new char[strlen(s)+1];
          strcpy(str, s);
          return * this;
      };
      ~String(){delete []str;}
  };
  ```

  