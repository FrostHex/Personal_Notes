# C++
--------------------------------------------------

# 1. 常规

## 1.1 头文件
`.h` 的作用包括: 
1. **声明函数和类: ** 使得这些函数和类可以在其他源文件中使用, 而不需要重新定义。这样可以避免代码的重复编写和提高代码的可维护性。
2. **引入常量和宏定义: ** 例如常量、枚举值、宏定义等, 以便在多个源文件中共享使用。
3. **提供接口和模块化: ** 将程序分解成多个模块, 每个模块有自己的头文件和源文件, 便于程序的组织和管理。
4. **提供外部库的接口: ** 用于声明库中的函数、类和常量, 以便用户在自己的程序中使用这些库。

示例: 
1. **声明函数: **
   ```cpp
   // math_utils.h
   #ifndef MATH_UTILS_H
   #define MATH_UTILS_H  //防止头文件被多次包含导致重复定义错误
   
   // 声明一个函数, 用于计算两个整数的和
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
   - `.h`文件在C++中用于声明类、结构体、函数原型、全局变量等。它的主要目的是提供一个接口的声明, 让其他的`.cpp`文件在包含这个`.h`文件时能够知道如何正确地调用这些接口。
   - 可以在`.h`文件中包含函数体, 但这通常不是最佳实践, 除非在以下情况: 
     - **内联函数**: 对于小的、频繁调用的函数, 可以在`.h`文件中声明并定义为内联函数 (使用`inline`关键字) , 这样编译器可能会将函数体嵌入到每个调用点, 以减少函数调用的开销。
     - **模板函数**: 模板函数的定义必须对编译器可见, 通常意味着它们需要在`.h`文件中定义。这是因为模板需要在编译时实例化, 编译器必须能够看到完整的定义。
     - **类成员函数**: 对于类的成员函数, 特别是小的或者是模板成员函数, 可以在类定义内直接定义, 即使这个定义在`.h`文件中。这样做的成员函数自动成为内联函数。
   - 然而, 将函数体放在`.h`文件中有几个潜在的缺点: 
     - **编译时间**: 每次`.h`文件被修改, 所有包含它的`.cpp`文件都需要重新编译, 这可能会显著增加编译时间。
     - **代码组织**: 将函数声明和定义分离 (声明在`.h`文件, 定义在`.cpp`文件) 可以使代码更加清晰和易于管理。
     - **链接错误**: 如果一个非内联函数在多个`.cpp`文件中被包含, 可能会导致链接时重复定义的错误。

2. **声明类: **
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
   // 冒号后是初始化列表, radius 初始化为 r 的值
   
   double Circle::area() {   // Circle::area() 表示这是 Circle类 的成员函数 area()
       return M_PI * radius * radius;   // 成员函数可以访问类的所有变量, 包括private
   }
   ```

3. **声明常量和宏: **
   ```cpp
   // constants.h
   #ifndef CONSTANTS_H
   #define CONSTANTS_H
   
   // 定义一个常量 pi
   const double PI = 3.14159265358979323846;
   
   // 定义一个宏, 用于计算圆的面积
   #define AREA_OF_CIRCLE(radius) (PI * (radius) * (radius))
   
   #endif // CONSTANTS_H
   ```

4. **extern: **
    想在一个源文件中声明一个全局变量或函数, 然后在其他源文件中引用它。\
    `extern` 关键字用于声明一个外部变量或函数, 它告诉编译器该变量或函数是在其他文件中定义的, 需要在当前文件中引用。
    ```cpp
    // example.h
    #ifndef EXAMPLE_H
    #define EXAMPLE_H

    // 声明一个外部变量
    extern int globalVariable;
    #endif // EXAMPLE_H
    ```

    ```cpp
    // main.cpp
    #include <iostream>
    #include "example.h"

    // 使用 extern 声明的全局变量
    extern int globalVariable;

    int main() {
        // 访问外部变量 globalVariable
        std::cout << "Global variable from main.cpp: " << globalVariable << std::endl;
        return 0;
    }
    ```

    ```cpp
    // other.cpp
    #include "example.h"

    // 定义外部变量 globalVariable
    int globalVariable = 42;
    ```
    `example.h` 头文件中声明了一个外部变量 `globalVariable`, 表示它在其他文件中定义 \
    `main.cpp` 使用 `extern int globalVariable;` 声明了外部变量 `globalVariable`, 然后在 `main()` 函数中可以直接访问该变量。 \
    `other.cpp` 定义了外部变量 `globalVariable` 的实际内容, 它的值为 `42`。 \
    这样, `main.cpp` 中就可以使用 `globalVariable`, 而且它的值是从 `other.cpp` 中定义的。


