# · 常规
## 头文件
`.h` 的作用包括：
1. **声明函数和类：** 使得这些函数和类可以在其他源文件中使用，而不需要重新定义。这样可以避免代码的重复编写和提高代码的可维护性。
2. **引入常量和宏定义：** 例如常量、枚举值、宏定义等，以便在多个源文件中共享使用。
3. **提供接口和模块化：** 将程序分解成多个模块，每个模块有自己的头文件和源文件，便于程序的组织和管理。
4. **提供外部库的接口：** 用于声明库中的函数、类和常量，以便用户在自己的程序中使用这些库。

示例：
1. **声明函数：**
   ```cpp
   // math_utils.h
   #ifndef MATH_UTILS_H
   #define MATH_UTILS_H  //防止头文件被多次包含导致重复定义错误
   
   // 声明一个函数，用于计算两个整数的和
   int add(int a, int b);
   
   #endif // MATH_UTILS_H
   ```

   ```cpp
   // math_utils.cpp
   #include "math_utils.h"
   
   int add(int a, int b) {
       return a + b;
   }
   ```

2. **声明类：**
   ```cpp
   // circle.h
   #ifndef CIRCLE_H
   #define CIRCLE_H
   
   // 声明一个圆类
   class Circle {
   private:
       double radius;
   
   public:
       Circle(double r);
       double area();
   };
   
   #endif // CIRCLE_H
   ```

   ```cpp
   // circle.cpp
   #include "circle.h"
   #include <cmath>
   
   Circle::Circle(double r) : radius(r) {} 
   // Circle::Circle() 表示这是 Circle类 的构造函数
   // (double r) 表示这个构造函数接受一个 double 类型的参数 r
   // 冒号后是初始化列表，radius 初始化为 r 的值
   
   double Circle::area() {   // Circle::area() 表示这是 Circle类 的成员函数 area()
       return M_PI * radius * radius;   // 成员函数可以访问类的所有变量，包括private
   }
   ```

3. **声明常量和宏：**
   ```cpp
   // constants.h
   #ifndef CONSTANTS_H
   #define CONSTANTS_H
   
   // 定义一个常量 pi
   const double PI = 3.14159265358979323846;
   
   // 定义一个宏，用于计算圆的面积
   #define AREA_OF_CIRCLE(radius) (PI * (radius) * (radius))
   
   #endif // CONSTANTS_H
   ```



--------------------------------------------------
--------------------------------------------------
# · 面向对象
面向对象编程（Object-Oriented Programming，OOP）是一种编程范式，它将数据与操作数据的方法组合成为一个对象，通过封装、继承和多态等机制来组织和管理代码。

## 1. 定义类（Class）
类是面向对象编程的基本单位，它描述了一类对象的属性和行为。在 C++ 中，使用 `class` 关键字来定义类，例如：
- 类的成员可以是变量,也可以是函数。
- 类的成员变量也叫属性。
- 类的成员函数也叫方法/行为,类的成员函数可以定义在类的外面。
- 用类定义一个类的变量叫做创建(或实例化)一个对象。
- 类的成员变量和成员函数的作用域和生命周期与对象的作用域和生命周期相同。
举例：
```cpp
class MyClass
{
public:
    string name;
    int age;
    void show(string var)
    {
        cout << "变量为：" << var << endl;
    }
};
```
方法二：
```cpp
class MyClass
{
public:
    string name;
    int age;
    void show(int var) //在类中只写函数的声明
};

void MyClass::show(int var) // 表示show是MyClass的成员函数，不是普通函数
{
    cout << "变量为：" << var << endl;
}
```
## 2. 创建对象（Object）

类是抽象的模板，而对象是类的具体实例。可以使用类来创建对象，例如：

```cpp
MyClass obj1;
obj1.setField(42);
std::cout << obj1.getField() << std::endl;
```

## 3. 封装（Encapsulation）

