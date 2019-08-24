## C++  Tips

### vector

- 向量（Vector）是一个封装了动态大小数组的顺序容器（Sequence Container）。跟任意其它类型容器一样，它能够存放各种类型的对象。可以简单的认为，向量是一个能够存放任意类型的动态数组。

- 函数

  void push_back(const T&x): 向量尾部增加一个元素x

### sort

- sort（begin，end，cmp）， begin 和 end是地址，这个cmp是一个返回布尔值的函数，可以根据自己的排序结构需要进行改写：

  ```C++
  static bool cmp(const vector<int> &a, const vector<int> &b)//根据频率排序
  	{
  		return a[1] > b[1];
  
  ```

### n&1

- 位运算，最低位为1（奇数），则结果为1，最低位为（0），则结果为0

### 二分查找

- lower_bound(起始地址，结束地址，要查找的数值) 返回的是数值 **第一个** 出现的位置。返回**大于或者等于val**的第一个数值

- upper_bound(起始地址，结束地址，要查找的数值) 返回的是数值 **最后一个** 出现的位置。返回**大于val**的第一个数值

- binary_search(起始地址，结束地址，要查找的数值)  返回的是是否存在这么一个数，是一个**bool值**。

### 优先队列

- 头文件 #include<quene>
- top 访问队头元素
- empty 队列是否为空
- size 返回队列内元素个数
- push 插入元素到队尾 (并排序)
- emplace 原地构造一个元素并插入队列
- pop 弹出队头元素
- swap 交换内容

```c++
//升序队列
priority_queue <int,vector<int>,greater<int> > q;
//降序队列
priority_queue <int,vector<int>,less<int> >q;
//默认降序大顶堆
```