## 1.2 Typedef
定义新的类型别名。一般形式为: 
```cpp
typedef type new_type;
// `type` 是已经存在的数据类型, `new_type` 是别名。
```
示例: 
```cpp
typedef long long ll; // 将 long long 类型定义为 ll

typedef std::vector<int> IntVector; // 将 std::vector<int> 类型定义为 IntVector

// 函数指针
typedef int (*FunctionPointer)(int, int); // int(*)(int, int)定义为 FunctionPointer
```

在上面的示例中, `typedef int (*FunctionPointer)(int, int);` 定义了一个函数指针类型 `FunctionPointer`, 它可以指向一个接受两个 `int` 类型参数并返回 `int` 类型的函数。这样一来, 在需要声明函数指针的地方, 就可以直接使用 `FunctionPointer` 作为类型名, 使代码更加清晰易懂。



## 1.3 函数指针
函数指针是指向函数的指针, 它存储了函数的地址, 可以用来调用该函数。函数指针的类型与函数的类型一致 (参数列表和返回类型) 。


--------------------------------------------------
--------------------------------------------------
# 2. 面向对象
面向对象编程 (Object-Oriented Programming, OOP) 是一种编程范式, 它将数据与操作数据的方法组合成为一个对象, 通过封装、继承和多态等机制来组织和管理代码。
```cpp
// 示例
#include <iostream>
using namespace std;

// 定义一个表示汽车的类
class Car {
private:
    string brand; // 品牌
    string model; // 型号
    int year;     // 出厂年份

public:
    // 构造函数, 用于初始化对象
    Car(string brand, string model, int year) {
        this->brand = brand;
        this->model = model;
        this->year = year;
    }

    // 成员函数, 用于获取汽车的详细信息
    void displayInfo() {
        cout << "Brand: " << brand << endl;
        cout << "Model: " << model << endl;
        cout << "Year: " << year << endl;
    }
};

int main() {
    // 创建两个汽车对象
    Car car1("Toyota", "Camry", 2020);
    Car car2("Honda", "Civic", 2019);

    // 调用成员函数显示汽车信息
    cout << "Car 1 Info:" << endl;
    car1.displayInfo();

    cout << "\nCar 2 Info:" << endl;
    car2.displayInfo();

    return 0;
}

```
## 2.1 定义类 (Class) 
类是面向对象编程的基本单位, 它描述了一类对象的属性和行为。在 C++ 中, 使用 `class` 关键字来定义类, 例如: 
- 类的成员可以是变量,也可以是函数。
- 类的成员变量也叫属性。
- 类的成员函数也叫方法/行为,类的成员函数可以定义在类的外面。
- 用类定义一个类的变量叫做创建(或实例化)一个对象。
- 类的成员变量和成员函数的作用域和生命周期与对象的作用域和生命周期相同。
举例: 
```cpp
class MyClass
{
public:
    string name;
    int age;
    void show(string var)
    {
        cout << "变量为: " << var << endl;
    }
};
```
方法二: 
```cpp
class MyClass
{
public:
    string name;
    int age;
    void show(int var) //在类中只写函数的声明
};

void MyClass::show(int var) // 表示show是MyClass的成员函数, 不是普通函数
{
    cout << "变量为: " << var << endl;
}
```
## 2.2 创建对象 (Object) 

类是抽象的模板, 而对象是类的具体实例。可以使用类来创建对象, 例如: 

```cpp
MyClass obj1;
obj1.setField(42);
std::cout << obj1.getField() << std::endl;
```

## 2.3 封装 (Encapsulation) 

封装是面向对象编程的一种核心概念, 它将数据和操作数据的方法封装在一起, 使得对象的内部细节对外部不可见。在 C++ 中, 可以使用访问修饰符 `private`、`protected`、`public` 来控制成员的访问权限。

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

## 2.4 继承 (Inheritance) 

继承允许一个类 (派生类) 基于另一个类 (基类) 来定义。派生类继承了基类的成员变量和成员函数, 并可以添加自己的新成员。在 C++ 中, 使用 `class` 后跟冒号 `:` 来指定基类。

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

## 2.5 多态 (Polymorphism) 

多态允许同样的方法在不同的对象上表现出不同的行为。在 C++ 中, 通过虚函数 (virtual function) 和纯虚函数 (pure virtual function) 来实现多态。

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

## 2.6 在主函数中使用类

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
# 3. 多线程

## 3.1 join
例如: 
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

    t1.join(); // join() 阻塞当前线程, 直到对应的线程执行完成
    t2.join();

    return 0;
}