封装是面向对象编程的一种核心概念，它将数据和操作数据的方法封装在一起，使得对象的内部细节对外部不可见。在 C++ 中，可以使用访问修饰符 `private`、`protected`、`public` 来控制成员的访问权限。

```cpp
class MyClass
{
public:
    int a
private:
    int b
};

int main()
{
    MyClass obj;
    cout << obj.a << endl; //可以
    cout << obj.b << endl; //会报错
}
```

## 4. 继承（Inheritance）

继承允许一个类（派生类）基于另一个类（基类）来定义。派生类继承了基类的成员变量和成员函数，并可以添加自己的新成员。在 C++ 中，使用 `class` 后跟冒号 `:` 来指定基类。

```cpp
class BaseClass {
public:
    void baseMethod() {
        std::cout << "Base method" << std::endl;
    }
};

class DerivedClass : public BaseClass {
public:
    void derivedMethod() {
        std::cout << "Derived method" << std::endl;
    }
};
```

## 5. 多态（Polymorphism）

多态允许同样的方法在不同的对象上表现出不同的行为。在 C++ 中，通过虚函数（virtual function）和纯虚函数（pure virtual function）来实现多态。

```cpp
class Shape {
public:
    virtual void draw() const {
        std::cout << "Drawing shape" << std::endl;
    }
};

class Circle : public Shape {
public:
    void draw() const override {
        std::cout << "Drawing circle" << std::endl;
    }
};

class Rectangle : public Shape {
public:
    void draw() const override {
        std::cout << "Drawing rectangle" << std::endl;
    }
};
```

## 6. 在主函数中使用类

```cpp
int main() {
    MyClass obj;
    obj.setField(42);
    std::cout << obj.getField() << std::endl;

    DerivedClass derivedObj;
    derivedObj.baseMethod();
    derivedObj.derivedMethod();

    Shape* shape1 = new Circle();
    Shape* shape2 = new Rectangle();
    shape1->draw(); // 调用 Circle 类的 draw 方法
    shape2->draw(); // 调用 Rectangle 类的 draw 方法

    delete shape1;
    delete shape2;

    return 0;
}
```



--------------------------------------------------
--------------------------------------------------
# · 多线程

## join
例如：
```cpp
#include <iostream>
#include <thread>

// 线程函数
void threadFunction(int n) {
    std::cout << "Thread " << n << " is running" << std::endl;
}

int main() {
    // 创建线程并启动
    std::thread t1(threadFunction, 1);
    std::thread t2(threadFunction, 2);

    // 主线程继续执行其他操作
    std::cout << "Main thread is running" << std::endl;

    t1.join(); // join() 阻塞当前线程，直到对应的线程执行完成
    t2.join();

    return 0;
}

// Note:
// 调用了 join() 后线程对象进入了不可结合状态，再次对相同的线程对象调用 join() 会导致异常
```

## detach
`detach()` 将线程对象分离，使其在执行完毕后自动销毁。这样就可以在循环中多次创建并启动线程
```cpp
#include <iostream>
#include <thread>

void threadFunction() {
    // 线程任务
    std::cout << "Thread is running" << std::endl;
    std::this_thread::sleep_for(std::chrono::seconds(1));
}

int main() {
    int numThreads = 3; // 设置要创建的线程数量

    for (int i = 0; i < numThreads; ++i) {
        std::thread t(threadFunction);
        t.detach(); // 分离线程，使其在执行完毕后自动销毁
    }
    //主线程会迅速结束，而线程函数 threadFunction 会在后台独立地执行，直到完成其任务

    return 0;
}
```

## 原子类型
在多线程编程中避免竞态条件和数据竞争等并发问题 \
无锁，避免了锁的竞争和开销 \
当一个线程对 std::atomic 类型的变量进行修改后，其他线程立即可以看到该变量的修改结果
```cpp
#include <atomic>
std::atomic<int> flag(0); // 将flag声明为原子类型，初始值0
```
