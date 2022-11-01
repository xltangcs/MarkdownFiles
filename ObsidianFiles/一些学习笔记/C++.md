# 第8章 函数探幽
## 8.1 C++内联函数

- 内联函数执行速度更快，但是更加消耗内存
    常规的函数调用是跳转至函数，而内联函数用内联代码替换函数调用

- 使用内联函数需要声明或者定义前加上关键字`inline`
- 类比于 C语言的 宏
    ```c
    #define SQUARE(X) X*X

    inline int SQUARE(int x){return x*x};
    ```

## 8.2 引用变量
- 引用变量的定义
  ```c++ 
  int rats;
  int & rodents = rats;
  ```
    此时rodents作为rats的别名
- 引用常被用做函数参数，这种传递参数的方法称为按引用传递


# 8.3 默认参数
```c++
char * left(const char * str, int n = 1);  //此时n默认为1
```

# 8.4 函数重载
- 函数多态（函数重载）使用多个同名函数
- 以参数列表进行区分

# 8.5 函数模板
-定义交换模板
```c++
template <typename AnyType>
void swap(AnyType &a, AnyType &b)
{
    AnyType temp;
    temp = a;
    a = b;
    b = temp;
}
```

# 第9章 内存模型和名称空间
## 9.1 单独编译
- 自己编写的头文件命名为 "filename.h" 而不是<filename.h>
  
## 9.2 存储持续性、作用域和链接性
## 9.3 名称空间


# 第10章 对象和类
## 10.1 过程性编程和面向对象编程
## 10.2 抽象和类
典型类声明格式
```c++
class ClassName{
    private:
        pass;
    public:
        pass;
};
```

## 10.3 类的构造函数和析构函数
构造函数函数名与类的名称一样，无返回值。
析构函数删除对象。

```c++
class Student{
    public:
        int age;
        Student( );  //构造函数，无返回值
        ~Student( );  //析构函数
        void f( );  //普通函数
}

void Student::f( )
{
    printf("Hello\n");
}

Student::Student( )
{
    age = 18;
}
Student::~Student( )
{
    
    printf("Delete successfully!\n")
}
```

## 继承
```c++
class A{
    public:
        void set(int ii)
        {
            i = ii;
        }
    private:
        int i;
}

class B : public A{
    //  B继承了A，A是父类，B是子类
}
```

# 第11章
# 重载运算符
`operator + ( )` 重载 + 运算符