// Note:
// 调用了 join() 后线程对象进入了不可结合状态, 再次对相同的线程对象调用 join() 会导致异常
```

## 3.2 detach
`detach()` 将线程对象分离, 使其在执行完毕后自动销毁。这样就可以在循环中多次创建并启动线程
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
        t.detach(); // 分离线程, 使其在执行完毕后自动销毁
    }
    //主线程会迅速结束, 而线程函数 threadFunction 会在后台独立地执行, 直到完成其任务

    return 0;
}
```

## 3.3 原子类型
在多线程编程中避免竞态条件和数据竞争等并发问题 \
无锁, 避免了锁的竞争和开销 \
当一个线程对 std::atomic 类型的变量进行修改后, 其他线程立即可以看到该变量的修改结果
```cpp
#include <atomic>
std::atomic<int> flag(0); // 将flag声明为原子类型, 初始值0
```

## 3.4 线程挂起与唤醒 (优化等待标志位时低效的循环检测)
```cpp
#include <iostream>
#include <thread>
#include <atomic>
#include <chrono>
#include <mutex>
#include <condition_variable>

std::mutex mtx;
std::condition_variable cv;
std::atomic<bool> flag(false);

void waiting_function() {
    // 将 mtx 互斥量上锁, 创建了一个独占锁
    // (创建一个 std::unique_lock类型 的 lock对象, 使用 std::mutex 类型的 mtx 对象进行构造)
    std::unique_lock<std::mutex> lock(mtx);

    // []{ return flag.load(); } 是Lambda表达式, 使用 flag.load() 返回原子变量flag 的值
    // cv.wait(lock, condition) 如果 condition 为 false, 则释放 mtx 的锁并阻塞线程, 直到被 cv.notify_one() 唤醒
    cv.wait(lock, []{ return flag.load(); });

    // 一旦 condition 为 true, 继续执行
    std::cout << "Flag is set to true, continuing..." << std::endl;
}

void setting_function() {
    std::this_thread::sleep_for(std::chrono::seconds(3)); // 模拟一些耗时操作, 阻塞3秒
    flag.store(true); // 将标志位置为true 
    cv.notify_one(); // 通知等待的线程
}

int main() {
    std::thread t1(waiting_function);
    std::thread t2(setting_function);

    t1.join();
    t2.join();

    return 0;
}

```
- 相比于循环检测标志位的方式, 此方法使用 `cv.wait()` 和 `cv.notify_one()` 时, 线程被挂起并且不再消耗 CPU 时间, 直到条件满足并且被唤醒。这避免了循环检测时的持续 CPU 占用
- 在等待期间, 线程会释放互斥量 `mtx` 的锁, 允许其他线程在需要时访问被保护的资源。这样可以避免了循环检测时的等待, 减少了竞争和资源争用。


--------------------------------------------------
--------------------------------------------------
# 4. 顺序容器

## 4.1 vector 示例
vector可在运行时动态地添加或删除元素
```cpp
// 声明和初始化
#include <vector>
#include <iostream>
int main() {
    // 声明一个空的 vector
    std::vector<int> vec1;
    // 创建并初始化一个 vector
    std::vector<int> vec2 = {1, 2, 3, 4, 5};
    return 0;
}

// 访问元素
std::cout << vec2[0]; // 输出: 1
std::cout << vec2.at(2); // 输出: 3

// 向尾部添加元素
vec1.push_back(10);

// 从尾部删除元素
vec2.pop_back();

// 获取元素数量
std::cout << vec2.size(); // 输出: 4
```

## 4.2 常见操作
- `push_back()`: 向尾部添加一个元素。
- `pop_back()`: 从尾部删除一个元素。
- `size()`: 返回元素的数量。
- `empty()`: 判断是否为空。
- `clear()`: 清空所有元素。
- `resize()`: 重新调整大小。
- `insert()`: 在指定位置插入一个或多个元素。
- `erase()`: 删除指定位置或者指定范围内的元素。

## 4.3 迭代器
用来访问容器中的元素。在对容器进行插入或删除操作后, 迭代器可能会失效。

```cpp
// 获取迭代器
std::vector<int> vec = {1, 2, 3, 4, 5};
auto it_begin = vec.begin(); // 指向 第一个元素 的迭代器
auto it_end = vec.end();     // 指向 最后一个元素的下一个位置 的迭代器

// 遍历元素
for (auto it = vec.begin(); it != vec.end(); ++it) {
    std::cout << *it << " ";   // *it 解引用迭代器, 访问当前迭代器指向的元素
}

// 遍历元素 (范围-based for循环) (foreach 循环)
for (int element : vec) {   // 每次迭代时, 容器 vec 中元素的拷贝到 element
    std::cout << element << " ";
}

// 移动迭代器
++it; // 将迭代器向后移动一个位置
--it; // 将迭代器向前移动一个位置

// 比较迭代器 (在容器中的位置)
std::vector<int>::iterator it1 = vec.begin();
std::vector<int>::iterator it2 = vec.end();
bool isEqual = (it1 == it2);
bool isLess = (it1 < it2); // it1靠前, 返回true
```

```cpp
// 用 -> 访问迭代器指向的元素的成员 (通常用于指向对象的迭代器) 
#include <iostream>
#include <vector>

struct Foo {
    int value;
    Foo(int v) : value(v) {} 
    // 构造函数 Foo
    // : value(v) 是成员初始化列表, 传入的整数参数 v 用于初始化成员变量 value
};

int main() {
    std::vector<Foo> foos = { {1}, {2}, {3} }; // {1}, {2}, {3} 为三个Foo类型的对象
    auto it = foos.begin(); // it 指向容器中第一个元素 {1} 的位置
    std::cout << it->value << std::endl; // 输出迭代器所指向的元素的 value 成员, 即输出 1
    return 0;
}
```

```cpp
// 在迭代器失效后需要重新定义迭代器
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};

    // 获取迭代器指向的元素
    std::vector<int>::iterator it = vec.begin() + 2;
    int element = *it;
    std::cout << "Element pointed by iterator: " << element << std::endl; // 输出3

    // 在第三个位置前插入一个元素
    vec.insert(vec.begin() + 2, 10);

    // 重新定位迭代器
    it = vec.begin() + 2;

    // 获取迭代器指向的元素
    element = *it;
    std::cout << "Element pointed by iterator after insertion: " << element << std::endl; // 输出10

    return 0;
}
```


--------------------------------------------------
--------------------------------------------------
# 5. 泛型算法
可以用于不同数据类型的算法

## 5.1 示例
```cpp
// std::sort 排序
#include <iostream>
#include <algorithm>
#include <vector>

int main() {
    std::vector<int> numbers = {4, 2, 5, 1, 3};
    std::sort(numbers.begin(), numbers.end()); // 排序, 接受两个迭代器参数表示排序的范围
    for (int num : numbers) {
        std::cout << num << " "; // 输出排序后的数组 1 2 3 4 5
    }
    std::cout << std::endl; // 输出换行符
    return 0;
}
```
## 5.2 常见的泛型算法
- **排序算法**: 如 `std::sort`、`std::stable_sort`。
- **查找算法**: 如 `std::find`、`std::binary_search`、`std::count_if`。
- **算术算法**: 如 `std::accumulate`、`std::inner_product`、`std::transform`。
- **集合操作算法**: 如 `std::merge`、`std::set_union`、`std::set_intersection`。
- **堆操作算法**: 如 `std::make_heap`、`std::push_heap`、`std::pop_heap`。
- **遍历和修改算法**: 如 `std::for_each`、`std::transform`、`std::replace`。


--------------------------------------------------
--------------------------------------------------
# 6. 动态内存 (智能指针)
智能指针 可自动化管理内存的功能

## 6.1 std::unique_ptr
- 一种独占式智能指针, 它确保了在任何时候只有一个指针可以管理给定的资源。
- 离开作用域时, 它所管理的资源会被自动释放。
- 不能被拷贝, 但可以通过移动语义来转移所有权。

## 6.2 std::shared_ptr
- 共享式智能指针, 资源可以被多个指针共享。
- 内部使用引用计数来跟踪共享的资源, 当引用计数为零时, 资源会被释放。
- 支持拷贝构造和赋值操作, 会增加引用计数。

## 6.2 std::weak_ptr
- 也是共享式智能指针, 但它不会增加资源的引用计数。
- `std::weak_ptr` 可以从 `std::shared_ptr` 构造而来, 用于解决 `std::shared_ptr` 的循环引用问题。
- `std::weak_ptr` 可以通过 `lock()` 方法获取一个指向资源的 `std::shared_ptr`, 但在获取之前需要检查资源是否还存在, 因为资源可能已经被释放。
```cpp
// 解决ab循环引用
#include <memory>

class B;  // 前置声明

class A {
public:
    std::shared_ptr<B> b_ptr;
};

class B {
public:
    std::weak_ptr<A> a_weak_ptr; // 若 std::shared_ptr<A> a_ptr; 则会循环引用, 引用计数无法归零. 内存泄漏
};

int main() {
    std::shared_ptr<A> a = std::make_shared<A>();
    std::shared_ptr<B> b = std::make_shared<B>();

    a->b_ptr = b;
    b->a_weak_ptr = a;

    // 在需要访问 a 所指向的资源时, 先通过 lock() 方法获取一个指向资源的 shared_ptr (若资源不存在则返回空的 std::shared_ptr)
    if (auto locked_a = b->a_weak_ptr.lock()) {
        // 使用 locked_a 访问资源
    } else {
        // a 已经被释放了, 处理资源不存在的情况
    }

    return 0;
}
```