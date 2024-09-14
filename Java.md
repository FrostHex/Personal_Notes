# Java
--------------------------------------------------

# L03 Java History And Basics

## 3.1 主类需要与文件名一致
```java
// Myprogram.java
public class Myprogram{
    // methods (similar as functions in C)
}
```

## 3.2 Compile in CMD
```shell
javac 文件名.java
# 编译为.class文件

javac *.java
```

## 3.3 Run
```shell
java 文件名
```

## 3.4 main() Method
```java
public static void main (String[] args)
```
- **method name**: main means the entry point for the program 
- **static**: means there's a single instance of the method and it's associated with the class rather than individual objects
- **access restrictions**: public means it's globally accessible 
- **type of value returned by method**: void means it returns nothing 
- **command line arguments**: accessed as an array of Strings (more later)

## 3.5 打印
print 在现在这行打印 \
println 换行打印


--------------------------------------------------
--------------------------------------------------
# L04 Nuts and Bolts

## 4.1 命名
Varable & Method: start with lower case, like myVariable \
Class: start with upper case, like MyProgram

## 4.2 类型的兼容
小的类型可以直接用于大的类型, 比如float变量可以直接参与double类型的运算, 反之不行(需要类型转换) \
byte < short < int < long < float < double
```java
public double squareX(int x) { return x*x; } // valid
public int squareY(double y) { return y*y; } // invalid
```

## 4.3 强制类型转换 Type Casting
eg: `(int)1.3` 丢弃小数

## 4.4 自增
a = b++ 先赋值再自增
```java
public class Test {
    public static void main(String args[]){
        int a = 0;
        int x = a++ + 5;
        System.out.println(x); //x为5
    }
}
```

## 4.5 Continue
跳过本次循环体中剩下尚未执行的语句, 立即进行下一次的循环条件判定


--------------------------------------------------
--------------------------------------------------
# L05 Object 

## 5.1 Structure of Class
1. Class Name
2. Attributes (states)
3. Operations (behaviours) (Written by methods)

## 5.2 Object
- Object is defined by a class 
- Class defines attributes and operations 
- An object is an instance of a particular class 
- Object stores attributes and operations
- A class only exists at compile time
- An object only exists at runtime

## 5.3 Abstraction
为几个相似的subclass抽象出一个super class \
subclasses inherit the methods form the super class
```java
public class ParticularShape extends Shape{
    // ...
}
```

## 5.4 Method
```java
// modifier returnType methodName()
public int methodName(int x, int y){
    // ...
}
```

## 5.5 Stack 栈
方法执行时, 占用stack \
计算完后空间释放


--------------------------------------------------
--------------------------------------------------
# L06 

## 6.1 Create Instance
occupy the space of heap (堆)
- `Cat myCat` allocate space for reference variable of type Cat called myCat
- `new Cat()` allocate space for a new Cat object on the heap
```java
Cat myCat = new Cat();
```

## 6.2 Encapsulation 封装
public protected default private
1. Private (类访问级别) : 表示私有的, 被private修饰的成员, 仅能包含该类的其他成员访问, 任何其他类都不能访问, 即private成员只能在类的内部使用。
2. Default (包访问级别) : 如果一个类或类的成员不使用任何访问控制修饰符, 则称它为默认访问控制级别, 这个类或类的成员只能被本包中的其他类访问。
3. Protected (子类访问级别) : 被protected修饰的类的成员, 既可以被同一个包中其他类访问, 也可以被不同包中的子类访问。protected比默认访问权限的访问范围要宽。 (protected=默认权限+不同包中的子类) 
4. public (公共访问级别) : 是最宽松的访问级别权限, 如果一个类或者类的成员被public访问控制符修饰, 那么这个类或者类的成员能被所有的类访问, 不管访问类和被访问类是否在同一个包中。


--------------------------------------------------
--------------------------------------------------
# L07

## 7.1 初值
Java automatically sets some initial values for you for variables of the class (instance variables), **but not for variables in methods**. 
- boolean: `false` 
- char: `'\u0000'` 
- byte, short, int, long: `0` 
- float / double: `+0.0f` / `+0.0d` 
- object reference: `null`

## 7.2 Heap 堆
![Life_on_the_heap]
b 储存着对第一个Rabbit对象的引用 \
c 和 d 同时储存着对第二个Rabbit对象的引用 \
( 通过d修改对象的属性后, 通过c访问对象时, 访问到的也是修改后的结果 )

## 7.3 Method Overloading 重载
define same method with different parameter list
```java
public int run(int duration, boolean zigzag) {...}
public int run(int duration){...}
// Both of these methods can exist in the class Rabbit.
// Which one is called depends on how you call it, e.g.
// ...
int distance = bugs.run(5, true); 
// OR 
int distance2 = bugs.run(5);
```
```java
// 错误, 传参列表不能完全相同
run (int dur){...}
run (int dis){...}
```

## 7.4 Constructor
等效于python的__init__, 类的初始化方法 \
Constructor 的名字必须与类的名字一致
```java
public class RaceCar {
    private String bodyColour;
    public RaceCar(String input) {   // Constructor
        this.bodyColour = input;
    }
}
```


--------------------------------------------------
--------------------------------------------------
# L09 Array
provides fast random access by using index position 

## 9.1 Declaration
```java
typeName arrayRef[];
// or
typeName[] arrayRef;

// eg. Sting[] args
```

## 9.2 Using New to Create
```java
int[] nums = new int[7]; // an array is an object

MyClass array[0] = new MyClass(); // fill the first place in array with a MyClass object
```

## 9.3 Exception
- ArrayIndexOutOfBounds
- NullPointerException

## 9.4 Method Overriding 重写
redefine the inherited method for particular subclass
```java
// default:
for (int i = 0; i < rabbit_array.length; i++) {
    System.out.println(rabbit_array[i]); // call the default toString() method
}

// output:
// Rabbit@3e25a5
// Rabbit@923e30
// Rabbit@9cab16

// toString() 方法被定义在内置的 Object Class 中, 我们定义的类都是它的子类
// 打印 object 程序会自动调用 toString() 方法, 可以在我们的类中重写此方法以自定义打印内容
```
```java
// override:
public class Rabbit {
    // ...
    public String toString() {
        return this.getName() + " is a " + this.getFurType() + 
        " Rabbit that runs at " + this.getSpeed() + " km/hr.";
    }
}
```

## 9.5 Java Docs
```shell
# create the docs subfolder
javadoc -d docs file.java
```


--------------------------------------------------
--------------------------------------------------
# L11 ArrayList
ArrayList can enlarge or shrink
```java
// define
ArrayList<Flower> myList = new ArrayList<Flower>(); // <Type>
```
## 11.1 Add Element
.add()是引用传递, 将对象的引用添加到列表中
```java
Flower f = new Flower();
myList.add(f); 
// r 和 myArrayList 的第一个位置都存储着新对象的引用
```

## 11.2 Compare ArrayList with Array
```java
// create
String[] my_array = new String[6];
ArrayList<Type> my_array_list = new ArrayList<Type>();

// assign an object
my_array[0] = b;
my_array_list.add(b);

// get an object
my_array[4];
my_array_list.get(4);
```

## 11.3 Convert Int to String
```java
b = "" + 3; // "3"
c = "" + 3 + 1; // "31"
```


--------------------------------------------------
--------------------------------------------------
# L12 Inheritance

## 12.1 Aggregation 聚合
eg. The Car object **has** (contains) four Tire objects.
```java
public class RangeRover {
    public Tire[] array = new Tire[4];
    // array是长度为4的Tire类型的数组
    // 之后可以如 array[0] = new Tire();
    public void drive() {
    // do driving things ... 
    }
}
```

## 12.2 Inheritance 继承
- **Subclasses inherit the properties (attributes and operations) of their superclass.**
- private instance variables and methods are not inherited

eg. The class BlueCar **is** a subclass of the superclass Car
```java
public class Car {   // the superclass
    public String bodyColour;
    public void drive() {
    // do driving things ... 
    }
}

public class BlueCar extends Car {   // the subclass
    // ...
}
```

## 12.3 Polymorphism 多态
Using a single definition (superclass) with different types (subclass)
```java
public class Creature(){
    // ...
}

public class Turtle extends Creature{
    // ...
}

public class Rabbit extends Creature{
    // ...
}

Creature aCreature = new Creature();   // valid
Creature aCreature = new Turtle();   // also valid
Creature aCreature = new Rabbit();   // also valid
// creature reference can put a creature object, a turtle object, or a rabbit object
```

## 12.4 Abstract Class
abstract class cannnot be instantiated
```java
public abstract class Creature(){   // abstract class
    // ...
}

public class Turtle extends Creature{
    // ...
}

Creature aCreature = new Turtle();   // valid
Creature aCreature = new Creature();   // not valid
```
**concrete class**: non-abstract class is called 

## 12.5 Abstract Method
abstract method must be overridden in the concrete child class (if the subclass is abstract then it's fine)
```java
public abstract class Creature { 
    // ...
    public abstract int run(int duration, boolean zigzag);   // run() is a abstract method
}

public class Turtle extends Creature{
    // ...
    public int run(int duration, boolean zigzag) {   // must override run() method in subclass Turtle
        // ...
    }
}
```
if a class contains at least one abstract method, then the class must be abstract

## 12.5 Mega Class
`java.lang.Object` is the ultimate parent of EVERY class in java. \
It is implicitly inherited by every class. 

## 12.6 State
the value of the instance variable

## 12.7 Convert & Override
```java
// override equals() method
public boolean equals (Object o){
    Rabbit r = (Rabbit)o;
    if(r.getRabbitSpeed() == this.getRabbitSpeed())
        return true;
}

// 这个类和这个类的子类 的对象才能转换为这个类的类型
// e.g.
// A类
// |
// B类 (是A的子类) 
// |
// C类 (是B的子类) 
//
// C obj = new C();
// A a = (A) obj;
// 只有A和A的子类可以转换成A
```
## 12.7 Call the Parent Class Method after overriding
```java
public class ParentClass{
    public void method(){
        // ...
    }
}

public class SubClass extends ParentClass{
    public void method(){   // overriding
        // ...
    }
    super.method();   // call the method defined in ParentClass
}
```


--------------------------------------------------
--------------------------------------------------
# L14 Interface

## 14.1 Example
```java
public interface Flyable {
    public abstract void fly(); // OR public void fly(); 
    // Even if you don't declare the method abstract or public, it is!!!
    // Interface cannot be instanciated: e.g. Flyable a = new Flyable() // Error
}
```
```java
public interface Walkabe {
    public abstract void walk(); 
}
```
```java
public class FlyingSquirrel extends Creature implements Flyable, Walkabe {
    public void fly() //must provide implementation (method body), as you "said" you are Flyable
    {
        // some code
    }
    public void walk() 
    {
        // some code
    }
}
```
## 14.2 Notes
- A subclass can extend **one** superclass but implement **many** interfaces
- An interface may have many methods. If a class implements an interface, but only implements some of its methods (that is, create definition of the method), then this class becomes an abstract class; it cannot be instantiated.
- If you don't provide any method implementation, then it's better to use an interface instead of an abstract class.

## 14.3 Extending the Interface
```java
interface Father 
{
    int age = 30;
    void wash();
}
interface Mother 
{
    long bank_account = 100000;
    void cook();
}
interface Child extends Father, Mother
{
    void cry(boolean tear);
} // Child has age, bank_account, cook(), wash(), cry()
```
- If Father interface and Mother interface have the same methods:
  - different parameters: ok, it's overloading
  - differ by only return type: error
  - identical: only keep one
- If Father interface and Mother interface have the same variables:
  - ok, use Father.variable or Mother.variable to refer one of them


--------------------------------------------------
--------------------------------------------------
# L16 Garbage Collection

## 16.1 Heap & Stack
They are the main areas of memory.
- Heap: 
  - Garbage-collectible
  - where objects live
- Stack: 
  - where local variables and methods, when called, live
  - Method at top of the Stack is always the method being executed
  - ![Example_of_the_Stack]

## 16.2 Variables
- Local Variables:
  - goes on the **Stack**
  - Variables declared in a method and method parameters.
  - Temporary variables, alive only when the method they belong to is on the Stack.
  - The local object reference variable goes on the stack, and the object it refers goes on the Heap
- Instance Variables:
  - goes on the **Heap**
  - Variables declared in a class (not inside of a method).
  - Live inside the object they belong to.

## 16.3 Overloaded Constructors
```java
public class Account 
{
    public Account() 
    {
        // ...
    } 
    public Account(int balance) 
    {
        // ...
    }
    public Account(int balance, boolean giveOverdraft) 
    {
        // ...
    }
    public Account(boolean junior, int balance) 
    {
        // ...
    }
}
```

## 16.4 Constructor Chaining
When a new object is created, all the constructors in its inheritance tree must be run. \
The constructor of the superclass will run first implicitly
```java
public class BigCat {
    public BigCat() 
    {
        System.out.println("Making a BigCat");
    }
}
public class Tiger extends BigCat {
    public Tiger() 
    {
        System.out.println("Making a Tiger");
    }
}
public class TestTiger {
    public static void main(String[] args) 
    {
        System.out.println("Starting ...");
        Tiger myTiger = new Tiger();
    }
}
// Output:
// Starting ...
// Making a BigCat
// Making a Tiger
```

## 16.5 Using Superclass Constructor in Subclass
- `super()`, and can use parameters in the bracket
- If call super() explicitly, super() must be the first statement in a constructor.
```java
public Dog(int dogWeight) {
    weight = dogWeight;
    super();  // Wrong
}
```

## 16.6 Using this() for Overloaded Constructor
```java
public class Tiger()
{
    public Tiger()
    {
        this(5);
    }

    public Tiger(int a)
    {
        System.out.println(a);
    }
}
```

## 16.7 Life of Objects and Variables
- object: lives when its reference lives
- instance variable: lives when object they belong to lives
- local variable: lives when:
  - being in scope, or
  - out of scope but the method where it was declared is in stack
```java
public class ExampleGoneWrong {
    public void method1() 
    {
        int x = 10;
        method2();
    }
    public void method2() 
    {
        x = 20; // x is still alive since method1 is still in the stack, however x is out of scope so it's an error
    }
}
```


--------------------------------------------------
--------------------------------------------------
# 17 String

## 17.1 Example
```java
// Different from other object:
String s1 = "Sherlock";
String s2 = s1;
s2 = "Holmes"; 
System.out.println(s1);  // Sherlock
System.out.println(s2);  // Holmes
```

## 17.2 Elements of String  
starts at `0` and ends at `length() -1`

## 17.3 Operations
```java
String s = "HelloWorld!";
System.out.println(s.length());  // 11
c = s.charAt(5);  // c = 'W'
c = s.indexOf('W')  // c = 5, returns ch's first occurrence position (int); if not found, returns -1.
if (s.equals("abc")) // false
```
- `compareTo(str)`: compares two strings, returns int that is <0, >0, =0
    ```java
    String str1 = "abc";
    String str2 = "aef";
    int result = str1.compareTo(str2); // 从第一个字符开始比较字典序, b 在 e 前, 返回负数
    ```
- `substring(index1,index2)`: returns the substring between index1 and (excluding) index2.
    ```java
    String s = "HelloWorld!".substring(1,6); 
    // S = "elloW";
    ```
- `concat(s)`: concatenates two strings.
    ```java
    String s = "Hello".concat("World"); // s = "HelloWorld"
    ```
- `toUpperCase()` / `toLowerCase()`: convert all characters in string to 
upper/lower case.
    ```java
    String sUpper = "Cat".toUpperCase(); // sUpper = "CAT"
    String sLower = "Cat".toLowerCase(); // sLower = "cat"
    ```
- `toString()`: convert input to a string.
    ```java
    double d = 12.3;
    String dString = Double.toString(d); // dString = "12.3"
    ```
- `split(String s)`: splits the string around matches of the given regular expression s and returns an array with those substrings.
    ```java
    public class UsingSplit 
    {
        public static void main(String[] args) 
        {
            String str = "bar:foo:bar";
            String[] splitStr = str.split("a");
            for (int i=0; i < splitStr.length; i++)
                System.out.println(splitStr[i]);
        }
    }
    // b
    // r:foo:b
    // r
    ```
- `void getChars(i,j,A,k)`: returns characters from i to j (excluding), and stores them into array A starting from A[k].
    ```java
    char[] A = new char[4];
    "The rain in Spain".getChars(4,8,A,0);
    // A = {'r','a','i','n'}
    ```
- `substring(index)`: returns substring from index to end.
    ```java
    String s = "Monkeys".substring(3); // s = "keys"
    String s = "Monkeys".substring(3,"Monkeys".length()-1); 
    // s = "key"
    ```
- `replace(oldCh,newCh)`: replace oldCh by newCh everywhere in the string.
    ```java
    String s = "goose".replace('o','e'); // s = "geese"
    ```

## 17.4 Character class
- static methods:
  - `isLetter(char c)`
  - `isDigit(char c)`
  - `isUpperCase(char c)`
  - `isLowerCase(char c)`
```java
// e.g.
Character myCharacter = new Character('c');
myCharacter.compareTo(new Character('f')); // returns -3
myCharacter.compareTo(new Character('a')); // returns 2
myCharacter.equals(new Character('e')); // returns false
Character.isLetterOrDigit(new Character('?')); // returns false
```

## 17.5 String Tokenizer
- old fashion. We should use split() instead.
```java
String s = "I am from Portugal.";
// Create a StringTokenizer.
StringTokenizer my_tokenizer = new StringTokenizer(s);
System.out.println("Number of tokens is " + my_tokenizer.countTokens() + ".");
while (my_tokenizer.hasMoreTokens())
    System.out.println(my_tokenizer.nextToken());

// Number of tokens is 4.
// I
// am
// from
// Portugal.
```
```java
StringTokenizer my_tokenizer = new StringTokenizer(s, "ru"); // seperate with 'r' and 'u'
// Number of tokens is 4.
// I am f
// om Po
// t
// gal.

StringTokenizer my_tokenizer = new StringTokenizer(s, "ru", true); // don't discard 'r' and 'u'
// Number of tokens is 7.
// I am f
// r
// om Po
// r
// t
// u
// gal.
```

## 17.6 The Format Specifier
```java
String.format("I have %,6.2f bugs to fix", 12345.6789);
// I have 12,345.68 bugs to fix
```
- % [argument_number$] [flags] [width] [.precision] type
  - argument_number$: which argument it refers to, if there’s more than one
  - flags: special formatting options, e.g. inserting commas, putting negative numbers in parentheses, left/right alignment
  - width: minimum number of characters used
  - .precision: number of decimal places
  - type: 
    - %d – decimal
    - %f – floating point
    - %x – hexadecimal
    - %c – character

--------------------------------------------------
--------------------------------------------------
# L19 Numbers

## 19.1 Final
- **Final variable**: Cannot be changed once initialized.
- **Final method**: Cannot be overridden in a subclass.
- **Final class**: Cannot be inherited.

## 19.2 Static
- **Static variable/method**: All objects share the same copy of the variable/method (class-wide global).
- **Static variable/method**: Can be called without an object, directly using the class name.

    ```java
    public class Math extends Object {
        public static float PI = 3.141592f;
        static double random() {
            // ...
        }
        // ...
    }
    ```
    ```java
    // Usage:
    Math.random(); // Call this method directly
    float p = Math.PI;

    // If the random() method is not static, we have to use an object to call this method
    Math m = new Math();
    m.random();
    ```

- Static Method
  - Static methods cannot access non-static methods.
  - Static methods can be accessed by subclass but cannot be overridden.
  - (Three types of variables: local ~, instance ~, static ~) 
  - Static methods can access the variables:
    - static variable
    - local variable that is declared inside
    - (cannot access the instance variable and outside non-static variable)

    ```java
    public class Parent {
        public static void print() {
            System.out.println("Parent");
        }
    }

    public class Child extends Parent {
        public static void print() {
            System.out.println("Child");
        }
    }

    public class Test {
        public static void main(String[] args) {
            Parent p = new Child();
            p.print();  // prints "Parent", since static method print is bound with Parent class when compiling

            Child c = new Child();
            c.print(); // prints "Child", not override
        }
    }
    ```

- Static Variable
  - Static variables are created and initialized with the class (before any object is created).
  - If a static instance variable changes, all of the objects will access the modified value.

## 19.3 Constant
**Static final**: Declares a constant.

```java
// e.g.
static final int MY_VARIABLE;
```

## 19.4 Math Method
```java
double rnd = Math.random() * 5.0; // returns 0.0 ≤ rnd < 5.0

double absNum = Math.abs(-123.45); // returns absNum = 123.45

int roundedValue;
roundedValue = Math.round(-10.8f); // -11
roundedValue = Math.round(-0.5); // 0
roundedValue = Math.round(0.5); // 1

double minValue = Math.min(123.45, 123.46); // returns minValue = 123.45

double maxValue = Math.max(123.45, 123.46); // returns maxValue = 123.46
```

## 19.5 Random Class
```java
import java.util.Random;
public class RandTest {
    public static void main(String[] args) {
        Random r = new Random();
        float aRandomFloat = r.nextFloat();
        int aRandomInt = r.nextInt();
        System.out.println("A random float is " + aRandomFloat);
        System.out.println("A random int is " + aRandomInt);
    }
}
```

## 19.6 Wrapper Classes
- (e.g. Character) used when variable of a primitive type (e.g. char) needs to be treated as an object.
- Wrapper classes are part of `java.lang` package (no need to import them explicitly).

## 19.7 Wrapping & Unwrapping
```java
int i = 10;
Integer iWrapped = new Integer(i);
int unWrapped = iWrapped.intValue();
```

## 19.8 Autoboxing
- Conversion from primitive type to wrapper object is automatic after Java 5.0.

```java
// After Java 5.0
public void doNumsNewWay() {
    ArrayList<Integer> listOfNumbers = new ArrayList<Integer>(); // ArrayList<int> is invalid
    listOfNumbers.add(3);
    int one = listOfNumbers.get(0);
}

// Before Java 5.0
public void doNumsOldWay() {
    ArrayList listOfNumbers = new ArrayList();
    listOfNumbers.add(new Integer(3));
    Integer one = (Integer) listOfNumbers.get(0);
    int oneUnwrapped = one.intValue();
}

// After Java 5.0
void takeMyNumber(Integer i) {
    // ...
}
int x = 1;
takeMyNumber(x); // valid due to autoboxing
```

## 19.9 Static Methods in Wrappers
```java
// Convert a `String` to a primitive value.
String str1 = "10";
String str2 = "123.45";
String str3 = "true";

int i = Integer.parseInt(str1); // i=10
double d = Double.parseDouble(str2); // d=123.45
boolean b = new Boolean(str3).booleanValue(); // b=true
```

## 19.10 Static Imports
Import a static method or variable to save on typing.
```java
import java.lang.Math;
class BeforeStaticImports {
    public static void main(String[] args) {
        System.out.println("square root is " + Math.sqrt(4.0));
    }
}
```
```java
import static java.lang.System.out;
import static java.lang.Math.*;

class WithStaticImports {
    public static void main(String[] args) {
        out.println("square root is " + sqrt(4.0));
    }
}
```

## 19.11 Abstract Class Number
Number \
  ├── Byte \
  ├── Short \
  ├── Integer \
  ├── Long \
  ├── Float \
  └── Double
```java
Number num = new Integer(10);
```
```java
System.out.println(Long.MIN_VALUE); // –2^63
int i = 181;
System.out.println("Hex value = " + Integer.toHexString(i));
```

## 19.12 Immutable
Classes like `Character`, `Byte`, `Short`, `String` define immutable objects (their content cannot be changed).

```java
String s = "Hello"; // the content of s cannot be changed
s = s + " World"; // will create a new String object rather than changing it
```

## 19.13 Recursion
Methods that call themselves. Without recursion, iteration can be used to solve the problem.

--------------------------------------------------
--------------------------------------------------
# L20 Exception Handling

## 20.1 Syntax for try/catch/finally Blocks
```java
try {
// code that can throw exceptions E1, ..., En
// statements in this section will end halfway if it encounters an exception
}
catch (E1 e1) {
// code to handle exception E1
}
// ...
catch (En en) {
// code to handle exception En
}
finally {
// it will execute regardless of whether or not an exception is thrown
}
```

## 20.2 Example
```java
public class RiskyClass {
    public void checkFileName(String s) throws Exception 
    {
        if (s.equals("/etc/passwd"))
        throw new Exception("bad filename");
    }
}
```
``` java
// Method 1: try + catch
public class TestExceptions{
    public static void main(String[] args) 
    {
        RiskyClass rc = new RiskyClass();
        for(int i = 0; i < args.length; i++) 
        {
            try {
                rc.checkFileName(args[i]);
            } // end try
            catch (Exception e) {
                System.err.println(""+ e + " at "+ i);
            }
        }
    }
}
// java TestExceptions /etc/passwd
// java.lang.Exception: bad filename at 0
```
```java
// Method 2: throw exception in main method
public class TestExceptions {
    public static void main(String[] args) throws Exception
    {
        RiskyClass rc = new RiskyClass();
        for (int i = 0; i < args.length; i++) 
        {
            rc.checkFileName(args[i]);
        }
    }
}
// java TestExceptions /etc/passwd
// Exception in thread "main" java.lang.Exception: bad filename
```

## 20.3 Creating Exception Classes
```java
public class MyException extends Exception 
{
    public MyException() 
    {
        super(); // call constructor of parent Exception
        // other appropriate code
    }
    public MyException(String s) 
    {
        super(); // call constructor of parent Exception
        // other appropriate code
    }
}
```
```java
public class MyDate {
    // ...
        if (a < 0) {
            throw new MyException();
        }
    // ...
}
```
```java
public class TestMyDate {
    public static void main(String[] args) throws MyException {
        MyDate d = new MyDate(-1980);
    }
}
```

## 20.4 Example
```java
try {
    statement1;
    statement2;
    statement3;
}
catch (Exception1 ex1) {
    // ...
}
catch (Exception2 ex2) {
    // ...
}
statement4;
```
- If an exception is thrown in statement1 or statement2, statement3 will not be executed. If no exceptions are thrown in statement1 or statement2, statement3 will be executed.
- If the exception is not caught, then the program will terminate and statement4 will not be executed.
- If the exception is caught in one of the catch clauses, the program will go on and statement4 will be executed.

## 20.5 Checked & Unchecked Exceptions
![Checked&UncheckedExceptions]
- Run-Time Exceptions: e.g. NullPointerException, ArrayStoreException, IndexOutOfBoundsException .etc

## 20.6 Example
![ExceptionsEx2] \
// test = "no": \
start try \
start risky \
end risky \
end try \
finally \
end of main

## 20.7 Assertion
- Can be used for internal checks.
- Syntax:
  - `assert expression`
  - `assert expression : detailMessage`
    ```java
    // e.g.
    assert i == 10;
    assert (sum>10 && sum<500) : "sum is" + sum;
    // if (i == 10) or (sum>10 && sum<500) is not met, java.lang.AssertionError will be thrown
    ```

## 20.8 Enable Assertion
- disable assertion
  - java 文件名
  - java -da 文件名
- enable assertion
  - java -ea 文件名
```java
public class Foo 
{
    public void m1(int value) 
    {
        assert 0 <= value;
        System.out.println("OK");
    }

    public static void main(String[] args) 
    {
        Foo foo = new Foo();
        System.out.print("foo.m1(1): ");
        foo.m1(1);
        System.out.print("foo.m1(-1): ");
        foo.m1(-1);
    }
}

// java Foo
// foo.m1(1): OK
// foo.m1(-1): OK

// java -ea Foo
// foo.m1(1): OK
// foo.m1(-1): Exception in thread "main" java.lang.AssertionError
```


--------------------------------------------------
--------------------------------------------------
# L21 File I/O

## 21.1 data form
- for human: text
- for computer: byte

## 21.2 Stream
A stream is a connection to a source of data or to a destination for 
data (sometimes both). Stream is a sequence of bytes and can represent any data

## 21.3 Methods in File
- `File(String pathname)`: creates file with specified pathname
- `boolean exists()` / `boolean isDirectory()` / `boolean isFile()`
- `boolean canRead()` / `boolean canWrite()`
- `boolean delete()`: returns true if file successfully deleted
- `String getAbsolutePath()`: returns complete absolute file/directory name
- `boolean renameTo(File dest)`: returns true if operation successful
- `long length()`: returns length of the file in bytes
- `String[] list()`: returns an array of strings containing the list of files in this directory
- `boolean mkdir()`:  returns true if folder successfully created

## 21.4 FileReader
- Constructor:
  - `public FileReader(String filename)`
  - `public FileReader(File file)`
- Methods:
  - `int read()`: read the next character 
  - `int read(char[] cbuf)`
  - `int read(char[] cbuf,int off,int len)`
  - `void close()`

## 21.5 Example of Read
```java
File file = new File("temp.txt");
FileReader in = new FileReader(file);
```
```java
import java.io.*;
public class FileReadTest 
{
    public static void main(String args[])
    {
        String fileName = "input.txt";
        String contents = "";
        try 
        {
            FileReader file_reader = new FileReader(fileName);
            BufferedReader buffered_reader = new BufferedReader(file_reader);
            String one_line = buffered_reader.readLine();
            while (one_line != null) 
            {
                contents = contents + one_line + "\n";
                one_line = buffered_reader.readLine(); // get one line of text
            }
            buffered_reader.close();
            file_reader.close();
        }
        catch (IOException ex) 
        { // file does not exist or not readable
            System.out.println("Errors occured");
            System.exit(1);
        }
        // It's ok but it's better to catch(FileNotFoundException ex2) as well
        System.out.println(contents);
    }
} 
```
## 21.6 FileWriter
- Constructor:
  - `public FileWriter(String filename)` 
  - `public FileWriter(File file)`
  - `public FileWriter(String filename, boolean append)`
  - `public FileWriter(File file, boolean append)`
- Methods:
  - `void write(int c)`
  - `void write(byte[] cbuf)`
  - `void write(char[] cbuf,int off,int len)`
  - `void write(String str)`
  - `void write(String str, int off,int len)` 
  - `void close()`
```java
FileWriter fw = new FileWriter("myFile.txt");
// Create a new FileWriter object to write data to myFile.txt.
// if the file myFile.txt does not exist, it will be created
// if the file myFile.txt exists, it will be overwritten (equivalent to delete and rewrite)
```

## 21.7 Example of Write
- `flush()` method of buffered writer ensures that data from previous calls to write() is sent to disk and leaves the file open.
```java
import java.io.*;
public class UsingFlush 
{
    public void write_to_file(String filename)
    {
        BufferedWriter buffered_writer = null;
        try
        {
            buffered_writer = new BufferedWriter(new FileWriter(filename));
            buffered_writer.write("Writing line 1 to file");
            buffered_writer.newLine(); // new line
            buffered_writer.write("Writing line 2 to file");
        }
        catch(FileNotFoundException ex) {ex.printStackTrace();}
        catch(IOException ex) {ex.printStackTrace();}
        finally
        {
            // close the buffered writer
            try
            {
                if(buffered_writer != null)
                {
                    buffered_writer.flush(); // ensures that data from previous calls to write() is sent to disk and leaves the file open
                    
                    // write more text to the output stream
                    buffered_writer.newLine();
                    buffered_writer.write("Writing line 3 to file");

                    buffered_writer.close(); // this method also includes flushing the stream
                }
            }
            catch (IOException ex) {ex.printStackTrace();}
        }
    }

    public static void main(String[] args) 
    {
        UsingFlush obj = new UsingFlush();
        obj.write_to_file("output.txt");
    }
} 
```

--------------------------------------------------
--------------------------------------------------
# L22 Collections & Sorting

## 22.1 Collection Framework: Interfaces
- Set: A collection that **contains no duplicate elements**; it models the mathematical set abstraction.
- List: An ordered collection (also known as a sequence). Elements can be accessed by their position in the list, and it is possible to search for elements in the list. Lists **allow for duplicate elements**.
- Map: An object that maps keys to values. A map does not contain duplicate keys; each key can map to at most one value.

## 22.2 Map
- cannot contain duplicate keys
- each key maps to one value only
```java
import java.util.*;
public class HashMapTester {
    public static void main( String[] args ) 
    {
        Map<String, String> petSounds = new HashMap<String, String>();
        petSounds.put("cat", "Meow"); petSounds.put("mouse", "Squeak");
        petSounds.put("dog", "Woof"); petSounds.put("guineaPig", "Squeak");
        System.out.println("map = " + petSounds);
        String val = (String)petSounds.get("dog");
        System.out.println("Value for key 'dog' is: " + val);
    }
}
// map = {mouse=Squeak, cat=Meow, dog=Woof, guineaPig=Squeak}
// Value for key 'dog' is: Woof
```

## 22.3 Iterator
- bool `it.hasNext()`: return true if there are more elements for the iterator
- object `it.next()`: returns the next object
- object `it.remove()`: removes the most recent element that was returned by **next**. If the collection does not support remove(), an UnsupportedOperationException will be thrown .
```java
// ...
    ArrayList<String> alist = new ArrayList<String>();
    // Add Strings to alist
    for (Iterator<String> it = alist.iterator(); it.hasNext(); ) 
    {
        String s = it.next(); // No downcasting required.
        System.out.println(s);
    }
// ...
```

## 22.4 2D Array & ArrayList
```java
// e.g.
int[][] nums = new int[5][4];
Square[][] board = new Square[2][3]; // stores the references to objects
```
```java
nums = new int[][]; // ILLEGAL
nums = new int[5][]; // OK
nums = new int[5][4]; // OK
```
```java
ArrayList<ArrayList<Integer>> myList = new ArrayList<ArrayList<Integer>>();
```

## 22.5 Bubble Sort
loop: switch the place of two adjacent numbers if the order is wrong
```java
    void bubble_sort_method_1(double[] list)
    {
        int n = list.length;
        for(int i = 0; i < n - 1; i++)
        {
            for(int j = 0; j < n - i - 1; j++)
            {
                if(list[j] > list[j + 1])
                {
                    double temp = list[j];
                    list[j] = list[j + 1];
                    list[j + 1] = temp;
                }
            }
        }
    }
```
```java
    void bubble_sort_method_2(double[] list)
    {
        boolean changed = true;
        do
        {
            changed = false;
            for(int i = 0; i < list.length -1; i++)
            {
                if(list[i] > list[i+1])
                {
                    double temp = list [i];
                    list[i] = list[i+1];
                    list[i+1] = temp;
                    changed = true;
                }
            }
        }
        while(changed);
    }
```

## 22.6 Comparable
```java
// in order to sort by salary
public class Employee implements Comparable<Employee> 
{
    int empID;
    String eName;
    double salary;
    static int i;
    public Employee() 
    {
        empID = i++;
        eName = "unknown";
        salary = 0.0;
    }
    public Employee(String name, double sal) 
    {
        empID = i++;
        eName = name;
        salary = sal;
    }
    public String toString() 
    {
        return "EmpID = " + empID + "\n" + "Ename = " + eName + "\n" +
        "Salary = " + salary;
    }
    public int compareTo(Employee o1) 
    {
        if (this.salary == o1.salary) return 0;
        else if (this.salary > o1.salary) return 1;
        else return -1;
    }
}
```
```java
import java.util.*;
public class ComparableDemo 
{
    public static void main(String[] args) 
    {
        List<Employee> ts1 = new ArrayList<Employee>();
        ts1.add(new Employee("Tom", 40000.00));
        ts1.add(new Employee("Harry", 20000.00));
        ts1.add(new Employee("Maggie", 50000.00));
        ts1.add(new Employee("Chris", 70000.00));
        Collections.sort(ts1);
        Iterator <Employee> itr = ts1.iterator();
        while(itr.hasNext()) 
        {
            Object element = itr.next();
            System.out.println(element + "\n");
        }
    }
}

// EmpID = 1
// Ename = Harry
// Salary = 20000.0

// EmpID = 0
// Ename = Tom
// Salary = 40000.0

// EmpID = 2
// Ename = Maggie
// Salary = 50000.0

// EmpID = 3
// Ename = Chris
// Salary = 70000.0
```
```java
// if sort by name:
// Employee.java:
public int compareTo(Employee o1) 
{
    if (this.eName.equals(o1.eName)) return 0;
    else if (this.eName.compareTo(o1.eName) > 0) return 1;
    else return -1;
}

// EmpID = 3
// Ename = Chris
// Salary = 70000.0

// EmpID = 1
// Ename = Harry
// Salary = 20000.0

// EmpID = 2
// Ename = Maggie
// Salary = 50000.0

// EmpID = 0
// Ename = Tom
// Salary = 40000.0
```






--------------------------------------------------
--------------------------------------------------
[Life_on_the_heap]:data:image/jpeg;base64,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9jPeT7vKt42kfaMnAGTiqPhrXYfEug22rwQvDFc7iiOQWADFecfSgDVooooAKKKKACiiigAooooAKjuIEubeW3lG6OVCjD1BGDUlFAGL4Qmebwpp/mnMkUXkOf8AajJQ/qtbVYXgvnwpZv8A89TJJ/31Izf1rdoAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigArybULzxI/jxPEC+Eb11to2hWHaSHHzDdux716zRW1Gr7Nt2vfQicOZWucB4p8M3csdr4q0G0ez1iELJLbIOZAeoIHUjofUVl+K4tf8RWek6teeH7n7LbSMLnTVchzyPm6ZwRx04/GvU6K0hiXG2l7benYl0k767njWs21zr2jyRaN4ANiiYzOY/3vUcKMAn368Vr3epeI7jwENG/4RK9DtF9lL8kgBR823Gef8mvTqKt4q6S5dnfdkqjZ3ueX+HvE3iLwtolvpuo+FL2dY1/cSRgg7Sc4YYPNWNNtvENxrV743v8ARpFlig8uz09TiRx0/kSenPpXpFFS8Sm21FJvfcapWSV9EeQeG77xT4Z1HUtSk8L3ktpey75YtpDIckgjjnqR0rSvzrvxFvrK2fRptL0u2lEsstx958dhkDtnp616bRTeKTlzqK5u+ovYu1r6HMeIvEutaRqC22n+GLnUoTGG8+NjjPpwDXFeE9R8T+F4LyIeEL65+1TmbO1l2+33TXrlFRCvGMHHkWu+5Uqbbvcgs5pLmyhmmga3kkQM0THJQkcg/SvMtDv9Z8BXGo2Fx4cu75bi5MsU0GdrD8jXqlFRTqqF01dMcoXtrqjmvDGseI9Xu55dU0VdNsdo8kOx8wtnuPTHsK6WiionJSd0rFRTS1dwoooqCgooooAKwPEQ+w6hpWtLwIJxbTn1ilIXn6PsP51v1n6/YHU9Av7ID5poHVPZsfKfzxQBoUVR0W//ALU0Sxv+9xAkh+pAz+tXqACiiigAooooAKKKKACiiigCvqFmuoafPZvJJEs8ZQvE21lz3BryLw/4Sh1XxJrWmXGsX0UWnSbY3EuC3JHOfpXsNxcQ2tvJcXEixRRqWd2OAoHc14xp9j4b8R+NNa/tPUzDHNcZtHilCCUsx6ZBz2rvwbkozs7K3a5z17aepuaJPc+GviBbaDYa1Jq1jcofNjd95hOCevYjHbsa6zxR4xh8NTQW/wDZ13e3FwpZEgXjj3rjNDjj+Gnix7LVY4msr4fuNRKYZQOxPYeo+hqx4i8S3us+LBotprsWjackSyC73YMwIByG/HjkdDWs6aqVIu11bfa/3fluRGXLF9HfY2dP+I6S6nb2GraJeaS1022F5uVY9uwrK+L2l2MenW+qi3UXjzrG8wzkqAeK5TXja2Wr6Yi+LZNaWK5V5N5JWEZGTuyR+XpXT/FXXNK1Hw9Zw2d/BcO06yhI3ySmGGfzq40lCrTlTW/r+oudyjKMi6vxSBi8+28N6hPYpw1yOBgdTjBH61qapPoXjTwVcX6ItzHDFJJGHyGikCnr6GrGmeL/AAquhwPFqVpBAkQHkswDIAPu7etcR4ZvbS00XxVftItnpt+7x2SyHbvbD8KPoRWPs07uMXFp/fr/AFsWpNWu7ph4L8df2T4bt9Ks9FvNSuYi7yCEYVQWJHOD/Ku58MeNdP8AEsktskUtpfQjMltOMMB6j1rl/hb4g0Gx8ONZ3F3BaXglZpfNYKZB2IJ68cUG7tNd+Ltjc6EwlS2hP2ueL7jcEde/UCtK1OM6k0423dyKcnGCd/kavjbxRptq8uj6poF9f2wVZHdFxGe45z2rf8K3dnfeGbK40+2a1tWQiKFjkoASMfpWP4z8TaH/AMI/q2mjVLf7X5Dx+SH+bdjp9aqeAfE+h2vhTTNPn1S3jugChiZ8MCXOB+orndNvD3UXe/n23Nea1TV9C38Rdf8A7K0KayWzu5WvYHUTRL8kXGPmPbrXN+FfiGNK8NWVi+ialdGFCvnRplW5PQ/pXc+MlZ/B2rKgLE2r8D6VgeBfEuiWPgiwiutVtYZIUYOjygMp3E9OtVScfq792+v+Yp39otbaf5HYafeDUNPgvBDLAJkD+XKuHXPYj1rK8a+JV8J+F7nVvLEsqYSGM9GdjgZ9u/4Vc0TxBpviG3luNMnM0cUhjZthXn8a5v4t6Tdat4EuFs42lltpUuNijJZV64/A5/CuGonFtNWOiGvmZ9n4W8d6npiandeNJ7PUJkEqWsUI8mPIyFI/+t+dLpPiq98Q+A/Ednq8Sx6rpcM0FzsGA52thgO3Q/lWzpXxF8L3fh6LUZdXtrfbEDLDI4Do2OV29Tz6da4/wpFPfeHPHHiZ4Xht9WErW4cYLIqvz/49j8DUz+0ulhx6PrcZ4A8P+K9d8GWUkfiSXRrKJWS0itogWf5jl3Oeec8e1dN4G8Satc32reGvEEiS6npJBFwgx50Z6Nj16fmKz/hj410KLwNaWV/qMFlcWKFZEuHCErkkMM9QQe1N8CufEHjnxL4st0YadMi21tIy483aACR/3yPzqpbv0ZK2RF4R8a3enfCzUPEOrXEt9Pb3MiR+a+Sx+UKufTJpLCw8T61pyarffEJNPvLhBJHaQbPKiB5CsM8+/wDWuf0XSLnWvgVqdvZo0k0d88yooyWClSQPwzWl4e074T6l4dgvbuKztp0iH2mKa5dHRwOeN3PPTFLv8vyH/wAH8zo/CXjya58P6y+ueU19oJYXLwEbZgAcMMcc4IrN0LT/ABn4300a/c+KZtHiuctaWlpGNqrkgFjkZqLQNN0bxD4L8Sp4W0CTTorqNoIZnlZhdFckEA9P/r1pfDzxpoUXgy0sdQ1GCwu9OjMNxDcuI2UqSM4PXij/AIAEE0HizUvAutWHiGeeyuNP3mO9t9oF7GFbgj0PfgdR71N8HtKuLfwlaai+q3U8NxEwSzcjy4SJDyv1x+tS2Xiq78YeHPFE8VkqaZDFLFZTjO64+VsnB/D86d8IdVsLnwLp9hDeQvd26OZoA43p+8bBI/EULr8v1B9Pmd3RRRQAUUUUAFFFFABRRRQAVHcSCG2llPRELH8BUlZfia4Fp4X1Sf8AuWkpH12nFAEXg+Iw+D9IQ9fscZP4qD/WtmqumWxs9KtLU9YIEj/JQP6VaoAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKK5Pxb45h0O4j0nS4P7S124IENknO3PdyPujHP/1uasaXZ+MLhfN1nVrO0z/ywsLfcV+rvnP5UAdJRXMa94c1e506c6d4p1G3n8tsbliZW46YCgj6g1xPwY1rXHb7Fqs8s1jdRSPZPI2470f94ueufnzzQB67RRRQAUUUUAFFFFABRRRQAUUUUAYPg/8Ad6NLZ97K8uIPoBIxX/x0it6sLQP3WseILbst8so/4HEhP6g1u0AFFFFABRRRQAUUUUAFFFFAEVxbw3dvJb3ESyxSqVdGGQwPY1kQ+C/DVvMk0Wi2iyRsGVgnQjoa3KKqM5R2dhNJ7lPUtI07WIFg1Gziuo1bcqyLnB9ap6j4S0HVYYYrzTIXWBAkWAVKKOwIwce1bFFCnKOzBpPcwx4L8NC1S1/sa1MSHcAUyc+pPU0sngzw1KIw+i2h8pdifu+g9P1rboqva1P5n94uSPY52bwD4WnuftD6NBvJyQpKqf8AgIOK0bvQNIvrGKxudOt5LaE5jiKDan0HatGih1Ju129A5Yroc9P4D8LXMSRvo1uqp93YCh/MHmtPS9F03RYDBptnFbIxy2wct9T1NXqKTqTas27AoxTukYtz4O8OXlzJc3Gj2sk0rbncpyx9abF4K8MwTJNFotorxsGVtnQjoa3KKftalrcz+8OWL6CEBgQQCDwQe9c7J8P/AArLcmdtGh3k5IBYL/3yDiujoqYzlD4XYbinuiCzsrXT7dbezt47eFeiRqFH6VPRRSbb1Y9jCn8E+F7m8N5NoNi85O4sYRyfUjoa15bS3ms3s5IUNu6GNosYUqRjGPTFTUUvIDDn8FeGLmGCGbQ7KRLZdsQaIfKM5xn0pviDX9F8FaIkl2BbWx/dQxwRcZwSAAOnSt6msqsMMoI9xSeqsCOH+D1hc2PgSNrqF4WubiSZFcYO04AOPfFb134J8L312bu60KxlnY5ZzCMsfU+tbdLVMCOCCG2hSGCJIokGFRFCqo9ABWVqPhDw5q139rv9Fs7ic9ZHiG4/U9/xrZopARQW0FtbrbwQxxQoNqxooCgegAqhpvhnQ9HvZbzTdLt7SeUFXeJNpYE5x+dalFABRRRQAUUUUAFFFFABRRRQAVg+Lj5+nW2mDltRvIoCB/cDb3/DYrVvVz8B/tfxhLcDm20eMwIezTvgvj/dXaPqxoA6CiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACuJ+IPjW60KEaVoNrJe61cplUijL+Qh43kAfkP8AJ6jWNSGl6e06x+bM5EcEIODLI3Cr+fX0GT2rjriDxRoOoLb6RpP26e/jM17qhK/NOeAvzH5Y144weOnOaAMf4e6R4m0hZbyTwmrahdEtPf6hfBZHzzgKFJArvpJ/EyxFk0/THcfwfbJBn8fLrH1XU/GR8QppmnadELbyEJvQ6bS5xuLKTkKOeAMnjmqHjnxd4k0m9az0SzzOHRYY2spJjdAjJYOMKoB4weT7UAR6z8Sda8Ph01vwZd28RBAube4E0eceoUD8zXMauLjwl8HPDc1u7QaoLtbiF1HzKXDsR/3yQCO9ei62bzUfDNlpV5GsV9q3lw3EcZyEGN02PYKGH1Irm/FtgPFfxH0Xw5ECtlpMRu7vZwFzjYv14GP96gDr/DviGz1XTbZZNTsZ7/y1FwkEwOJMfMMdetbdeQan8A4GZpdJ12WJs5C3MYb/AMeXH8qzP+EQ+K/hjnS9SkvIk6LDc7xj/ckoA9yorw5fix478Pt5fiDQhIq9Wlt2hJ/EfL+ldBpnx40C5wuo6fd2TdyuJVH5YP6UAeo0VzumeP8Awpq+Baa5aFz0SV/Lb8mxXQI6yIHRgynkEHINADqKKKACiiigDC075PGmtJ2e3tZPx/eL/wCyit2sLTPm8Za4/wDdhtY/yDn/ANmrdoAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAoopCQqlmIAAySe1AGXr+qSabZIloiy392/k2kR6M57n/ZUZY+wqfR9Mj0fTIrJHaQrlpJW+9K5OWY+5JJrM0BP7Yvp/Ek+WWQtDp4I4SAH74Hq5Gc+m2uhoAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAoorB8aa6/h/wzc3cA3XcmILRO7SucL+Wc/hQBSGq2lzrd3rV/cxwaVpDG1tnc4V5zxI49SOEH/AqzYbXTtPn1fWovEs8M1/mxjEsTAxz5yPkPLuMjGAOO1UJdR8HHR4/B19C2pjTZIYrjbIFJnZsEr8wZzuLE7c96n8Sz+ELGbT/Dd94fElhFeJBGySBfKlcBgdoO4jDDLe/egCl4W8NXul6b/bd94lsXFoLgW07xFMzNuQtNI+GbByMHP6CrXw/wBA8SR3Meqalqv2jdK7yXEeotcR3SEEBQmNq4bnOc8YxTPHXiHw/pWlppp0y7NlZTfZjJYypF5TFDlFBOW+UnPGOeua07u5t9L0vSPB3hiJrW41GLKg53WkB5klbP8AFyQM/wAR9qANaC9gnur7xHcN/oNlG8FseuQp/eOPXLAKP933pfCOjTWNvdapqCY1TVpftFznrGP4I/oq4H1zT0gtp72DQ7RAtjpSxtMo6bgP3cf4Y3H/AID61vUAFFFFADWRXUq6hlPUEZFYGp+AfCmr7jd6HaFm6vEnlt+a4roaKAPL9T+A+gXOW06/u7Jj0ViJVH54P61zzfCbx14ffzPD+vLIAchYp3hJ+qnj9a9xooA8N/4S34seGONT02W7iXq01sJB/wB9x/1NaWm/H2DIj1fQpYmBwz20gb/x1sfzr2Cs3UvDmiaupGo6VaXOf4pIVLfn1oA5/TPix4N1PAGrC1c/w3SGP9en611Vpf2d/H5lndw3Cf3opAw/SuG1P4K+Eb/c1tFc2DnvBKSv5Nn9K5W7+BerWEpn0HxCu8cqJA0TD/gSk/0oA9O0D97rPiC47NfLGP8AgEMY/nmt2vn/AEiT4q6DZm805Li9tJpGckKtwJGBwWx97nb1rVtfjlrOnSiDX/Dy7x12FoW/JgaAPa6K890z41+Er7aty9zYMevnRbgPxXNddpviXQ9YA/s7VrS5J6LHMC35daANSiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACimu6Rrud1VfVjgVEt7as21bmEn0EgoAnooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiisa+8SQRXT2GnW8mp368NBbkbYv+ujn5U/Hn2NAGu7pGjSSMqIoyzMcAD1Nc1NcS+MGNpZF49Ezi4uwdpux3jj77T3fv0HrU66Bd6tIs/iS4S4RTuTT4Mi3U/7WeZD9ePat9VCqFUAADAA6CgBI40ijWONQiIAqqowAB0Ap1FFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRWd4g1ePQNAvdWlQutrEZNgONx7D8TigCDxD4r0XwtbJPq94sHmZEaBSzuR6AVzY+JdzfjOh+EtVvUPSaYLBGfxNZOhaYuoi38V6zKmo6nfR+bAW5itYyAAqpjG7jk461vM7OcuxY+5oApP4o8d3AHk6NpFkD/AM/F2ZCP++a5LXNR8V6x4u0fS9Q1LSY5LdzdwmFCyK65xuU8seOBXaXVwlpaTXMmNkMbO2fQDNeaabHot1AbXxLZTaXfSym5h1HeQH38giToO3HT8aAO3g8P3a3smoyarZRalIcm7g0iPzAe5BJ6n1xSy+H57rW4NYvNWS4vYD+7nk02MlR24B7ds9Kpf2gumQxpL4rhuAwJQvAkkhAHJ+U84Hcim317p01qDdeJLuSN1BCWS7WYH/cUt+tAFXxMG0q8fW7rW9KubyFd0YvdNjMzEdANp5PocVW0zXfE/h+G88aahDptxNqSIWE7usip/DGgAwM8HFYutWWiyaZJHY+G9QhM8iINSvCU2sWAzliSfpWjpbP4z8UxFd39h6JhYVPSVwMKT69M/Qe9AHZ+Fdb1vSNO2ah4dkuJbmVri4nt7qNnZ3OeUYg8DAwD0Fdrpmt2GrKRbTYlX78Eg2Sx/wC8p5Fc1VW+sReKrxytb3UR3QXMf3429vUeo6GgDv6K53wT4gm8QaIz3gUX1pM1tdbBhS6/xD2Iwa6KgAooooAKKKKACiiigArP17URpWh3d6Pvxxnyl6lpDwij3LED8a0KwL8f2r4sstP62+nJ9tnHYyElYgfph2/4CKANDQ7D+y9CsbA9beBEY+pA5/XNWLqxtL6IxXlrDcIeqyxhx+RqeigDjtT+FPg3U8ltJW2c/wAdq5jx+A4/SuR1L4BWxJfSdclhbqEuIw3/AI8uP5V6/RQB4b/wh3xW8Mc6Vqcl3EnRYbreMf7kmKVfit498PNs8QaEJFXq01u0JP4j5f0r3GmsqupV1DA9QRkUAeX6Z8edBuMLqOnXdk3dkxKo/kf0rr9M+IHhPV9otNctd7dElby2/JsU7U/AXhXV8m80O0LN1eNPLb81wa5DU/gR4fuctp19eWTHorESqPzwf1oA9OR0kQPGyurchlOQadXhz/CXxx4ffzPD+vLIAchYp3gY/VTx+tJ/wlfxZ8L8alp0t3CvVprYSD/vuP8AqaAPcqK8e074+whvL1fQpI2BwzW0mcf8BbH8667TPiz4N1PA/tUWjn+G6Qx/r0/WgDs6Kr2eoWWoR+ZZXcFyn96KQOP0qxQAUUUUAFFFFABVLUtXsNIhWW+uViDnCLyXkPoqjlj7AVnXmtXV7eyaXoCxyzxHbcXcgJhtT6cfff8A2R07kVUv/D9ppuk3F27yXd/JsEt5OcyOCwyo7Kv+yuBQBaF/4h1T/kH6dHpkB6T6iN0h+kSnj/gTD6Uv/CMy3PzaprmpXZPVI5fs8f4CPB/Mmq3he7mgggtppWkhlLrEXOSpUnAyexA/T3rp6BtNbmGngzw2jbjo9vI396YGQn8WzUzeFPDrLg6Fp2Pa2Qf0rWooEYP/AAhehJzbWslk3960uJIT/wCOsKP7H1yx503XmnUf8sdSiEoP/A12sPxzW9RQBgDxNJp7CPxBp8mnDOPtSt5tsT/vjlf+BAfWt1JEljWSN1dGGVZTkEexpWVXUqwDKRggjINc/LoNzpEjXXhp0hBO6TTpCRby/wC7/wA829xx6jvQB0NFZ2ka1bavE4RXguYDtuLWUYkhb0I9PQjg9q0aACiiigAooooAKKKKACiiigAooooAxvF1xLa+FNRlgkMcnklVdTgruO3PtjOa0NP0+00uzS0sbdIIUHCoMfifU+9N1XT49V0q60+UkJcxNGSOoyMZqp4c1KTUdLC3QC31q3kXcf8AdlXqfoeGHsRQBrUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABWF42tLe98F6tBdNKsJtmZzEAW+X5uM/St2q99bi70+4tmGRNEyH8QRQB4no0Pijw/o9lLpb2+t6VcxebBGzbJYwTyvPTBzxzzWknxAtbc7NY0rUNNcdTJCWX8xVbwDdNJ4UWykJ8ywuZImB7AnI/XNdLvbbtzlfQ8igCkfEXhjXrKWzOq27R3CFHRpPLYg9ucGsrSNM1zw9I0FjPBrmkMfkieYCSL6E5B+n8q1LrRdIvc/atKtJCe/lAH8xWa/gfw6x3RWk1u3rDcMtAF280jTtTuIrq78KyyTRDC5MYH44bB/GrNzJ4lmUR6dZWOnr/wA9LiTzGA9lUY/Wsb/hDbdP9TrGrxDsFuuB+lIfClyAQviXVgp7GUGgCxJ4Fk1K4huNd1u61FonDmEqEiPttHSt21ttJ8PWXkQfZ7K3DFsM4UZPU5Jrmv8AhDkb/Xa5q8meoNzgGpIPBOgQtvks2uX/AL1xKz/pQBoXXjjRIZPJtZpNRuD0is0MhP4jis++1HxHeWklxcND4c09Fy8kh8ycj2HQGtu2ggso/LtIIrdPSJAv8q5P4mXGzw5HFuOZZwOvUAE0AegfCu302Pw20+kyzS28shJeb7zvnkmu3ri/hLZmz+HmngjBl3S/ma7SgAooooAKKKKACiiigArB8Lf6Wuoaw3J1C7cxn/plH+7T/wBBJ/4FRr9zPeXMPh6wkaOe7UvczIebe3BwxB7M33V/E9q2LW1gsrWK1tolihhQJGijhQOAKAJqKKKACiiigAooooAKKKKACiiigDN1Hw7ourqRqOlWl1nvJCpb8+tcjqfwW8IX+5reG4sHPeCUlfybP6Yr0CigDxW8+BWq2Mpn0LxCu4cqJVaJh/wJSf5Cq/l/GPwt91rm/hX0K3II/H5q9yooA8TtfjjrenSiDX/DyFh12boW/Js1naT8aL+y8WXl3dRyT6PeTbhbMcvAOgKn6DkdD7V7hq1imoabcQG3t55GjYRidAy7scZyDxmvJtL+AA4bV9cz6x2sX/szf4UAes6Tq9hrmnRahptylxbyj5XU9D6Edj7VmaneXWr6g+h6VM0Kxgfb7xOsIPSNP+mhHf8AhHPUisi18Nab4Asvs3hxZ31LU3EEInmLqWxkuy9MKMkkDtjvXU6RpcGj6dHZwln25aSV/vSueWdj3JPNAE1hYWumWUdnZwrDBEMKi/z9z796x/FExP2a1B+UkyuPXbgD9Tn8K6CuY8Rn/iZc9Bbr/wChNQBT0tjcaW0KHE1tIQp9CDuU/wAv1rSvfG+iafDG09wzysoZool3snsewNck4vJLhoLB5d9yApji6vjvnsOetVr/AMAeIPs5eCC3Y4z5ayjP64H60krGk5KSR2WlfEDw7q14LOK8ME7cKlwuzd9D0rpa+X9Ygube6kguIHgniOHjdcMpr0r4e+Pr+20wW/iSCcWES/udTkU7QP7rE9fYjNMzPVqKgs7y21C0ju7OeO4glGUkjYMrD2NT0AFFFFAGRrOjPeSR6hp8q2uqW4xFMR8si945B3Q/mDyKm0XV01e0ZzEbe5hby7m2c/NDIOoPqO4PcEGtGuf1+GTSrtfEtmhYwJsv4kHM0HrjuycsPbcO9AHQUUyKVJoklicPG6hlZTkEHoRT6ACiiigAooooAKKKKACiiigArB1ixurG+GvaVEZZ1QJd2q/8vUQ6Y/2152+vI7jG9RQBWsL+21OxivbOUSwTLlWH8j6EdCO1Wa5u/jfwxfy6xaoW0y4bdqECjPlN/wA91H/oQ7jnqDnoo5EljWSNw6OAyspyCD0IoAdRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAeI6An9neNfFOkdAt15yD23H+jCumrC16P8As742TfwrqFoD/vHb/wDYVu0AFFFFABRWRquvfYrpLG0tmu7xxny16KPeqU3ibUbAoNR0cxCRgFZZOP610Rw9SSTS380ZyqxjudJRRRXOaBXn3xQlMk2m2SclizY9zgCvQa4HxBbnVPidpdjjcFEeR7ZJoA9z8OWYsPDthagY8qBRj8K06bGoSNUHRQBTqACiiigAooooAKiurmGztZbq4cJDChd2PZQMk1LXO6451u/Tw5bjdGCk2oydo4gciP8A3nIxj+7k+lAE3hi1mNpLq94hW91RhM6nrGmP3cf/AAFevuWrcoooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiis3xDqD6XoF7eRDMscREQ9ZDwo/76IoAo6OP7W16+1p/mhgZrKy9Nqn964+rjGfRBXQVS0fTl0nR7TT0ORbxKhb+8QOT+Jyau0AFcp4mkivp0jhJ/dBklcdGBxlR6nI69ua3NVnkWNLaFirzE5YdVQdT9eg/GufvlCrtUYA6CgClpI/0m8ZJWiljhDrs6lQSG/LIP4VwfxCn8Q+C/Gr6rp99ex2VyqyWjCQvCTgBkYEkHoT+Irr9Gh1S41wyWK5eKTJZ8hFXoQfYj8Sea7aPRIGhWO+P2tVbcsUg/dJzkYX27ZzQByGm2Nr8TLDS9Z1fR5bKSHPnbvlW4HYDuVzzn6jvWb4++Fer+IZluNN1SAxQRhYrORNgHHOGHGfwAAwO1egX1xO+Hs7XzktH3N823eQCCq8HJGf6VQu/EgEamRktYHQt5qN5jn2AwACR3PpRcai3sY3hDQbvwh4VgtbiaYXUVtJcyor7lRg2doGcEEHn6Eiu4gkM0EcrIYy6hijdVyOhrJjtnSyWzPmm5vAVd5n3ssY6kn6Hp6tWndXUGn2b3E7bIolyTigRPRWXo3iHT9dEos5G3wkb0cYYA9D9K1KACkIDAggEHgg0tFAHP+G86bdXvh5ydtkwltM97d8lR/wFgy/QCugrB1z/AEHXtG1QcKZWspiO6yD5c/R1X8zW9QAUUUUAFFFFABRRRQAUUUUAFFFFACEBgQQCD1Brm7MnwtqSabIT/ZF4+LJz0tpDz5JP909V/FfSulqvfWNtqVlLZ3kQlgmXa6n/ADwfegCxRXP6bqFxpN6mh6zKZC5xY3r9Llf7jHtIB/30OR3A6CgAooooAKKKKACiiigAoqC9s4dQs5bS4DGKVdrhXKnH1GCK4jwv4O0W/wBEN1di7MgubhN/26ZcKsrqOjdgBQB31Fc14PuZHfU7KO/k1GwsrgR2t3I29mBUFkL/AMe08Z/DtVvUtX1e3vGttN8OzXu0AmeS4SGI57AnJJ/CgDaqra6nYXs0sNpewTyQnEiRSBih9wOlU9E1xtUlubS6sZbC/tNvnW8jBxhs7WVhwwOD+RrnrvUbbQfH92lrpzXF3eWEXlWtqgVpW3uWYngADuxo6h0O3qqNTsDfnTxewG7AybcSDzAMZ+716VjQeKLy3vYLXXtEk0sXTiOCdZ1niZz0VmGNpPbIwfWqXiu7sdF8U6FqctvmRvPT9zFulmYoAqDHJJPSgDsKK5d/Fmp2Ci61nw1cWOnk/PcpcJMYR6yIvIHqRnFdBc3Dx2L3FtAbtgm6OONgDJ6AEnFADYNTs7nULnT4Z1e6tAhnjAOUDDK/mBVquc8PahHe67qYm0GTS9R8uF52kdHMqncE5UnptNbd/cT2tlJPbWj3kqD5YI2VWfnsWIFAFiiuC8NeI9eFneY8L313/p0/zfaovk+c/Jy3bp6V21nNLcWcU09s9rK65aF2DFD6Ejg/hR0AnooooAKKwdQ8RzpqMmm6NpUmqXUABnxKsUUORkBnP8RHOADUdl4puH1q20fU9EudPvLlXdCXWSJgoycOOvXpgGgDoqKKKACisjVfEUWk3QgfTNUuiV3b7SyeVB7ZHf2qj/wm1v8A9AHxB/4K5P8ACgDpaKhtLgXdpFcCKWISKGCTIUdfYqehqagAoqtqNzNZ2E1zBaPdyRrkQxsqs/0JIFc1Y+NdR1uxjv8AQ/DFzd2rKC0k1wkOT3VAfvY6Z4Ge9AHXUVR0jVbfWdMiv7cOiPkMkgw0bAkMrDsQQRWP/wAJTqN+7voHh+XUbRGK/apLlYEkIODsyCWHvgCgDpqKytH16PVkuIzaz2l7akCeznwHQkZByDgg9iDiq3h/xJPrTXfn6RPp8dpI0TvPLGw3qeR8pOMdc9KAN6isHVvEdzpms2Wnx6LcXa3rbY545YwucEtwTngDNb1ABRRXH+NdFsr3UNGnm88PPfR28nl3EiBoyrnGFIHUdetAHYUVwviDRdO8Kaf/AGlo99dWeoIw+zwG7klW6bOPLMbE7s9OOR1rsrq5ktrF7hbWW4dFz5EOC7H0GSB+tAFiq17qFlpsQlvruG1jJ2h5pAgJ9MmsCfxTrNhEb3UvC01tp6cyzJdxySRL3Zox2HfBNaHiiG3vPCmomSKOZBaSOm9QwB2HBGaTdlca1djWR1kRXRgysMgg5BFMubmCzt3uLmaOGFBlpJGCqv1JrktH8T6ldaPZnRPDs2oWsUCIbl7hYFkIUA+WG5bB4zwK3tK1Wy8R6fLm3ZSjmK5tLlBvicdVZeR6H0NU1roSmX7a6t7y3S4tZ454X+7JGwZW+hFS1wHhTxBdRaKum6HokmoyWs84mbzVghhJlchdxHLYIOAOOK6fRfEC6pPPZXNnNp+o24DS2sxBO09GVhwyn1H44pDL+oahaaVYTX19MIbaBd0khBIUfhU6OsiK6HKsAQfUVzni7U5LSxuYbnw1Pqmm+QXuHWWNV2jkghiCcYzXQWzpJawvGu1GRSq+gxwKAJaK43xprGq2d/pcNpo91NEL+IiaKdFExw37vBOfz44rY0zWdWvb1Ybvw1dWERBJnkuInAPphWJoWoM2qZLNFAoeaRI1JCgswAyTgD86fXJ6i/8AbXxBstJbm10qD7fMvZ5WO2MH6fM31xR1DodU7rGjO7BVUZLE4AFCOkiLJGwdGGVZTkEeooZVdCjqGVhggjgiuW8FTNZT6t4adiRpFwBbknnyJBvQfhyPwFAHV0UVy/iDx3YeHvEmnaHcWd1LNqBAWSJAVXLbR355646UeQHUUUUUAFFFFAHknxYiFl448M6rnarMYXP/AAIf0Y1qHrUXxytmPhex1BB81neKc+mR/iBSwyCaCOVTkSIGB9cjNAD6KKKAOWuLgaF4quL28ic210gCyqM7enH6VLqPiTRbyJIlge/kDhkiCEc/WujZVdSrqGU9QRkUyO3ghOYoI0PqqAV1e2g7OUXdedjFwlrZ6MejFkVipUkAlT1HtS0UVymwVzHhi2/tP4zXEuMraIB+OB/9euo71mfCS3+1+Jtf1UjObhkU+wJ/xoA9aooooAKKKKACiimu6xozuwVVGSxOABQBn65qx0qxDQx+feTuIrWDP+tkPQewHJJ7AGl0PSRpNh5byefdTMZbqcjmWQ9T9OwHYACs/REbWtRfxHOpEJUxaajD7sX8UmPVyP8AvkD1NdDQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABWD4o/fHSbHtdajFvHqqAyH/0AVvVha1z4m8Oqegnnb8RCw/qaAN2iiigDF1G5WK9lO0vJtWKJB1J5Y/TqM/QVhanFdFIg0x82aQKsUC59z7nge3WtAuW1O8uJQQPOMUS92wADge5A/KtiwsPJb7TOoM7DA7+WvoP61N22bcsYwu92Zugxn+ybizjcQX6SFphjJQljtBx6qB36Vt2sxntYpWADMoLAdj3H51A9nJDdyXdmIw8wUTI4wJMcA5HQ4479qydX8QT6aBbQWQinYFyZCGVQT1wDySc+lUYm7DGlnbbWkG1cks3HU5/rXI3fgvRbvXDqtvazTsz+YEV1Fuz+pPXGeoFZUvja+huY2v7e3vIY2zs2lSPcckZ+orqdL1OO6RbnTxG0cz+Y2MLvUlgAB/eAXJ+hpOKe5pTqzptuDtfQJ5rnTpZrsvJcywJGjxBB869SwPbknnOOOemag8b3Ui6TFbRqT9ofcw/2Vwcfnirvmz3l+sqGNYvsm5g4yV3jge4yOR/jXDar4vs9Uaw0ryJ4phGYxIxG1sqPQ56imZmD/as2iaxFqdu5E0TDcpfO5O6n69K9qsruC/soby2cPDOgdGHcGvL9e1rSX8Kz2S2oiunUKIkiwAwI+bPTHH1rS+EGuG70u70aVsvYuHjz/zzfJx+DZ/MUkXJJbO56LRRRTIMPxmhPhO/lUfPbILhP96Ng4/9BraRg6K6nIYZFUPEKh/Depqehs5Qf++DUmisX0OwdjktbRk/98igC7RRRQAUUUUAFFFFABRRRQAUUUUAFFFFAFe+sLTU7R7S9gSeB/vI4yPY+x96wpTeeEmEzTz3uif8tfNJkms/9rd1eP1zkjrkjp0tIQGUqwBBGCD3oARHSSNZI2DowBVlOQQe4p1c9omdF1abw85P2YobjTie0ecPHn/YJGP9lh6V0NABRRRQAUUUUAMlljhjaSWRY0UZZmOAPqa878PeEfCniXR7k3MUUt5Nc3JeSG4PmAec+GwD6Y7Yr0K4t4LuB7e5hjmhkGHjkUMrD0IPBqtZaJpOmytLYaXZ2kjDaXgt0QkemQKAMnwzf/YJJPDWoGCK8sgPIKKI1uYTna6qOM8EMB0I96zLRG8Sy313qXiO6sVt7mSFbG0uBAIFRiAXP3iSBu64wa6+Wxs57qK6mtYZLiDPlSvGC8eeu0nkfhVK+8MaFqd2Lu+0izuJ+P3kkIJP19fxoA5nwdd6aPGOsQ2mtTaghgt0jlupg7OQZMhGwNwHqM9+alk13S7L4oSG4niCy6dHCLjcCkb+Yx2M38JPv6V1X9kaZ9qiuv7OtPtEChYpfIXfGB2U4yBz2pg0LRwtwo0qyAuv9eBboPN5z83Hzc+tHYO5i+NL61vNKGiW0qT6hqEiLbxRsGZcOGMhx0CgZz7VV8Xaxp+m+K/Dk13IjJbyzmbB3GANHgOw6gDPX3rotM0DR9GLtpum21oz8M0UYBI9M9cVMdK043rXx0+1N067WnMK+YwxjBbGcY4oAz9e17SrTQ5pZbiG4E8ZSGGNg7XDMMBVA65zUuip/YvhjToNSnjieC2jjkaRwAGCgYyadZeGNB028N5ZaRZ29wf+WkcKgj6en4VdvLGz1GA299aw3UJIJjmjDrkd8HigDmrHVtMXxzq0p1G0CNZWwDGdcEhpc966mOWOaNZInWRGGVZTkEexrL/4RPw1/wBC9pf/AIBR/wCFacFvDawJBbQxwwxjCRxqFVR6ADpQHU5zwheWsNvqtvLcRRyw6ncmRHcAqC5IJB7EEGtyw1Ww1TzjYXcVyIH8uRom3BWxnGRxVbUPDOhatci51DSbS5mAx5kkQLEehPer9vbW9nAsFrBHBEnCxxIFUfQCjoHUlooooA5bw3e22napq+k3sqQXzX0lyokIUzxvgqy564HynHTFasmt6OdXtrAXEU98+7y0iHmNGMck4+6OMZOM1Nqei6ZrMax6lYW92qHK+dGG2/Q9qXTtH03SIjHpthb2it94Qxhd31x1oQF2iiigDH1XSdVvroS2XiG406MLgxR28Tgn1ywJql/wjviH/odLz/wDg/8Aia6WigCG0ilgtIop7hrmVFAaZlClz6kDgfhU1FFAFe+mit7GaSaVIkCHLOwUD8TWN4Hubd/BGlMk8TLFaIHKuCEIXnPpW3dWdrf27W95bRXMLY3RzIHU49QeKitdK06ytpLa00+1t4Jc+ZFFCqq+Rg5AGDxR3A53wsY9R8M6rbWtzG0kl3eKGRwdu6R8Hj86yPDGmpdaTDanxdq9ld2aCG4sjNEpgZRgjBTO3jg9xiu5sdK07TA40/T7WzEmN/2eFY92OmcDmoNS8OaLrEiy6jpdrdSKMB5IgWA9M9cUAY/h6z0uDxHcvB4jutXv1thHKssiSCNN2RkqoAOc8E55NYutxtL4mv8Awmu4R67PBctt4xCFIm57Z8sD/gdd3ZafZabbi3sLSG1iH8EMYQfkKkNrbtdLdGCM3CqUWUoN4U9QD1x7UAcN4TmmvfEdvptyWaXw3bS28rHuzOFjb8Y0z+JrvqijtreKeWeOCNJZsebIqAM+OBk98e9S0AFcj48/sy6Gj2GoywGKTUozLFJIFym1+TznHvXXVRvdD0jUphNf6VZXcgXaHnt0dgPTJHSgDlbvwvp3huWPxR4bs45Ps65nt1PmCaH+Ixk5KuByMHnGK0fEHiAPo1jNpOpQww6jcpAb8YdYFYE5543HAAz0JFdHBbw20CQW8McMMY2pHGoVVHoAOlV10jTEsZLFNPtVtZSS8CwqEYnrlcYNAHB+L9P0vSPDd60vi3VpbmW3dUia9EhmO08bAOnrgDArptUvrM+ArqQXcGxrB0VvNGC3lngHPX2q9ZeGNB01ZBZ6RZwiVSsm2FfmU9QfUe1SHQdGayWyOkWJtVfesBtk2BvXbjGfek1dNdxrdMzPB+u6Xd+F7IRTxW7W1ukc0EjBGhYKMgg9PXPcVFoF5b3mua5rsMiLpsvkwpcMdqStGGDOCeo+YLnvtrTvvDGg6lMk17o9nPJGAqs8KkgDoPp7VeksbSazNlLawyWxXaYGjBTHpt6Yqm7u5KVlY5H4d63pj6RNYCaOG5iurhyjkKZVaViJF/vA9Mj0q7HdQax48hm091mi020liup4zld7spWPPcjaSR2yPWtS68M6Fe2sVrcaRZSQQZ8qPyFAjzyduBx+FXbOytdPtltrK2itoE+7HEgVR+ApDMXxjqVgnhfWLd723Wb7HKPLMqhs7TxjOav6TqVhcWdrDBe28svkr8iSqzdB2BoufDmhXlw9xdaLp88znLSS2qMzH3JGTTrPQNF0+4FxZaRY20wBAkhtkRgD15AzQgZl+MpY7eLR7mZxHDDqsDSSMcKg+YZJ7DJH51q3euaTYKjXWo20XmMFQGQZck4AA6mrc9vDdQPBcRJNFIMPHIoZWHoQetZ1h4X0HS5/PsdHs7ebtIkIDD6HqKEDNWuQsgbP4r6osvH2/TYZISe/lsVYD8wa6+snWNFbUL3TtQtphBd6fNuVyuQ8bcSIfYj9QKOqDoa1cj4cH2rx/wCKb+P/AFKm3tQ3ZnRCW/LcBXVyiQwuISqyFTsLDIB7ZrO8O6Kug6RHZ+aZpizS3ExGDLKxyzfiT+WKFuHQ1K5ceLkufHreGLbS2uHtoxJPd7wFgyM4xjryB1711FY+ieHLXRLrUbuN3mudSuDPNK4Gf9lR7AUdQ6GxRRRQAUUUUAcn8ULH7f8ADzVYwu5o4xKP+AkH+Wa4/wAL3H2rwxp0uckwKpPuOP6V6hq1oL/SLyzIz58Dx/mpFeOfD2Ut4Y+zt961uJIj+ef6mgDp6KKKACiiigAooooAiuphbWc07dIo2c/gM1Y+Ctm0PhA3Tj57mVnJPfk1h+MLn7L4U1CTOC0Xlj/gRA/rXf8AgKx/s7wbp0GMERAn8qAOiooooAKKKKACue1pm1zU18Owki2VRLqTr/zzP3Yvq+Of9kH1FaurajFpGlXF/MCywIW2jq56BR7k4A+tVvDumy6dpu67Ie/u3M9247yN1A9lGFHsBQBqKqooVVCqowABgAUtFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUVDdTPb2ks0cD3DxoWWJMbnIHQZ4yaAJqwtf8A3Ws+Hrg9FvmjP/A4ZAP1xXnd78foomaO28Oy71OD584Ug+4Cn+daGl+LNb8ZeFr3XbnToLS00yeKe38vczyNG4Zzk9guR9T7UAeo0U1HWRFdGDKwyCOhFOoAgSytY7l7lIEEz9XxzU9FZ19qDQ3a2yER/uzI8rIXCjOAMDuT/wDWzQBoEgAknAHUmvP9Yuxc3b3Jzi4fEfsoHy/mAT+NdFeXd3PG1nuIEi/vS0exlT25PJ5H51zOuFVWNwRtWRf14/rQBymsgtHIF611/wAL7Y3Wizz7iBHeZibGcjb8w+nzH8TXJ6n1asiz8Wa14af/AIlt4Ui3bmgcbo2Pfjt+GKAPVLyS4s9P8nYyy3Ucke7+6gKgn/vkYH1ryjWXMXiKyZeMXKY/OvQ9H8XReM9InvhD5FxbosM0WchWOTlfY8flXET2DX/imAAfJA3nOfYdP1xQAuunashPQU/4Taitt4/EBbC3ts8Y9yMMP5Gm6zE1wxhRGkdzwiAkn8BWh8PPAmsjxbbazf2ctlaWe5l84bWkYqQAB1xznJoA9pooooAyPFc/2fwlq0vcWcoH1Kkf1rQsoPsthb246RRKn5DFZHi0+fZWemDltQvYoiB/cVvMf8NqH863qACiiigAooooAKKKKACiiigAooooAKKKKACiiigDC1UCTxboEY6oLmXPsEC/zcflW7WDGftnjqZ1+ZNOsREx9JJW3EfXain8RW9QAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAV4l4fi/szxj4o0c8LHdedGPYk/4rXtteP8AiiH+yvjMkuMR6rZf+PAY/wDZB+dAGxRRRQAUUUUAFFFFAHM+OSZrCw08cm8vY0I9hya9msIfI0+CIDG2MD9K8e1GM6h4/wDDtgOQjPMw/Qfyr2jpQAtFFFABRRSUAYOrf8TTxLp2lDmG1H265HY4OIlP1bLf8ArfrA8Lf6b9v1xuf7RnPkn/AKYJ8kf54Zv+BVv0AFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRXKeMfiHovg6EpcSfab4jKWkRG76sf4R9fwBoA6W7u7awtZLq7njggiG55JGCqo9ya8g8V/F6+1a7/sTwTbyySSnZ9qEZLv/ANc17fU/p1rHhsvGnxhvxcXTmy0dH+U4IhT/AHR1dvf9RXrnhTwTovg+08rTrfdOwxLcyYMkn49h7CgDxS9+EHimL+zZp9ss+oz7JwpLm3J53Oe/GST7e9e96XodlpOgw6LbxD7LFD5W0/xAjkn3OST9a0aKAMPwnNImlNpdwxNzpUhtZCerKoBjb8UKn863K57WD/YetQ68PltJwttqHooz+7lP+6SQT6N7V0FAC1jb45YDKsm5bq62SvGckKOFXI6dAPxNbNZUsPlS3FuihGkYT2+MAM4A+X81H50AUbweTaStbhYvMufLUKOFAOzH6H865+9hCWqwsoICBSDyDxzW/fOos2jmBRDcOHfODEd25SfzFYN6ZCpEjo5B+8nGR9O1AGJY+HJdZvJUjuzb28ChpXcb8ZyFAHXr7+tcZ4t0ybQ9UubC4YO8JHzqMBwRkEfga7nTtTbT9XjSWdks7hxHcKMYwcgN+BINdJ4h+H9j4pEQu5p7We2Xy/PiAPmx5yBz3H+NAHnPw3sLxfD+u6lEGaGR0gKr97gElh64DfWuw0zw7OblogALq6IZyeRDGPX3/rWzo3hmDT9Pi0rSfltLeQu7zZJdz1JxjLHjjsOOp46aysI7JXIJeWQ5kkbqx/oPagCLS9FsdIh2WsIDn78rDLufc1foooAKKKztc1UaRpj3Cp5s7ER28I6yytwqj8fyGT2oAoxn+1PGcko5t9HhMQPrPIAW/wC+UC/99mt+s7QtLOk6VHbySebcOTLcy/8APSVjlm/Pp7AVo0AFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFUNb1NdH0ie9KeY6DEUQ6ySE4RR7liBVyaaK3heaaRY4o1LO7nAUDqSa5+xWXxLqUOrzI0emWp3WETjBnfp5zDsME7R7k+lAGhoOlvpen7Z5BNeTuZrqb+/I3XHsOAB6AVp0UUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFeYfGO3NpP4e19Bj7JeeVIw/utg/8Asp/OvT65X4l6UdY8A6nAi5kij8+PHXKHd/IGgDC+lJVTSbj7Xo1lcf8APWBG/QVboAKKKKACiiloAyfDEP2/4uyydVsrRV+hPNeu15h8LovtPibxDqJGcz+Up9l4r0+gAooooAKw/E15N9lTR7En+0NSDRRkf8sk/jlPoFB/EkDvW5WDYgS+N9XlYZMNpbRIT/DkyMQPr8v5CgDYtLWKys4bSBdsUCLGi+gAwKmoooAKKKKACiiigAooooAKKKKACiiigAooooAKhu7u2sLWS6u544IIhueSRgqqPcmua8Y/EPRfB0JS4k+03xGUtIiN31Y/wj6/gDXlsNl40+MN+Li6c2Wjo/ynBEKf7o6u3v8AqKANjxX8Xr7Vrv8AsTwTbyySSnYLoRku/wD1zXt9T+nWrXg74NgTDVvF8hu7pzv+yb9wz6yN/Efbp9a7rwp4J0XwfaeVp1vunYYluZMGST8ew9hXQ0AMiijgiWKGNY40GFRBgKPQCn0UUAFFFFAEc8EVzBJBPGskUilXRhkMDwQawdIuZdEvU8PahIXjIP8AZ1y5/wBag/5Zsf76j8xz2NdFVTU9MtdXsXtLtCyMQVZThkYdGU9mB6GgC3TJYY502SorqezDNYNpq91o1xHpviGQEOdltqWNsc/or9kk/Ru3pXQ0AYGpxW+mljbKWaUZe2X5mf8A2vr254OK5e+ntVYqiiFj/CybDW+1zMLi53pvdpnARBklQxAZmPQcYA9jWTqhA3E9BQByGqclq7rwFdX2t6AVv5ZxFbSeShA2+coA6t1OOnGOlZWkeD59bmW5u90FjnPo8o9vQe/5eteh21tDaW8dvbxLFFGu1EUYAFADo40hjWONAiKMBVGAKfRRQAUUVWv9QtNLtHu764SCBOruf0HqfYUASzzw2tvJcXEqxRRKWd3OAoHUk1haTFNrmpJ4gvI2jt41K6bbuMEKesrDszDoOy+5NMis7vxPcR3eqQNbaXEwe3sJBh5iOjzDsB1CfieeB0lABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABUV1cwWVrJdXMqQwxKWeRzgKB3NS1zjqPE2utGw3aTpcuGX+G5uR2Pqqfq3+7QA2C1uPFUyXupRPBpKEPbWLjDTkdJJR6dwn4nngdJS0UAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABTJYkmieKQbkdSrA9wafRQB4/davofhS6i8Nz3ciS2abDJJEyoRkkYPfggZrUt7mC7iEtvMkyHoyMCK7zVtB0nXYPJ1TT4LtO3mJkj6HqPwrhL74LaekxuPD+sXulSHnYG3p/Q/qaAH0VmSeCviPp/wAttqmnaig6eaNpP6f1qu2kfE5jsGnadH/ths/1oA3KoX+t6ZpYze30MJH8JbLfkOapL8O/HernGpa4lrGeqQDH8sV0egfB3w9pUq3N/wCZqdyOcznK5+nf8aALPwusYrbRJ7iKXzhdTGXzNpG7cSeh5rt6ZFFHBGI4o1jQcBVGAKfQAUUUUAFYWj/N4o8Qt6SwJ+UQP/s1btYWhc6/4jP/AE+RD/yBHQBu0UUUAFFFFABRRRQAUUUUAFFFFABRRXKeMfiHovg6EpcSfab4jKWkRG76sf4R9fwzQB0t3d21hayXV3PHBBENzySMFVR7k15B4r+L19q13/Yngm3lkklOwXQjJd/+ua9vqf061jw2XjT4w34uLpzZaOj/ACnBEKf7o/jb3/UV654U8E6L4PtPK0633TsMS3MmDJJ+PYewoA4Xwd8GwJhq3jCQ3d053/ZN+4Z9ZG/iPt0+tesRRRwRLFDGscaDCogwFHoBT6KACiiigAooooAKKKKACiiigCK4toLu3e3uYUmhkG145FDKw9CDWENM1fQR/wASWUX1kv8AzD7pyGQekcp7f7LZHuK6KigDlv7W027vGjaY6PfS48y2vothkI7g5wx91JrQt/Dlt5onvH+1MDlVK4jH4d/xrTurO2voTDd28VxEeqSoGU/gax/+ERsYDnTrq/0z/Ztblgg/4A2VH5UAbtLWF/ZPiGI/ufExkA6C4sY2/VdtH2DxS3Da7YqPVdOOf1koA3ahuru2soTPd3EUES9XlcKo/E1j/wBg6rPxeeJ75l/u20UUP6hSf1qW28J6Nbzi4e1N3cDpNeSNO4+hcnH4UAQHxJNqX7vw9YPe54+1zAxWy++48v8A8BB+oqay8Pf6Ymo6xdHUr5OY2ZdsUH/XNOQP945b3rZAwMDpS0AFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFAGR4i1C4tLSO0sMf2hfv5FtkZCHGWc+yqC34Ad6uaZp0Gk6bBYWwPlwrtBY5LHqWJ7knJPuazJ/3/AI8s4z0tdOlkH1d0X+Sn863qACiiigAooooAKKKKACiiigAooooAKqXup2enyW8d1OI2uZPLiBBO5qt1x1j/AMVJ43mvj81lpI8qH0aQ9T/P8hXRQpKfNKW0Vf8AyXzZlVm4pKO7Z2NVLrU7Ozura1uJwk10xWJMEliKtdK4/RP+Ki8XXett81rY/wCj2mehPdh+v5iijSU1Kctor8ei+8Ks3Gyju3/w52NFFFc5qFFc5rvjfS9CvVsGjuLy9Iybe0j3so9+eK4rS9TsNS+KWn3OnSX8Zn81rm3uyQY32NwB6YrN1FdJHXTwk5Qc3okrnrFFFFaHIFFc/qfjCy03UHsBaXt1cR43LBDnGRnqauaL4gstchle2EiSQnEsMq7XQ+4reWGqxh7Rx0MlWpuXInqalFcqfiFpJkeGK1vpZ1OBEsPzH8M1raJ4gsteika2EkckJ2ywyrtdD7iqqYWvTjzTi0hRr05PljLU1KK5vUPG2mW11LZwwXd60eRK1rHuCfjmsXwLLbSeJtSFjPcS2nkqY/PYlhyM5/HNaxwVT2Uqk01ZX23/AMiJYmCmoR1u7HfUUUVwnSFFchefEjSYL2W1s7S/1IwnEklnDvRT9cjNavh3xXpvidbg6f5wNsVEiyptIJz/AIGpU4vZm8sPVhHmlHQ2qKKZNKkEDzSZ2RqWbAzwKpK5gPorlP8AhYOnY8wWGom3HWfyPkHv1rel1W1j0g6opea38sSAxLuLA+gronhq1O3NG1zKNanO/Ky7RXKj4h6K0TFEummDbVgEXzsfYZrRs/FOmXekS6mZGt4YWKSiZcMjemPX6U54SvBXlBijXpSdlJGzRXKr8QdLLK0lpfxWzHAuXh+Q/rXTwzR3EKTQuHjcBlZTkEGoq4erStzxsVCrCp8LuPooqlqurWWjWZu76Xy4wcAAZLH0A71nGMptRirtltpK7LtFebeLPEmnaxpnMOp2VxGCbYuuxJMkZzg88V1v9rwaR4Ysbm6SeVXhjX90hdsla7KmBqQhFvdu1v63OeOJhKbS2Svc3KK5vwXNpkthcrpb3jIk3z/azlgxHb2q74i12LQrHzXjld5Awj8uPcAwHGfQVjLDyVb2UVd/caRqxdPnexr0V5Np81hqUEcl9fa5/aMz8ywjKKSeMe1dx4g1tfDejJDm4muGhKxTbN3zAY3Ma6a2AlTnGnF3k/K39IxpYpTi5NWS8zoaK8p0z+z9RW286/11dSnYBpkyUDE9vau81bxJp/h9Yba4eW4uWUBYol3SN7mlXwMqc1CN235W/pBSxMZxcnovU2qKwtJ8Xadqt59i8ue0uiMrDcptLfSl1rxZp+g3K293FcksobckeV59/wAK5/qtbn9nyu5t7any819DcormF8faO94sKLctCziP7SIv3e49s9f0q3q/i3TtJuxZlZrq6IyYbZNzD60/qldSUeR3Yvb0mm+bY3KKxtF8Uafrcz28PmwXMYy0E6bXA9ao3Hj7Sbe7ltDBePPGxURrDy5z25oWEruTgou6B16Sjzc2h09FZGieJbLXHlihSaC4h5eCdNrgetc7r/i82nimyhiN2kFs7rcxiPHm+mB/FVU8HWnUdO1mlf8Ar1FPEU4w576Hc0Vj6N4ms9bnkhtoLqNo13EzRFRj61sVz1Kc6cuWaszWE4zV4u4UUUVBQUUUUAeYXmvePovFo0CO40/7RMrSxYjG3ZyRyeegq3L4p8X+Fbu1bxPbWk9hcSCMzW/DIf8APt2ql4qg1W4+LFpFo1zFbXps/kllGVAw2ex7Z7VnXcGpJ40sbTx9eyy2m7dbvGQIHbtngYHrxn8K9eMISUbpaq7XX5HFJyTlZvf5HrN5qFnp1sbm9uoreEfxyuFH61lW3jjwxd3K20Os25kY4AJKgn6kYrJ+IuqabDa2mlXGlHVby6k3W1sGK8jjJI574x3rhfE2ma1beH5JL3wlpenW6lcT2+BJHzwPvHOelc1DDwnFOTtfbb+mbVKkouyPQfiJaXz+H5NRsdWubE2KNIyQsQJenBIPb+tV/DfjXRrLwtpg1fWo/tbw5fzHLvnJ+9jJ/On6tI8vwikeRizNpqEk9TwKz/h74P0C58KW99c2cN7cXIYyNKN2zkjaB2ximlBUWqnR9CW25px6o665aHxHoUq6VqvliddqXVswYoa4fwL4kj0p9bj8Qa6zrb3CxRPdSlicbgdoOT2HSn6Bbx+HPirc6Lpbt9guLfzJId2RE2Mj/PoazvBHh3Stb8Xa9NqUaXDWty3lwP0OXbLEd8Y/WrjThGEk37rSfnuKUpNrunb8D0jSvEWj65u/szUIbkryyqcMB9DzSa3qmnafZtDfanDYNcIyRyO4Ug46j6Zrg/HmkWPhW/0nWtDjWyvDchDFFwJB/u/ofrXfaroGk64I/wC07CK6MWdm8crnrXNKnTjyzTfK/v0NYyk24vdGb4KWGPS5Y4vEJ1wrLlpy+4pkD5ep+v41tX2oWemWxub66itoQQN8rBRn0rhvhGipp+roowq3pAHoMV2+paXY6vaG11C1juYchtjjjI70V4qNZp7BTd4HF+DfiBb3dtfHX9WtYpFuWEG8hMx9seortrDUbLVLf7RYXUVzFnbviYMM+leZ/DfwzomsWepvqGnRXDQ3ZRC+flXHTrXpGmaZp2kW5s9Nt4raMHeY4/U9zV4qNKM2o3v+BNJza1LtYWgc6z4iP/T+n/oiKt2sLw9zqfiA+uo4/wDIMdcZubtFFFABRRRQAUUUUAFFFFABUN3d21hayXV3PHBBENzySMFVR7k1zXjH4h6L4OhKXEn2m+IylpERu+rH+EfX8M15bDZeNfjDfi4unNlo6P8AKcEQp/uj+Nvf9RQBseK/i9fatd/2J4Jt5ZJJTsF0IyXf/rmvb6n9OtWvB3wbHnDVvGEhu7pzv+yb9wz6yN/EfYcfWu68KeCdF8H2nladb7p2GJbmTBkk/HsPYV0NADIoo4IlihjWONBhUQYCj0Ap9FFABRRRQAUVX1Cee10+ee2tmupo4yyQqcGQjoM15/bfEnxBe3U9rbeE5JZ7Y4mjSQkxn34ranRnUTcenmRKajuekUVyPh/x2NT1f+xtU0ufStQK7kjl6P34yB2rrGZUUs7BVHUk4AqJ05U3aSHGSlsOoqOK4gnz5M0cmOuxgcflXDfEDXfFHh2eO8sbi1TTpGWNVMYZ95yTnPbiqp0nUnyLcJSUY8x3tFQi6hBSN5o1kYD5CwBP4Vj+L5tdttGa50KW3jkgzJMZlzlACTj3qIxvJId9Lm9RXNeCdfn1fwpb6jqtxEJpHdSxwgOGIFdIrK6hlYMD0IOQac4OEnF9BRkpK6ForM1/+1TpUi6JLBFfErsab7uM8/pU+lC+Gl241J43vNg85o/ulu+KXL7vNcd9bFyiqGuakdI0O81FYxI1tC0gQnAYgdKg8Na0dd8PWepyokMlwhLIrZAIJH9KfJLl5umwcyvY1qKKhurqCytZbq6lSGCFS8kjnAUDqTUDJqZLLHBE80zrHGilmdjgKB1JNcI3xd0lg89ro2s3VhGcNexWv7oe+SelbOp61p+v/D/UtR0y4We3lspsMOCDsOQR2I9KTdk2NatI37W7tr62S5tJ47iCTlJImDK3bgipScDJryXwP8Q7DRvBOm6dDpmpapPbxM1yLK33iHLsRuORzjmvQ/D3ifSvFWlNfaZMXjUlZI2G1429GHanLS9iV0NCy1Cz1KAz2N3DdRBipeFw65HUZFWK4z4cXnh8eEZ7nR4J7GwjuJDILuQEggDc2cniqr/FvSmaSSx0bWb+yiJD3lva5iHqck9KBne0Vn6Lrum+INLj1LTblZrZ/wCLoVI6gjsRXLXXxX0kXc0OmaZqmrpbnEs9lb741/EkZo8gO5pAwYZUgjOOK4rVvHVlqXgG81bQ4ry83I8LLbpiW2Yqfmcfwgdc1U+EGszXnhS10+TTb6JbeNmF5Mn7qcmRvut3PP6UdwPQaKKKACiiigAooooAwT8nxAUnpLpRA99soz/6EK3qwdcP2TxBoeoHhDNJaSH2lXK/+PIo/Gt6gAooooAKKKKACiiigAooooAKKKKAMTxbq50fQpZIj/pE37qADqWP+HWpfDOkDRNCgtCP3pG+Y+rnr/h+FS6holpqd9ZXdyXLWTl40B+Uk9yPwrRrplViqCpx6u7/AEX9dzFQbq876bfqc/4z1V9O0QwW2Td3reRCo65PU/l/MVf0HSk0XRrexTGY1+cj+JjyT+dF3olpe6taalPvaW0B8tM/Jk9yPWtGidWPsY04+r9en3L8wUG6rnL0X6hRRRXMbHm+m6rZeEPGuuf8JArwNfyiS3u2jLKyc/LkfUflWZqPi3QpfiXputQ70s4YmSS58ojzThgCBjJxkDNerT21vdJsuII5l/uyIGH60C2gVFRYIwqDCgIMD6VlyNWV9jvWKp3cpRd2rPXTa3YkVg6hlOQRkUtFFanAebXmrveaxfrrOvXWjiCQpDbW6MCy9jkdad4J1WztPEeowz3Nw7XW3ynuEO98AklvQ4r0KS1t5ZBJLBE7r0ZkBI/Gn+WgbdsXd645r1ZY+m6Tp8mjVt1p+F/vZw/VZ86nzbO/X/M4PwrrGm3PjbVZEfc16w+zsUOSACW+nSjw/qtpd+M9bS3nIa9XEB2kZKjk+1d2sUancsag+oFAijVtyooPqBUTxlOTk1F6pLft8vJfiVHDzVve2d9v+CcL4U17TPDenS6ZqxayvYpWMm+MnzOeDkDmoPDWt6d/wnWoSKjW6X+1YEKEFjwc47Z6/jXfS2tvOwaa3ikK9C6A4/On+XHu3bF3DvjmnLGUpc75Hea11076aCWHmlGKkrRemn/BH1W1GGW4026ggbbLJC6oc9GIIFWaK8tq6sdydnc828E+K9D8NaEujauW02/tnfzlkib5ySecgHtgfhW34O1HQtQ1fV59DtLlVmdZJrp1Ijlbnhc9O5/GumuLCzumDXNpBMR0MkYbH51LHFHCgSJFRB0VRgCpUWmr9Dqq16c+ZpNOW+un5D6zPEd7d6foN3dWMXmTxplRjOOeTjvgc1p0VtCSjJSavboccldNI8nury2n0dpG8Uajd3ksRL20SMIwccgjpj3rqvC/iPTLXwbFLLOQtkqxzfITtYnj611EdpbRMzR28SM33iqAE/WniKMKVEahT1GODXo18bTqw5HF2vfdfdojjpYacJc3N0t1/wAzzfw54j0DT9X1W+vGxJPcFoJPKJOwk/lW345tZNV8Lw3WmoZIhIs7qicspH3sd+tdZ5EP/PJP++RTwABgdKmeNj7aNaEXdd3dafJDjh5ezdOT0d+nf5nlsuppc6cYZ/GhMTpta3Ngc49MdK7fwbGkXhi1SK4eeMbtjvGUONx7GtT7BZ+Z5n2SDf8A3vLGfzqcDAwKWJxkatPkira36fokFHDuE+Zu/wB/6ti1yPjaNob7SNUmgaexs5iZ0UZ25xhsfhXXUhAIIIyD2NctCt7Gop2v/wAHQ6KtP2kHE4Lxj4p0TVvDstrZubqZtrLiMjysEckkcen41q6f4x0Sz8P2Ek1ywGwRcRsfmVRnt710cdpbQ7vKt4k3fe2oBn60/wAmIqF8tMDttFdMsRQdNUuR2Tvv/wAAxVKrz8/Mr2tt/wAE888LeLNH0ybVDdXDILm7aSPEZOVPfiuq8T65p+m6S6XUpVruF1hwhO47f06itjyIf+eSf98inMiOMOqtj1GamriKNSsqnK/PX7ug6dKpCDjzL7v+CcR4O8WaPaaJYaXNcMtzkpt8skZLHHP4itbxnrVjp+j3FlcylZ7uBxEoUnPGOtb4hiByIkBHcKKc0aP99FbHqM0TxFGVf2vK97tX6/cEKVSNLk5l2Wn/AATj/CXizR10vTdKa4YXWwR7fLON3pmsnxJDd6Z42lv5NQk0+G5QCK7EPmAcAFfbpXoohiU5WNAR3CiiSKOZCkqK6nqrDIrSGMhCs6kY6Sve7T37afmmQ8PKVJQlLa1vl8zzHzYL/WtPaXxU9/PFMpj8uxbI5HGeOK1/iNrVg2nvpHmn7Wskbsm04x1612kNpbW/+ot4ov8AcQD+VPaKNzlo1Y+pGat46Dqwnyu0dtl+UUSsNJQlG+svX9WYGg6/4ev/AC9L0zbmNNyxeSQBjv061yF2l3o3izUWuNXfSvtLl47j7P5iyqTnGe2K9OWKNDlUVT6gYpJYIbhNk0SSL6OoI/Ws6WMhSnJxi7SWt2m/xVvwLnh5Tgk3qu2n6nnWkNb3ni+xuD4jfUblCRlLMqCuDwWq3putaZP8SrmcPuE0awQsUOd4wD9Oh5ruYreC3GIYY4x6IoH8qcIow24RqG9cc1c8dCTd4vWPLul1v0SIjhZJLXrfr+rOIstYsX+J9yVlOJYRbr8p5kGMj9DzVnxfMlh4l0LUbnctrC7iSQKSFziuu8qMNuCLu9cc0SRxyoUlRXU9VYZBrP63D2kZqOijy7+Vuxp7CThKLe7uYlr4y0i+1KGxsXmunlON8cR2p7knFb1RQ28Fuu2CGOIeiKF/lUtclV02/wB2ml5u/wCiN4KaXvu4UUUVkWFFFFAHAXPwsFxqL358SaiJ2JIk4LKD2DZz3ro9Z8LWmueHk0i9lkkMaqEuWwZFYD72fU963KK2lXqStd7bEKnFX03OKufhtBcaVa251i9+22bs0F6xy6g87evQY454qrL8Lm1CBxq/iO/vZuPLZj8sfP8AdJOa7+iqWKqrZi9lB9DhX+GW/SF01vEmpGFXJ2lsqRgDbt9OKhi+GFzp0YTR/FF/Zqw/eqOjH1wCMV6BRT+tVu/4IXsYdjkdN+H1npumXsMWoXZv71dsl/u/ejnPy+nv61lQ/CZLR2ubPxFfQ3hOROoAPvnByc/WvQ6KSxNVNu+4/ZQ7HGaT8O47fVYtU1nVbnV7mE5i877qHscEmrfiPwbLr+ordpr1/YgRhPKgfC8d+tdRRUuvUcua+o1Tilax55B8Jxahhb+JtRhDnLCP5cn1ODXeWdubSyhtjNJMYkCGSQ5Z8DGT71PRSqVp1PjdwjTjHY4W5+G80N/cXGh+IbvS4rly8kMeSM+2CK1vDPgy28OXM14b66vryddsk075yM56f45rpKKqWIqSjyti9nG97BWF4b5u9db11Nh+UcdbtYOlH7D4p1fTzwtzsvoffI2P+RQH/gVYGhvUUUUAFFFFABRRXKeMfiHovg6EpcSfab4jKWkRG76sf4R9fwzQB0t3d21hayXV3PHBBENzySMFVR7k15B4r+L19q13/Yngm3lkklOz7UIyXf8A65r2+p/TrWPDZeNfjDfi4unNlo6P8pwRCn+6P429/wBRXrnhTwTovg+08rTrfdOwxLcyYMkn49h7CgDhfB3wbHnDVvGEhu7pzv8Asm/cM+sjfxH2HH1r1iKKOCJYoY1jjQYVEGAo9AKfRQAUUUUAFFFFABRRRQAV5Fpuo69p3jjxK2haSmos0580M+Ng3HHcZ716rfpdyWE6WMqQ3TRkRSOuVVuxIrgdF8GeM9J1yXUhrGn5u5Va7wrMZBnJwCox1PpXZhnFKXM1qupjWTdrFHwjPdeL/HJ1TWriK3u9MUrFYqhRh1HfsCee9XfiVPoM2pWltfT6jcXSIcWNiwwwPILZ6H8zWv4q8G3Wo6rba3oF1FYapCcPI+Qsi474B57dORWdf+D/ABNa64niDSL+0k1GWBY7oTJhSwABK8cA49q3jUpynGd7WW3Z/wCXmZuMkmrX8ziY7iDSNf0qfSNM1PSJTcKkgupCVlUkDHQe+a7j4w5/4Ri1x1+1rj/vlqp6r4G8Z66ba8v9ctGuYJN6RYKxxdMEYXk5HpU3iLwZ4y8RWdta3ms6fJHEoZxsZMyc88Lzwfb6VpKpTlOEnJab7kxjJKStuSWvwm0ubTVe+vbuTUJEDNcCT7rH0B6j61B4Z1W/l8N+JdD1Gc3EulRyRrMTksu1hgn/AID+tTpo/wASLKBdOtdXsZbdV2JcOPnVfxGf51KngTVtM8NTWOkapD9vvpC19cXCkiVSCNo4JHX+dZSndNTmnfby/wAtCoxs01G1tznvAXgGy8Q6Euo6tcXEkRdkggjk2hADyfzrU0mK58EePrbQIbuW50vUkLRxynJiPP8AUfiDTdJ8IeOvC9n5OkapYyxyEs8D5KqfUZH+FbPh3wfqUevHxD4kv0vNQC7YUjHyRDp6D1PQd6urVTlJuacXey/L/hyYQaSSjr3IPH/g+wvbLUNfe4u1uobYlUSXEeVHHGP61qfDslvAmmEkk7G5P++1Zev+HvHGrS3tvDrdgunXO5VhZCCEPYkKf51Bofhfx3o0dpZxa5p62MDDMQQsduckcp7nvWOkqHI5rf8AT0NHpU5lE0PiN4ftNU0C41GeW4SWwgd4ljkwrH/aGOelc54T+HGka34YstRubu/SWdSWWKUBRhiOBt9q9H1XT49W0q60+ViiXMTRlh1GR1rhbDw/8Q9Gs00nT9R04WkWRHKy8qCc91z396KNWXsnBTs7/gFSC51Jq53un2UWm6fBZQs7RwIEUyNuYgeprifjTNNF8P5FjYqktzEkpH93JP8AMCum8M6Vqek6e8eraq+pXEkhcuw4T2HtVnXdFs/EOjXOlX6loLhcEjqp6gj3B5riqL3nrc3g9NrEml2lra6Pa2trGgtkhVUVRxtxXlnhhVtbT4j2FrxYwNIYlH3VJWQED8h+VbVt4U+ImmWI0jT/ABTYmwQbIp5oD58adgOCOB71s6V4Fg0LwZf6JZTmW6vopPOupuskjKRk4zgfnUS1u/IcdLIh+E9rbW3w60xrdFBmVpJWHVn3EHP5Y/CsbwsiWnxd8W2lmAtq0CSOi/dEhCn+bNSaL4G8c+F9JisdE8RWKxuuZoriNnWJz1MZ25wfQjrXS+EfB8fhWyvJZ7t77Ur5jJd3bjBdueB6Dk05bt+TEtrHllnPPB8AdT8gkeZqJRyP7pZc/wCH411+h/8ACybXQrGDTtP8OizWBPJ+d+VxwTg9T3qP4V6Va658Mb3Tb5N9vdXUyMBwf4eR7g81asvCXxA0Kz/srRvE1g+nplYXu4SZYl9BwRx9fyo/4H5D/wCD+Zk2Gi+IPDPhLxpc3hs4jdxNLHFZSblichg+B24I/Kux+GVtbW3w90gWyKokh8xyv8TknJPvn+VO8KeCLTw7o13ZXMzahPqBLXs8o/1xIIIx2HJ/M1hWfgvxn4aSTT/DHiKzGlsxaKO+iLPBnqFIBz/nijbT0A1b208OWWjeKU0Y2y3jwSvfRxSZZX2tjcufl6mj4Uf8k20j/ck/9GNUnh3wLDouhajZ3N493fasHN7eMMF2YEcD0GTUHgHwz4l8KxNpmo6lZXelQoRbLEpEisWzzkdOT3NC6r0B9zs6KKKACiiigAooooAzPEWnSapoVzbQHbcbRJA392VCGQ/99AVNpGpR6vpNtfxAqJkyyHqjdGU+4IIP0q7XOxn/AIR/xK0J40/WJC8Z7RXOPmX6OBkf7QPrQB0VFFFABRRRQAUUUUAFFFFABRRRQAVQ1DWLPTJ7SC4ZvMu5PLiVVySfX6VfrjtI/wCKj8ZXWsN81pp37i29C3dv5/mK6aFKM+ac/hivx6L7zGrNxso7t/8ADnY1QvNYs7HULSxmdvPvGIjVVz07n0FXiQoLEgAckmuQ8OA6/wCJb3xFIMwQn7PZ59B1P+fWihSjKMpz2ivxeyCrNxajHdv/AIc7CiiiuY2CiuXTxsG1pdLOjXyTM+OVGducbsenekuvGwttZfSxo19LMrYARRlh/eA9K6/qVe9uXpfdbGH1mkle/kdTRWDqviS4sL77Fa6Je30gUMWjXCYPvzUmheI49ZmntZLSayvLfBkgm6gHoQah4aqoe0tp8vy3K9tDm5b6m1RXMap42g0fUzaXunXccW7aLgr8rDuR69afpfi86jqENs+kXltFc58ieReHxzz6frVfU6/Jz8um/Qn6xS5uW+p0LyRxgGR1TPA3HGafXF+LdYsROLfVNCvpoLWUMk6kohYjse9dkrbkDDuM1NSg6dOM319P8yoVVKbiug6msyopZ2CqOpJwK5y78V3kd7NbWfh2/uhCxVpAu1T9ODmrFread4x0OZJYJBGG2TQuSrIw5xkU3hqkUpzXu6dnv5X/ADEq0JPli9TbSRJF3Rurj1U5p1ebeD/Ek2n6Q1hZaPdahKkrO5i4VQenPPPFdnoXiG012OQRJJBcQnE0Eow6GtcTgqtBy0ul1/4HQijiYVEu7NEXEBfYJo92cbdwzmpa4LW9B07SPE+hTWMJje4uyZCXJzyD3PHU13NxcRWtvJcTyCOKNSzsegArOtRjFQlBt83l528y6dSUpSjJWsSUVyX/AAnMkytcWWgX9zZKTm4UYBA6kDH9a3LHXbDUNIOqQy/6Oiln3DlMdQR60qmFrU1eUf6/QIV6c3aLNGiuRHjqZ4TeQ+Hr+SwGT9oHcDvjH9a6LSdSi1fS4L+FGRJlyFbqOcf0pVcNVpR5prTboOFanN2iy5RRRXOahRRWfreoSaZpr3EVpPdN93ZAuWGe/wBBVQi5yUVuxNpK7NCmSTRRY8yREz03MBmuA8LeK7210SOF9J1LUCHb9+ilgeemat/EK0trnw9Dqslu8dypRV3kgorckEdM13/UJRxCpVHZN2T0f4XOVYpSpOcVqlex21LXIReOhFHDNc6Newae5CLduOPrj0/Gt3WdYGk2aXC2dxeGRgqpbruPPr7VzzwtaElFrfbY1jXpyTaexpUVzNr4xc39va6no13p32ptkUkvKs3oeBil8capPp+hzRQW1yxnjI8+IfLD05J7U1hKvtY02rX9Be3hyOSex0tFcdoniy7NlY276FqcpKIhuAmQ3bdn0712NRXoToytMqlVjVV4hRRWD4h8UDw9Ivm6bdTxFQTMgGxTnGM+tRSpTqy5IK7KnOMI80tjeork08exTSLJBpF7LYlwjXQTgE+3er2r+K4NOvhp1raT6hfEbjDAPuj3Patng66kouOv9b9vmZrEUmm7m9RWBpPiyK/1D+zbyyn069I3LFOPvj2NZHxA1y6t7N9OhtbqNXZN10owjA9VB9aqng6s6ypNWb/Lv5iliIKm6i1sdmk0UjFUkRiOoDA0+vP/AA/pGmT6zbNFoer6e8P7zzpHIRiOzZ9faty+8YpHqElhpmm3OqTw8S+TwqH0zzVVMG1Pkp66Xd7K34tfiTDEJx5p6ff/AJHSUVi6H4mttZmltTBLaXkHMlvMMMB6j1qjqXji30nUzaXunXcMYYgTso2uB3X1FZLCV5TdNR1X9fM0demo87eh1FFc5pPi1tS1GK1l0i8tEuFLQSyLw4HPPpXR1nVozpS5ZqzLhUjUV4sKKKKyLCiiigAooooAKKKKACiiigAoopGYKpZiAAMkntQAtIzBQSxAA6k15zqXivVPG+qyeH/BkjQWkTAXusDOEGekfqT69/pzXSaV4F0XTAHmWfU7j+KfUJTOxPrhuB+AoA1ptY0uBWaXUbVAgLNmZeAOvem6Rrema9aC70u9iuockbkPTkjkdR0NUta8I6Bq+nywXek2bZQhXESqyHHUMORXmHwjt/8AhHY7PWbi52WWttJaMH4VJUbMfP8AtAOPr9aAPa6KKKACsHxF/oWo6Rq68CG5+zTH/pnNhefo/lmt6svxJYSal4cvrSH/AFzwkxf745X9QKANSiqmlX8eq6Va38X3LmJZAPTI6fhVugAqG7u7awtZLq7njggiG55JGCqo9ya5rxj8Q9F8HQlLiT7TfEZS0iI3fVj/AAj6/hmvLYbLxp8Yb8T3Tmy0dH+U4IhT/dH8be/6igDY8V/F6+1a7/sTwTbyySSnZ9qEZLv/ANc17fU/p1q14O+DY84at4wkN3dOd/2TfuGfWRv4j7Dj613XhTwRovg+08rTrfdOwxLdSYMkn49h7CuhoAZFFHBEsUMaxxoMKiDAUegFPoooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACsbxNoNx4h09bSDV7rTMPl5LY4ZxgjafbmtmigDK8N+HrLwvokGk2G8xRZJdzlnYnJJrVooo3AKKKKACiiigAooooAKKKKACiiigArO1/TW1bRbi0iYJMQHgc/wSKQyH8GArRooAoaLqa6xpFvfKnltIuJIz1jcHDKfcMCPwq/XOXB/wCEa11rzppWpyAXB7W9weA/sr8A+4B7mujoAKKKKACiiigAooooAKKKKAMDxjqz6ZobpBk3V2fIgUdcnqfy/pV3w/pKaLotvYrjci5kI/ic8k1Ld6TZ317a3lxFvltGLRHccAn279Ku10yqx9iqce93+n3L8zFQftHN+i/U5vxtqUlrpK2Frk3mov5EQHXB6n+n41r6PpsWkaTb2EWMQpgn+8e5/OifSbO51O31GaLdcWykRMScDPtV2idWPsY04+r9f+Av1BQftHN+iCiiiuY2OX8ZWM8X2TX7FC11p7gsqjl4z1H+fU03whaT3lzeeI76JknvXKwo45jjHQfp+ldVRXZ9bl7D2VvK/lvb7zndBOpz3+Xn3PNtZuFm8RXsXiSbUooEbFpDaqdjr659aPCVxHpniydPsWopDdoscPnpuYdDlj2FekEA4yAcdKWuh5gnSdPk0atvp6pWMvqj5+fm632PPPFWt297r2nD7BdyRadcN54aAkOMjp69K67RNfttcEv2e2uYfJxnz4tmc+n5Vq0Vz1cRTnSjBQtbbXzv2NYUpxqOfNv5Hn/jXxDDqmmzaZb2V750c4yzQEKdp5rpNG8SwawXt7a0u45Iot2Z4tqntjNblFOeIpSpKmobefe3l5BGlNVOfm/A8qWWC8mnPiOTWZNT8whba3UhV9AtX/CGsR6HaalBdWN/uMpkAEJY44GCfWvRcDOcDPrS101MxjODg4aO3Xa3bTQxjhHGSkpary/PU848H+JLbQNMkt9RsrqEPKzpKsJIfpx9RWroDTX3iLUvEv2Oa2s2gCRqyYeXGMnH4V2JAYYIB+tLWVXGwm5yjCzlvrfQuGHlFRi5XS8jznXfE0Gp6rpF1BYX4SynMkgaAgkcdPyrfvLseMPDGoW9hBcQyYCqJ02biCDgfliunoqZYuFockLOO2t+t+w40JczcpXvvoeT2lxHZ2qW15rGvWM8Q2tbpGdq/wC7z0rf8PLFp3hbVri2tL65RiW8q8iCebxg4xnI9a7gqpOSAT9KWtauYe0jbl3ab1/4Cf4kU8JyNO+39dzyjzNFhtybSXW9NvCv/HrGCyhvQeo+tegeFmv28PWp1KLyrgKQV27TjPGR2OK1tq5zgZ9cUtZ4nGKvDl5et7t3f5fncqjhvZy5r/oYsuvSf8JVHolvaiXEXmTTF8eWPpj6fnW1WfY6RDZahe3wdpJ7xwzMw+6oGAo9q0K5arptpQWyXzfU3gpauXf8AqOZS8EiL1ZSB+VSUVitDQ8/8M+JbXw5o50vULW8W7ilfMawk5ye1O8YazJqfheGI6ZeQTXMm9UaPOFU9TjpnNd7tBOcDPrS16X1yn7ZVvZ+9e+//A/zONYefs3T5tLW2OE8X6tHf+ELaKCzuw11goDCRtCHnPp7UzxBqt1d6ZpUifbrTSpQVunijIlBHGD6Diu+pCARg0oYyEFFKGzb37/LpoOWHlJv3t0lt2PJLpdPgvbC80q21ea2huFaSScFg2OflGOteg66JNY8H3RtIZC9xb7kjZcN64x61tAADAGBS0Vsd7Vwly6x7u/mFLDcnNrv5HE6X42sbPRrWyWzvZryGJYzCkJzuAx1rsLWZ7i1imkheB5EDGN/vIT2NS7QDkAZPelrmr1adR3hGz9b/wCRrShOCs5XXoFcT8QdUSTT5dHjtbp5yUfesRKYznrXbUUYaqqNVVGr2+Q6sHUg4p2uc54f8S2N88Gm21jdwFI+C8G1Bgetcxrun3GleKry9ubnULW0vPmS5slzj/ZavSqQgEYIyK3pYxUqjlCOjVmr3/G36GU8O5wUZPbY8z01LO/8QWEkd/rd/JDKCsksPyoPck5ArT+IGqpPb/2TFa3TzRTJIXERKEYzwe/Wu5AAGAAPpS1o8enWjUcfh21/yRCwrVOUL7+X/BMPR/FNrrN0bWG0vImCbt00O1ePeuGaym0DU7yDUL/VLBJJS8c1ouUlHqeeteq0hAYYIBHvUUcZGjKXJH3X0v287foXUw7qRXNLVHn/AIWitbjxTHeQ3Or3brGwM9zCAhGOhOc0zxJrlte+JNNlOn3kkOnyuJg1vndyOg79K9DAAGAMUtX9ei63tHG+llr6+XmT9Vfs3BPd32/4PkZei69b64krQW9zD5RAPnxbM59K1KKK8+bi5XirL7zqimlaTuwoooqCgooooAKKKKACiiigAooooAK898YjxB42e48P+GpY7awgby76+kYqsj94lwCTj+LHfj1rq9evZkSHTLF9l9fkpG4/5ZIPvyf8BB49ytcfe6TZaxrSaVpXigWVlploVnsTb7gVJIaUM3yluvzc4PPWgC34X+Hmq6DYR2kni27SBMnybKGOJcn3IJP1ro5PD0jxbF17Vo2/vrOuf1XH6Vxs9vY+J/E1lNb+JLptKuYzb28P2bMchiGX2SN0PynL4z1ANU/FUUnjnXpdL0PxFYSuHUxsL2RGtgo+cKija5Jyc5J7cYoAteJ9P+IHhywudRsPFMeoWUMbNLFdwIrhcc4IGD+lY3jzTpNF+F3hrwtGmby5nQbO+/BLf+POBXoV7ZM8Gj+GnuJLrGyS6lkOWeOLBy3+8+0fnWG9kfFfxYFyw3ad4ajCA9nuW5x/wEYz7gUAdrpdj/ZulWlj5ry/ZoVj3ucs2BjJNW6KKACiiuU8Y/EPRfB0JS4k+03xGUtIiN31Y/wj6/hmgCbSry20C51bTb2eO3trV/tkDysFUQyEk8n0fePxFef+K/i9fatd/wBieCbeWSSU7PtQjJd/+ua9vqf061zOoL4t+Jjya7fQtb6RadXRPkjj3DdtHWQgcn6fhXtHhDwZoXhSwX+yolkklQF7t8M8o+vYew4oA4fwd8Gx5w1bxhKbu6c7/sm/cM+sjfxH2HH1r1iKKOCJYoY1jjQYVEGAo9AKfRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFAEVzbQXtrLa3MSywzKUdGGQwPUViaPdT6TfDw9qMrSfKW0+5c5M8Y6ox/vqPzGD610FZ+taVHrGnNblzFMpElvOv3oZB91h9D+YyO9AGhRWb4f1N9V0eG5mUJcrmK4jH8Eqna4/MH8MVpUAFFFFABRRRQAUUUUAFZmp65baXeWVpIkks17JsRYwCQO7H2rSJAGScAVyHh8HxD4pvdfcZtrX/R7TPT3Yf57104elGSlOe0V+PRGNWbjaMd3/AEzsKzL7XLax1ay0xkeSe8J2hBnYB3PtWi7rGjO7BVUZJPYVyXhVG1vW7/xLMDsZvItAeyDqf8+9FClFxlUnsl+L2/z+QVZtOMY7v8up19FFFcxsISB1OKWuF8f3+oRy2cCWLiCO5jdJxIMSP/dx2rc0vWdbvL5Ibzw/JaQsDmYzAhePSuyWDmqMat1rfqv8znWIj7Rws9PJm9RXN6l4puF1STS9F01tQuoRmZt21I/Yn1p+keJ5LrU/7K1WwfT74ruRS25ZB7GpeErKHPbpfdXt3tvYr29Pm5b+Xlf1OhooorlNhMgEDPJ6UjukSNJIwRFGWZjgAVwGu6rqyeNtPZdJk3weYsEXmj/SBg8+1dNpd7qGrie31bQzZwlMfPIGD56jFdtTBypwjNtWavuu/rqc0cRGU3C23kzTtb6zvgzWl1DcBOGMThsflVivN9Bvr7StX1iw0XR/tRNySBv2pGoyAM11ug+I11a1umuYDZz2TFbiNjkJ759ODVYnBSpNuOsdO19e6FRxCnpLfX008zborkU8XatqRebRNBa6tEJAmkkCb8egrY0DxBDrsEpEL29xA2yeCT7yH/CsamEq0480ltvqtPVdDSNenJ2T/wCD6GtRRVe+a4TT7hrRQ1yImMQPQvg4/WuVuyNkTGRFcIXUMeik8mnV4J4fg8Havayv4t12/s/ErSt5slxK0flNk428Y9Ov6V6L4K8OXS+AZtK1rUPtQu3lP2i3uS+Y27h/zP40+gdTtqK+dbOzutKubzxjodzcPpekagscUcspZpo+jt9OR2/i9q7r4xrBqXgew1q0uJQRKnkNHIVVlkHcd+g+nNHS4dbHqFFeKx+Pb6D4byeHXL/8JGk/9mKmfnIPAb8vlz64rD0rw5Dc/CvWdbubu9F9ZXBVAtwQny7Ryvf7xofUFrY+hqK+fNH03wtr72ejaXd6rNq91Ys5lN0VijnCE7SCuSMg8ivaPBul3mi+EdO07UCDdQRbZcNuGck9e/WnYVzboorM13XbbQbIXE6tI7tsiiT70jegqoQlUkoxV2xSkoq72NOq0mpWMV0LWS8gSdiAImkAY56cda5p/FmtWCC61Xw68FkSN0kcgZowe5H/AOqs/wAZy2NtqGia7a26yvLL5haP70oAXaK7aWBlKooT63s009Ur2OapiUoOUene60O+orkX8Xavp4S51fw+9tYuQDKkm5o89MitnVdUvLezguNK046kJufkkC4XGQeawlhasWk7a9bq333saxrwknbp5MvRXlrNcSW8VxE80X341cFl+o7VPXGaVrDw+KY7e58ODT7rUQxeYy5ZgATn8xWtrviUaVcw2FpaPfahOMpAhxgepParnhJqooRW6vuvnqnaxMa8XFyb29TdorlofFl9Z30Ftr+kGwW4bbHOkgdM+hq5rviQ6Zdw6fZWb32oTjckKHAUepNS8JW5lG2/mrffsUq9Ozd9v62N2kJAGScVyX/CW6tY3tpa6voX2f7XKI0kSYMOTz/Oq3xGvb6OxS2SycW3mI/2oSADdk/LjrWlPA1JVY020ubrdP8AUiWJgoSkunSzO3orntN1vXbq9ihuvDsltC3DTGYHbx1xXQ1zVaUqTtK3yaf5G0KimroKKKKyLCiiigAooooAKKKKACiiigAooooAKKKKACkJCqWYgADJJ7Utch8R9Ve20CPSrSUJeazOtlGwP3FY/O34Ln86AKJ8SJp2n33ji4tJ7tLyRbawiiUkrACQGPXAY5Yn021WvdX0vT9Al1Wfws+7WZjaM0ULjfCf42GNyryflAyfxqKPxbrVrrMuh2OkmzsLB4oLaeSMGFogQGeSQsABt6BQTmpvEPjHWbXxpY6bpMonjluUVoVhVonhwN7GXOQwOeOMAA0AVrHRfC/hLws+rXGk3NrNfRSwqjTESLGQ33TIQIyVGcHnnHNXfh/4e0Ww8OW2tw3F+tihkuoYr8InkcFWc7RzwDgk4waoeMvFHiS41L+zvD8azOLhVjhFos8MseM72lJIHPGMDGOa1tQvJ/FWv23hSMobWxRJ9akh+4zcFYB7EjJHoMetAGnaXc8Wl3XiF4Cb3Uiq2cD8EJyIUPpnJZvTcfStTw/o0ehaTHZq3mSkmS4mI5mlY5dz9T+mKq6dcrretXF2nNnpztbwEdHl6SMPYfcH/Aq3aACobu7trC1kurueOCCIbnkkYKqj3Jp07SpBI0MYklCkohbaGOOBntXhb6V47+KusOupBtN022lKMrqViiIOCFXq7e/6igDT8V/F691a7/sTwTbyySSnZ9qEZLv/ANc17fU/p1q14O+DY84at4wlN3cud/2TfuGfWRv4j7Dj613XhTwRovg+08vTrfdOwxLdSYMkn49h7CuhoAjSCGKAQRxIkSrtEaqAoHpj0rn9HnXw9f8A/CO3bhLdiW0yVzw6d4c/3kPQd1x6GukqtqGn2mqWclnfW6TwSDDI4z+I9D70AWaK5W1kvfB0ZttQkuNQ0gMTFfMTJLbD+7KOpUdnHTuO9dLb3MF3AlxbTRzQyDKSRsGVh7EUAS0UUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQBz8P/En8XyQdLXWV82P0W4QYcf8CQA/8AaugrI8T2M15oskloM3lmwubX/ronIH4jK/Rqv6few6lp9vfW5zFcRrIn0IzQBYooooAKKKKACiiigDnfGupyWWjC0tcm7v28iEDrz1P5fzrT0TTI9H0i3sI8fuk+Yj+JupP51NPp9pc3UF1PAkk1sSYnPVM9cVZrolVXsY0o+r830+5GSpv2jm/Rfqcx43v5UsIdIszm71NxEoHUL/ABH+n51u6ZYRaXpsFlCPkhQKPf1P4mlk0+0mvor6SBGuYVKxyHqoPWrNE6qdKNOPTV+b/wCG/UI037RzfogooornNTmfHNjd3el20tpA1w1rcrK0acsVHoKbF4uvr6aOKw8OXzEsA7zjy1Qd+a6iiuuOIiqahOF7Xtq+phKlJzcoytc4pW1Dwjruoztps99YX8nmiW3G50PPBH40+1XUPE3iey1WTT5bCxsAxQzDDyk+3pXZUVbxmnNyrmta/wArbd7EfV+nN7t72/H8wooorhOo5LxVFd2niHStaispru3tQ6yrCMsM98fjVi08UX9/cj7N4evVtlVmeSb5DwOAo7nPHWulorr+sRdNRnC7Ssnd+v6mHsZKblGVrnEeErjULbVNVe40S+iW8drhS8ZAGMnbz3Oag0CO/u7/AFu2udJvbSPVtzLLJGQsXB4OfrXfUVrLHXcmoJOSXV9NvyRmsM1yrm2bf3/0zyeHSBpam01bTtc85CQr2UgMTj1HHFdR4I09La6vLhNN1G0WRVG+9kBMnPpgGuwoq6+YzrQcWt/N/kTTwcack09vIKzPEj6hF4b1F9KDNfLbubcIuW344wO5rTory3qjuWjPIT4kkl0mGz8YfDu+1HVPLC+cLNW870O7GVPrjNRWEPirwp8NLmwg0K/lutVml8iGBTIbGNgB82MkE84/WvY6Kb1v5iWljxXSfAGjv4Ik1G98L6+L+3AR7TzCsk7cZZV9OT27d6yJ38WXXw7h8KzeE9Zd7a5EkU5tnx5YJIUjHXk19A0UdQPLho9vLer8RG8M6uNRiYJ/ZPlDe7gbRLjGenPTqM1y9i/iG1+HuseHm8Ha002oXDSJKLZtqhiDyMZ/h/WveaKGC0PHNO1W4sINOuF+G+tDVdPs/s8V0luwGduCSMc9+td98P7jW7rwhay+IVnXUNziQXEflvjccZGB2rpaKdxWCub8X6ZfXQsNR0+ITz6fN5ggP/LQcZx78V0lFaUarpTU10JqQU4uLOK1LxHqOt6dLpdl4evUuLhfLczphIwepz/jis7WbTVLRtF0+z0m6um0kq5mEZMcpOCQD9RjmvRqK7KeOjTa5IK2ul3u1b8jnlhnNPmlqcRq2v3+v6bLpFl4fvo57gbHadNqRjPJz/8AqrrNLszp2lWtmX3mCJULepAq3WbrOm3epQRpaapNp7I2S0QB3D0NZSrQqJUkuWN79XqWqcotzb5n9xiaz/yUXQv+uMn8mqj4y0C4k1yLV0t7q6tjGI5ktH2ypjuODxW5pPhVbDUf7SvdQn1G8C7Ekm6IPYVv1v8AW1RnB0ne0bPpfVv16mfsHUjLn0u7/dY8rGm2V7Ikdto/iO4+YZ86RVVffJUiul1iC/0bxSmv21jJfW72/kyxxcvHjuB/nvXX0Up5hKcleOlmrNt3uEcIop666dOxyEviS41ie2isvDFzLIkobzLyPasXqQfWrvjnT7rUfDrR2cRmljlWTYvVgOuPzroqKwWJUakZ0425fNs19i3GUZyvc5RPGF9dbIbDw3fvLwG85dir+P8A+qt3V76fT9Jmu4LRrmWNciFOp5/pV6ionUpuScYWS83qVGE0neVynpN5NqGlwXdxatayyrlom6rVyiisZNOTaVjSKaSTdwoooqRhRRRQAUUUUAFFFFABRRWB451O40bwVqt/aMUnigPlsP4SSBn8M5oAx/Enj26g1ddC8LWMeqamATOzsRFbjGQWP4+tZTR+N78A6j4rhsQesWm2oJHtvb/69Q+B7nTZfCNmNNIDyLvvcNlmmJ+Yt37ZH1rdoAw38KrckG+1/Xbw9997sU/go/rXDX0HhmPxTazSwXsmjxM8E00zyPGZhkfeJzjp0r0rVrz+z9IvLzn9xCzjHqBx+tcX4Uk1SPTNlt9l8QaVLy8W5UlgY8spVuDyTQB1lpoPhwWw+z6Lp00LjIYx+YCPqSc0y6s/DGlx+dd2Gk2yA5/eRIozXO6lfaZpFzDaweFZ0mnUsFEZC+wwhIJJ/KtkW90kSPZeGLOOcqCTPIgCnHP3QSaAOT8Ta34SeyuJtO8PedLghbqGBoYkY9CSCM8+1EulW3hvw9ZfZL2+/t3UwpiFvdMgd253EDsM4p3ijVtR8hdP1LVtNdZ5UR9P0+IyOV3DOWPTj9au+DtOu9a1248U6rC0e0mKyhdceWBxwD0wOPrmgDp9F0nUtCsobax8SX0axjmOWOOaMseW4IB5JJ6966K18XG0McOuRpEGYIL2L/Uk9twPKZ98j3qlVe+ks47OU37xJbFSJDMQFx75oA7wEMoZSCCMgjvRXEfCnVGvvDUtuHeS3tLl47R3+80Oflz645FdxQAUUUUAFFFFACViXHhmOK4e70W6fSrlzucRKGhlP+3GeCfcYPvW5RQBz/8Ab1/pXy+INPKRD/l+swZIfqy/eT8QR71t211b3tulxazxzwyDKyRsGVh7EVLWJceF7X7Q91plxcaVcudzPaNhHb1aM5RvrjPvQBt0Vzw1q/0SRYvEUcZtmO1NStwRGPQSqcmP65K+4roAQwBBBB5BHegBaKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACsHwsPsw1PSx/q7G+dYsdAjgSgfhvx+Fb1YWh8a/wCI0/6fIm/OCP8AwoA3aKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigArL8TI8nhjU1jjjkf7LIVWRAykhSRkHrWpTJYxLC8bDKupU/jQB4dpnhrS9V0LTdb0i4udIvJ4iJ/sr/J5inB+X074z3q8kXjbTwBBqOn6pGO1wpjc/j0/Wq3gF3h0zUNJc86ffOg9cH/66109AGOPFGvWoxqXhO5K93tJBID+Fc+t/wCHLLUX1CxfWNAuH/1kf2XdG31U5FdyGI6EilLswwx3D35oA5+Hxtp0i7T4otlPq1iyt+rYqG61Lw3qa41DxfPNF3hjkEKN9QoyfzroGtrZ/v20DfWJT/SoW0nTWOTp9qT/ANcV/wAKAMa11b4d6Vsa2NmrxMGVxCzuD67iCaut8QdOm40+w1K/c8ARW5A/M1oJY2cf3LSBfpEo/pU4+UYXgeg4oAxzqXi3U+LbTrXSIj/y1u5PMk/BR/WsrXdPstG02TV9cubjXLpCBHHO22LcemEHausrivifcbNFtYO8s+fyH/16APSfhZqEmr+EY9Qlgihd3ZAsS7VAU44FdpXLfDWxOn+AdLiIwzReY31JzXU0AFFFFABRRRQAUUUUAFFFFADZI0ljaORFdHBDKwyCPQiucty3hTUIrGR2bRrt9lq7HP2SQ9Iif7jfwnsePSulqvfWVvqVjNZXcYlgmUq6nuKALFFYvhW5ubjSGS6lM7WtxLbJcHrMsbFQx9+MH3Ga2qACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACsLS/k8X68n95LaT81Zf/AGWt2sKw/wCR31jH/PnaZ+uZqAN2iiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKAPE7NP7N+KXibT/urOwnUfiG/9mNdJWL4yj/s34z2VxjCX9ptJ98Ef0FbVABRRRQAVj6h4ij07UFtJLOdt5VRJwFJPpVW51DU9W1Waw0qVbaK24lnIySfasnWotXtrqxg1C5W5h88NHKFwc5GQa7qOGTklNrVbdTnqVWk+XodzSUp60lcJ0BXnnxHJvNc0vTlySR0H+0wH9K9DriLi1Oq/F7T7YfMsKoxH0yf6igD3TSrcWmlWtuowI4lX9Kt0gGAAO1LQAUUUUAFFFFABRRRQAUUUUAFFFFAGD4WP2ddS0t+JLO+lOO5SVjKrf+Pkfga3q5/Xo5NKvovElsjOsKeVfxKMmSDOdwHcocn6Fh6VuxSxzRJLE6vG6hlZTkMD0IoAfRRRQAUUUUAFFFFA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

[Example_of_the_Stack]:data:image/jpeg;base64,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KKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiorp5IrWWSLbvRCy7hxkClgl863jlxjeobHpkU7aXAjvUuJbKWO1dY5nXarn+HPGfqBzTXt3t9MNrp+yN0i2Q7ui8YBP0q1RSAhtLaOztIraLOyJQoz1OO596o+JdIl17w/eaVFdLam6TyzK0XmbQevy5Hb3rUooeoLTY4j/AIV9dPe/aJ9ajdGuTPIi2ZXduh8lwDv4yOQe3vVqx8IalHJpkF/raXVhpLq9rEloI5GKqVTe+45wD2Az3rraKAOY0fw1rWma5eajLrttcR30okuIV0/YWwu0AN5hxgAdjWFF8KVt7xfK1CFrNLjzlWWGVpB827bkShfx216JRQtLeQPW4Vy114X1WO81FtK1e1gtdUkMlxDdWPnlWKhWKncAQQBwwIrqaKAOVuPCmqxXl1PpOuR2o1CJEuxNZiTLKmzemGUKcDpgimQ+C7vSZUbw/q6WitaRWs4ubbz9yxghWX5lw3J45HtXW0UAecf8KpmSCzK6xDNPawm33SW0io0e4svCSg7gSec4PpXZeGtEXw7ocOmLIknllmLIhQEsxJwCzEdfU1q0U7huYmuaFd6rqmk3lvqMdqmnTmYxtbeZ5pIK4zuGOCex61z118N572wliutZSWf+0HvoXW1ZFVnGGVgJMkH2IIrvKKX9f19w7/1/XqcVp/gO70/RdUsoNTtYZ9TASSVLSRlVMEEYeUknB6549Knm8FXWoeEj4f1PV45li8r7LNBaeT5WzGMjed3T1FddRR/X3COS8KeCn8PanNqE1zbSySQ+SBDFKuBkHkvI/p04rraKKLgFFFFABRRRQAUUUUAFFFFAENp/x5w/9c1/lU1Q2n/HnD/1zX+VTUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFAEN15n2SXykLyFCFUEAk445NJZ262llDbqqqIkC4UccCp6Kd9LAFFFFIAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooA//Z

[Checked&UncheckedExceptions]:data:image/jpeg;base64,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ft9zfS2FxbzSkLFKikkhgOV6HOOnvVhfF+p6emuQaxp0D3mk2y3SiydikyMDj7wyCCpz1qOy8E3tpcaRcPeQzzwajNf30hBUO8iEYQYPAyOpHAq/c+H9TfxBrGpWd9FaNe2MUFvKF3tG6FjkqRgjkfr0oe39dv8AMNL/ANd/8iHwz4k1XWLuLzF0i8s5oi5uNNu95t24wrq3POeo9ORXV1xOmeENS/4Sey1q/ttGsHtFfe2mK4e6LLj58gADvjnnvXbU2SgooopDCiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAK4n4o+MbnwjoEMlgpN5cTqEYrlUVSCxP14X/gR9K7auK+Lf8AyIFz/wBfEH/o1aAOq0rUI9W0q11CNHjW4iD7HGGQkcqR6g8VboooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAqarYLqmkXmnNIY1u4HhLgZKhlK5/WubXwXqSqFHiBcAY/48h/8AFV19FAHI/wDCG6n/ANDAv/gEP/iqP+EN1P8A6GBf/AIf/FV11FAHHt4HvZXi8/XQ8cc0cpVbQKW2OGAzu45WuwoooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigBskaSxtHIiujghlYZBHoRRHGkMaxxIqIgCqqjAUDsBTqKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACims6oMswUepOKb9og/wCe0f8A30KAJKKj+0Qf89o/++hR9og/57R/99CgCSio/tEH/PaP/voUfaIP+e0f/fQoAkrivi3/AMiBc/8AXxB/6NWux+0Qf89o/wDvoVxfxZmibwDchZEJ+0QcBh/z0WgDuKKj+0Qf89o/++hR9og/57R/99CgCSio/tEH/PaP/voUfaIP+e0f/fQoAkoqP7RB/wA9o/8AvoUfaIP+e0f/AH0KAJKKYssbnCOrH2OafQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFYOseOPDGgzm31LWbeGYfeiBLuv1VQSPxqp8SPEE/hrwTe31q+y6fbDC391mOM/UDJ/CuC+Hnwp0rW/D8Wu+ITcXM16WkSISlQFyQCxHJJ69e4oA9M0Xxj4d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

[ExceptionsEx2]:data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAoHBwgHBgoICAgLCgoLDhgQDg0NDh0VFhEYIx8lJCIfIiEmKzcvJik0KSEiMEExNDk7Pj4+JS5ESUM8SDc9Pjv/2wBDAQoLCw4NDhwQEBw7KCIoOzs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozs7Ozv/wAARCAFlAmEDASIAAhEBAxEB/8QAHwAAAQUBAQEBAQEAAAAAAAAAAAECAwQFBgcICQoL/8QAtRAAAgEDAwIEAwUFBAQAAAF9AQIDAAQRBRIhMUEGE1FhByJxFDKBkaEII0KxwRVS0fAkM2JyggkKFhcYGRolJicoKSo0NTY3ODk6Q0RFRkdISUpTVFVWV1hZWmNkZWZnaGlqc3R1dnd4eXqDhIWGh4iJipKTlJWWl5iZmqKjpKWmp6ipqrKztLW2t7i5usLDxMXGx8jJytLT1NXW19jZ2uHi4+Tl5ufo6erx8vP09fb3+Pn6/8QAHwEAAwEBAQEBAQEBAQAAAAAAAAECAwQFBgcICQoL/8QAtREAAgECBAQDBAcFBAQAAQJ3AAECAxEEBSExBhJBUQdhcRMiMoEIFEKRobHBCSMzUvAVYnLRChYkNOEl8RcYGRomJygpKjU2Nzg5OkNERUZHSElKU1RVVldYWVpjZGVmZ2hpanN0dXZ3eHl6goOEhYaHiImKkpOUlZaXmJmaoqOkpaanqKmqsrO0tba3uLm6wsPExcbHyMnK0tPU1dbX2Nna4uPk5ebn6Onq8vP09fb3+Pn6/9oADAMBAAIRAxEAPwD2aikzVWPVLCaURRXkDyHoqyAmhXYFuiq63ls+zZcRt5hKphh8xHUD6YqC01a1uWERmjSfcymEuC2QSD/KnZiui/RVaO5Z7uW3aPb5aqwIbO4Ekfh900kN4s17PbqUPkquSrgnJzwR26D86LMZaoqt/aNn9p+zfaofOzjy943Z9MVYzxSAWiqw1CzNybYXUXnDjy943Z+lJDdNJdzW7x7TEFYENnIJIH/oJp2YFqiq8d9aSzvBHcxPKmdyBgSMdaRL+zkuDbJdRNMCQYw43ZHXiizAs0VWS/tJLg26XUTTDOUDjPHXirBOFJ9KVmAtFZFprjXU8cf9m3kKyYxJJ5e3kEjo5PIHpV6K+tJpmhiuYnkT7yK4JFNxa6CuizRVZL+0lmaGO6ieVM5RXBIx1qK21a0vQ4tp1ldN37tWG44OPX1FHK+wXRepKzLTWHu5I0OnXUCyj5ZJDGQOCedrkjoe1Wo9Rs5fLEd1C/m58va4O/HXHrihxa6BdFgIoYsFAY9Tjk06qqajZSXH2dLqFpskeWHG7I6jFCajZSPIiXUTNGCXAcHaB1NFn2C6LVFVYdRsrhzHBdxSOBuwrgnHrTLLVLO/JFtcJIykgqGGeDjOKLPsFy7RVa2u0uWm2MjLG+wMjhs8AnOOnXGKItQs55HjiuopHjBLBXBIoswuWaKrW+oWd2xS3uopWUZIRwePWiC/tLmVooLqKR1GSqOCaLMLlmikPQ1Xt7sXFxcRKhAt3CFj3JUNx+DCkMs0wopcOVBI6EjkU+igAooooASoPsVt9o+0fZ4vO6eZsG78+tWKSgBaKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKr3d3FZxeZKTgsqAAZJLEAD8zViqNzZG51G3mkb91b5ZU9XIwD+Az+ftQVFK/vbE32uI3htFOZVjEjADoCcDP1wfyp7TxrKsTOA7glVJ5IGM/zFVrGza3kuZ5nWSa4lLMwGMKOFX8B+pNQalpCX13b3SmJZYAygyQh+Dg+owQR1pa2LUYc1m9O/n/AMOaJkTB5HHXnpTDcwCZITIu+RSyr6gYyf1Fc7H4PRFuEF4W84YJdCTjeG+Yhhn07dasR+GUh+xMk0RktQ6qzwA8MwbgZ4Ixwee9K77Gjp0F9v8AB9v8zfJwM5xQCCMiquoafBqdr9nuRlMg8AdfxFO0+xh06zS1gBEak4yB3Oe1UYWjy3vr2Fgv7W5kkjhnR3iOHAPK8kc/ipH4VL5in+IVmaxpKTafOtnaw/aZMMrH5cOCWVs4PRiT+JrPHhBDJbSi42tEq7wUzlgxYsCCMEknP4VN2bxp0pK7lb5XN+W6ggiaSWRVRSAST0JOB+pp8E8VzCk0Lh43GVZTkEVj6b4cjsbu4nkkWZbj7yeXgfeLZJJPc9sD2raiijhjWOJAiKMBQOAKa8zOpGnHSLuPooopmQUUUUAFFFFACGsHT45ryGSEeWsAu3kLFGV8CUsBgjBz6+h6VvUU4yshNXMtbW+SVEQQGFLhpdxY7mDEnGMcEbvXnHaobfTbtIltpFtxH9pNwZEJJH7zfjGOvbOemeK2ulZ8OsxTbT9muUjMnleY6AKHztx1z14zjHvVqUmtBWSHRx3i6lJM0UIidFTIlJYAFjnG3/a6ZpscN4urS3LRw+VJGsfEpLAKWOcbe+7pmnjUo2EOIpR58jRAkD5WXPXn/ZNQWeqkoFuY5M+a0RnCbYywYqO+ecY9M96LS3sGg6G2uoykRhtmiWTeJDnd1z93H3vfPvWj/DxVS3kuBqNzDLIjxqiPHtTBXJYYPJz90elOhuGkvriIh1EaphWUDqW5BzznH6e9S7sZXtrW6h8uBordoonLCViS3f8Ahx97nrn+dPiivF1Oad44BFIipxISw27jnG3HO71p8epLLKqpbTtGzFVmCgoTz75xx1xirh4pttbgrGPbaffR3kM0rK3lk72ad235HUKRhfoPzottOuo76OZhGiozM+yV2V8g9EPC8nOR7+tWbfWLe6u2toUkYo7IzDaQpGc5Gcjp3HNLY6hJdvIrWc0QR2Xe23HBx65qm52J0K9rp9xHepKwSNVZmbZM7K+c9EPC8nOR7+tavaqUeqwS3xs9rLKM4yVOcewJI/ECiw1CS8Zw9nNEFd13ttwcNj1zmpkpPVjTSFjhuPtc7SJGsUigKUkJYY9scdfWqWnaRJZvboy7lthhZDcyHPykA7DwOD6mtC2uHluLlGDKI2ACsoGB65BOQfwpsGpLPJGEt5/KlJCTbRsbgnPByAccEineWqDQq2enXEF5HK/lxqoO4JM7KxPoh4T14NWLeK8gZ49kJiLu4fedx3EnGMcdeuaus21SwBbAzgdTVKLVo5fs+LecefuPIHybeu7nileUkFkirp2m3FjIClvbx7/9cySsTJgNjgrxyetLaaddwXYun8ndLuEyhjhOeNnHGe/rVq31OO4kjAhmRJuYpHUBZO/HORxzyBS2l00090H3KIpAArKAVG0dwTnPX8apynq2FkV7azuUihtZIrfy4BhZVJ3dCMgY+U4Pqe/rVey0ySx8oyruW1TiQXMr7htI4Q8Dj3NTHVZJb+yjjikSG4ZgTJH98BSQQQeOnQjkGtOaQQxPIVLBQThep+lJuS0fULJmNpME89lYFvJSK2G4bUZWLbSMFT06nPXPtV60iu4HaJkhMXmOwfedxDMSBjHHXHWo7XXILqZIlt7iPeQAzqAMldwHXuOf54qW21WC5u3tFVllVSxBKngEA9CcdR1x1py59boFYZFBds9ysyRIk/eOUll+UD+6PSo4bS7U24kSBVtVwpRjmQ7cDt8o9ue3pVq1uHle5LLIPLk2hGUAgbQexOc9c+9R2mqxXjxqsE8QlQyRmRQNwGM989x1pe9qGhFaWVxbpZqVhHkQtG+1j1OMY4Hp7UzTdOuLa4SSQRxqkZQpHKzqxOPuq33AMdAf5VbW5eXUZYFA8uGNSx7lmzx+AH6iqdhqk1zMqSCEM0JkeAErLEeMAg9e/PHT3p+87hoa56VRsIXgur4MhCyTiRGJzuBRR/MHj6dqXTtQe+j3vaSw8kZfbg4JHY+1FpqaXjkR21wApZWd1AAYHBHXnp2yKnlaugumXqKo2d40q3TuJP3UhHllAGUbQccE565z70yDWraZN7xzQKYTMplUDcgxk8HtkdfWlysd0aNJVGHVUlu47ZrW4ikkRpF8xQBtGOevuOOtLZy3E11eCR08uKURxqFwR8oJJOeevpQ4tbhcu0tVLJ5289J3WRo5du5V2gjAI4yfWrLNtGcE/Sk1ZgtR1FULTVoLyWWKNHEkS7ipKkkc+hPp0NJFrEUsbym3uEijDFndABkdR1yT9OPenyS7BdGhRVCLVUkuGge1uImWPzDvUY2/gT+VFhqsOpqTAj7doYPlWU/ipIz7daHFoLov0VT027N3ab3x5iO0cmOm5WKnHtxmrlJqzsMSlqnY3D3JndihRZWSPaOw4OTnnnNXKTVtACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKxdZn1eK8txp8W+LjzflB7jPJ9s/41tVmalrUGmzxRTRTP5v8SKNq8gckkY60mbUb8+kb+RnyS63bNfqiTTs0uYDhdqKdvfOTgZ4x2psNx4ilFkssTQMwcXDCNWAO75T9705OKtjX0jW8ae0mRbaXy1IKnzDkAAc9TnpRH4kgnS1aCzupTdByoCqCu04YHLDGDU6dzp/eW/hr1+X9MXTP7Qjv7uK8aaSMys0TFV2heMAHOf07Uan/aEerWk9uZmtgjrLHGFOSSpGckeh57VNp2pvfTXMbWkkIgmaMMzKQ2MehzTrzVktL+Cz+zTzSTqWUxhcADGc5I9RT0sZPn9q/dV7badjHutR1aytLy9upRDHC+Yo5IkXzUz0B3H5iAR07itzSnuZNOhkuypmkG8hRgAHkD8BgVV/tqNIb2WS3lP2SYRlFUFjkLjHPP3qqp4oibUbS3EDlL1CYQMbgQxDZ5xgY9c0rpGkoVKkdIL1+X9M6DGaMVmadrtvqV1JbwwzK8S5k3hfkO4rtOCeflP4Vp5q0cc4ODtIMc0tFFBIUUUUAFFFFABRRRQAUUUUAIa56K3/ALOsbi81Wee2tLeSS4eNmVkA3F93ALcdcZ7dK6KsHxz/AMiLrn/XjN/6Aaak0mkJq5jnxP4ca4WUa7dCNJTNHEto+0E5zz5eSOT+dJB4l8Nx7RJrt1NEsnm+U9q+C+7dnIjz15x0rr7Mf8S+D/rkv8qz47i5/tFBLLKgklYKhiBjdADjDDocYPJ7HirTk1uDSMWPxZoEeoNdnxBdvuABjNm23AzgcR57+tEXizQI79ro+ILtw2AYzZttIGcDiPPc966KzuL2W5nWWGERJIVDLKSegPTb7+tJBfXU97cW4tECW8oR5DL1yoYYGOuGGen1NL3tRaHPweLPD1vMCmuXP2dSSIPsj4Ge2fLzj8avHx74a/6CD/8AgLN/8TWnbyyNqt1FICNkcbKA+5cEvzjAweOevamWupXE7p5tqkcckrxKwl3HK7u2Bx8p70mpMLpHOxeJvDKXkVzJrVxMYiWQPZvkEgjlhGCRg9P8Klj8X+HorppE1u4ELMXMP2N8ZPXnZnGeetbceqXDy2n+hoIrt8I/ncgbS2SNvoOxNamKbcuo1Y4i28ReGba5hmXW7giHOxPsbAYI6HEeT9etWIvF/h2K6Mia3cCEsX8n7I+3J687M9TnrW5pt1ez+a1xDCqLLIgZZSTwxA42j+dRWeui7uIkFuRHN9xhuJHGQW+UADA9T2qmpu4lYxrfxboEN41w3iC6lD8GN7NsHrjpGDxn1pbXxZ4dtHRU1y5NvGMRwG0fCjsM+Xkgdufzrbg1h5tQNo1sIzuYAszAnHcAqAc/7JNSaXdXt0shuIYlVZZEDJISflcgDG0enWk+bqCsZ3/Ce+Gscag//gLN/wDE1Th8WeFYbqef+0pm87+BraXameuPk7nk11rHahbjisu11r7TcpD5CLv7iUNj8MVMVJptDbRhW3irw3byRk61cyRQjEMTWsmE4x1CZOAcck/jRbeKvD9vdSzya/dTiX70clm208YHSMHp712JFZlnaalb3QM96LiEK6lWGCfmyh4HUAlT64Bp3bvqFjnl8S+HFubeVtfu3W2bMSG1fAGCMH93k8HrV+fxz4bmgeManKhdSu5bWXIz35TFaVnqs06xPParCkysykSbiMdcjA/z6VJb6hNK0DSWyxxXP+rYSbm6FhuGOOAehNDUr6iTRzUXiTwvEUYazckq0bc2r8lUKdo+46/piktPEnhq0uIpV1y4YRoUC/YmUFTjg4jz1A5rorO01JLtZbq+3xgOTGoGCzNwOnRQAB65OatW9xLNc3ET24jSJgEfzA3mcZPA5H403KWuoWRzFt4s0GCaSQ+IryXzeSr2ZAzgAHiMegrV0JrLU7WzvdP1OW7htVeAMUC7+gIYFQcjA6YrcxXN+COLLVf+wxef+jTU8zHZGz9kYX006thJ4gjgdQwzgj8D+gqO20x4Zkklu5rjylKxiTb8ue+QAScetaFFLmYWKFvp8ttI229mMR3FYyqYUk564yetFlp8tmsim+nnDlmAdUG0kkkjCjue9X6KHJsLGbbaXNbvcMdRuJfP5bekYw20LkYUdAB7U1dFj2wJLcTTRw2zWxRgoDq2M5wOvyjpitSinzMLIx7Cxu11I3M7zsscTRJ5zIScsDwFHT5ep55q3aQXEF1dlxH5UsokjYMd33QCCMcdPU1doocmwSKlnFOhme4VFeSTdtRiwAwAOSB6elSXdut1ay27FgsqFCVODgjFT0Um7u41oZdtozW07zi9lLtF5fEcagDsQAvUU+30sxWsttPdzXMcgIw4QFc5zgqo9a0aKbnJisjGtNPvDcTy3E1wN8PlKzsm8cnkbRgfz/KrNnphtLh7hp2mkZdmSirxnPO0DJ+taFFNzbBJFTTrQ2dqI2ILszSSEdCzEsce2TVuiipbu7jKlnBJbtOrBdjSl02nseeR9c1apaKG7u4BRRRSAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACqd1aWE08cl1DA8q/6tpFBI78Zq5WNrGgxateQTvMUMJHAUHoQf6DrmkzSny83vOyLMtjpc0sry21q8jDErMiliPf8hSLp+kxmKRbW0Ux8xEIo285yPxrOk8KxusqrdbQ+75hEA53OGIZup5GO31pIfCcEX2NZJUuEtN4VZoFfIZsnr+VLXsdCVK38R/c+xsR21iLlriKGATuPmkUDcw9zST2thJdRzXEEDTr/AKt3UFh9CeazdF0Z7K9u7ueKONnYrBGjbhFGTuIHA6sSfy9KXVPDUOpanFfNO6sgUFeSPlO4Y54OaNbbEcsFUs56W3/QuHTtIxJm0tMScyfIvzYOefXkUpstL2IPs1oRgCP5F6AkjH0JNZUfg+CJ53W5JaZgxBhXaCH3jj0z1HQ9evNJN4PgluIbhpzuiwSiptUkOX4APy8n3pa9jTlpXt7R/czTtIbHSobmb7TuDuZZpJHBOcAckfQVd+0xeYiBsl87cc9K5zTvCgTT5YbwxK8sTxbYkUqAW3ZztGSOMZ6VfGhuJrOUXKK1oSVCW6qDnII9hg07vsTUjScn79/l5aGt58IBJlT5eD83SnK6uoZWDA9CO9c7/wAIjAVKNcZX5QAYlOQHD/N/eOR1PqfWtjTrIWFoLcSbwGYg7QuMknGB9aav1MqkKaV4yu/QuUUlLTMQooooAKKKKACiiigArF8Y28154O1e2tonmmms5UjjQZLMVOABW1SdaAOVt/GPl2kUbeG/EO5ECn/iXnqB9arW2u2FrKskPhrxKNn3Ea1kZU+ilsCuzIypFYGn6faQ6kYI7lmltUi580lmI3BsjPfvVx2eomZ//CR232s3Q8O+Jg5OSotJAhOMZ27sdvSmW2vWlpdSXMXhzxP5krFn3W8rKxOB90uR0AHTtWnaaley3Ubu6hJJPLaFmjAQ+g53bh7/AJCnQahcvqkebpXglmeNVjCsvAbjswPHJ5HHaqcJLqK6MmPXbOK9a8Xw74oMrdSYJSD1/hL4xyeMd6WLXbOBYRH4b8TAQyNKgNvIfmbOSctz1PB45rZ01pY7m4FxqW//AEh0EThRk4yAO/TtVHSfs4uA0hiXFw6wGO4Lu/zuMMD0GMetPleuoXRmx65Empx3S+G9fRImLIosZDyVI4BbCjk9B6Vq/wDCar/0LfiH/wAF5/xqa11K4kv44XvI2tzI4ScKMTn+4PQrz9ccd8S2l3PM0Nw9/GplYq1oyr8pAPyg9dwPXORweBSlGT3BNGQniK2juzcp4c8TBmJJUWkgTJ6nbuxn8KSHxDaW84mj8OeJlI6IbWQxr9F3YH5VpWGo31xNE0kgUXGVMbGMeWwB4UA7iQRyDn8KTT9SuJDbM2oR3EkzmN7cIFKAZy3qD0Jzxz24puE1fULozLfXbK2lWSPw14mPl/cV7WRlTjHALYHFPj8R2sV21xH4d8TBiSxQWsmwE9Ts3YyfpW1pjSJIwuNT8wmaRREwUHO4n69O1OsbiP8AtG9jE8UrEqy7QoY8HjjrjFS07vUEZ3/CaL/0LfiH/wAF5/xpf+E1X/oW/EP/AILz/jVq0vp3mtXN4k32rO+EIB5OFJOO/BGDnue3Sk0+9uSbOSe9SdbsMNoRVA2jqMfTn+lL2bsO5W/4TVf+hb8Q/wDgvP8AjSN4zRgQfDfiLkf9A8/41a06/uJr+PfcrLDcKzR7ApUgdMYww/EH6jvtdvelKPK7ME7nHRa/ZQC3EfhnxMBbbvKzayHG7rnLfN+OcUtv4gs7aYSx+GfEmVzsVrN2VP8AdUthfwrZ02SWESefqHnuZJVSFgoJIc9O/Tt71Dpmo3k8sMk0q7LhSWRjGPLIBPygHPGOQc/hV8stdRXRB/wmi4/5FvxD/wCC8/41VsvEtvYLN5XhrxEWmlaWRjp5yzH15+gHsBWlpuo3E97DFLeI0RD+W+wD7Xz1X02j8+vStuTcEYoMtg4471MouOg07nO/8Jqv/Qt+If8AwXn/ABpng63nk0XUPtNtdWRu7+5lVJVMcqo7kg+xwa1LSfVZLlVuLfZFzlvLUdvUSH+VaLfcPzbeOvpUtWYJnCaN4Z8aaDqV/dJrkerROwWCHUJJCWTr94E7Gzx905x26VsjxbLp4A1/RL3T/WeJftMAHrvTJH/AlFWLK9u/JhllulumubZpViCKvzLt4XHPfnOfwplne31wwAukcXEbGNmMeFOOCoU5Iz2Ofr2q/ZsXMamn6vp2rQ+bp19b3adzDIGx9cdKt5riE03SvEmo23nWHkzCMyNcwjyZJAMLnemGB35GM9qvz6D4js7eWPS/EJuY2QqsGpx7yMjtKmGH1IalKDi7MadzpwaWvP7bW59Lubua80W7WS2dvnsZDdQ/6teDj5gM85K8Z9q2dB8Tw6pMTDqltdxlGdgJIw0ZGOig7gOvXn3p8nZiudRSZrE027vZrryproSebAZFZQjKDkDKkc456MOfXimae7DRit1qPnM0DHYxCsuOvI5odOwcxugjNOrmdIaGONJJZ4re4aBtpjnMi7dqku2e4Oams9VvJFleVwzRWxaKIKAbnH/LQegPAx2z9Mt0mr2DmOgorGF5PDFJMmoRXrGBpVhVVHIxjGP4eo5yfeqo1G/S2uSLkSEWzzo7GMkEYxhV6qc9/bk5pezYcyOizRmsW0u5riQRR6mlz50JcsiL+5PAGMduTw3PFP0SR/7OhE2oiZ2gVsNtBQY5Pvz60nCw7msGDdDnnHFOrF0+8Eel3bJNFNLDJKSVAG75j8xC/n71HLqFzbxXCpfpc4tXnEuxf3ZGNo44IOTjPPHU0/ZsXMb1JWRDeTwSTpPeRygWwuFdlCheuen8PA9T70mk3d3JcSQ3c3mHyxICChHJPQrjj0yM+5pODs2HMbGaKz7A+ZfaizsSwmWMA/wqEUgfmxP40aMzHS0BcsEZ0RjySquQp/ICk42Hc0aKoaVdNe2huPtKXEckjGJ0jKDZngc9fr3q/Sas7DCiiikAUUUUAFFFFABRRRQAUUUUAFFFFABWDr1pfXl/ZLD9p+yoxabyHVe3GcsD+Vb1YureIrXS7+OzmhmkeRQxMaghVJxnrzz6elJ26m+H5+f3Fd6leV9aAv1t7ecM86GCRvKI2ZUNxu9M4zjp61A8/idXtgtq7hJD5p/dfOnmY9eDs54PU1ZHiq3O8fZLhSHKIDs/eMJPL4+bj5iOuKu6NqEmo2JuJY/KcSyIU9NrEep9PWp0ezOhynCN5U1b/gW7/wBMoNFe+Vq8f2C7KzNugHnJydoHHz8fMCe1QSX2pre6fp8UgilnjVZIpNheLaQWY4zkFQwHvirM3iZBa3MsFnK7RwvNEGKgShTg9+OcdcVoafNcT2ST3capMQSVXHA7dz/OjR9QcpRjzTgv+Db5l8dKWuZi8bWcpYG0uUIXKqQhL/d4GG6/OOKuW/iCO7ewaOORI7wPguACCAeDzkHg9jVcyMJYatFXcf63NqisrTNcj1OV41glhZV3L5hX5huKkjBPdTWoDTWpjOEoO0haKKKCQooooAKKKKACiiigAopKWgAopKKAA9Khhe3leTymR2jbY+3BKtgHB9+RUx6Vx2l2B0rXroPaarK8l2XidJWMJQqBubLYODnrzwK0hBST1E3Y60RRiTzAih+m7HP50CKNXLhFDHqQOa5HTbSa48QXTXEeuxQNOHti8zCNQAC2fm6FgQB0xio9Mtru48QHShfXElrpsxuGuBdMxlVwNkbc9uc/QevOro7+9srkc3kdl5MfmGTYpc8Fsc0xWtvtJgUIJVTeVC9BnGf0/SplqhbHGu3gZhloYig6Hblvz5zz71zrUsveUgxhQMdOOlIIY1cuFAYjGcc0+lpXGRGBMsygK7DBcAZqKysVsoBCJZJQvRpNucenAFWqKd3awWIxDGHMm0bz1bHNAhjByEUH1AqSilcCMQxqxdUUM3Ugcml8pBj5Rx046U6louBGsMaMWVFDHqQOTT8UtFAEYhjVzIFG89WxyaBDGGLhQGbqccmpKKAGCJAQQoGOnHSn0lFABiggEY7UtJQA0RIMYUcdOOlIsMaMWVQGbqQOTT6KLgIEVegxS0UtADFiRSSqgZ64FZmpeF9E1aQS3mnQvMOVmVdkin1DjBH51rUUAcwPDer6WzNoevSFScm31KMTofbeMOPxJpBreqaax/tnw3Lt/jutNIuEb3KYDj8jXUUUXAx9L17QtWYx2F7byS9GiPySD2KHDD8RWqI1HIABxjOKoap4f0jWgP7S063uWUYV5EBZfo3UfgazT4Z1GwGdE8Q3cIz/AKi+/wBKi+g3EOP++qLgdAsMaElEVSeSQMZqG5sYri1mtwTEJlKu0YAPPXtWGNb8Q6YT/a+gfaYl63OlSebn38psMPw3Ve07xXompyiC3v0S57204MUo/wCANg/pTvrcDSt7cQQrHvaQgYLsBlvrgCnCGNSxVFG772B1p+aWi7CwxYkXO1QM+gpBBEoIWNQCckADmn1Q1jXdL0CzN3qt7FaxDoXPLH0A6k+wpAXREg/hHTHTtSJDHHnYoXJydoxmvPJvjZoBlMen6Zql/t/jigAB/M5/SiD42+HxKIr/AE/VLAnvLCCB+Rz+lFwPQhbxrK8oUB5AAxHfGcfzNEdvFFAsCIFjVdoUdAPSuf8A+Fi+EPIhmOv2gWf7o3fMP94dV/HFb8dzFPbrPBIssTqGR0IIYHoQe9AnpqOhhjt4UhhQJHGoVVUYCgdBT6i8/wD2aPP/ANmnZke0h3JaKi8//Zo87/Zosw9pHuS0VF53+zR53+zRZh7SPcloqLzvajzv9mizD2sO5LRUXn/7NHn/AOzRZh7SPcloqLzv9mjzv9mizD2ke5LRUXnf7NHnf7NFmHtI9yWoLixtLt1e5toZmQ5UyRhtv0zTvO/2aPO/2aOVjVWKd0yH+ytPww+w2+GBB/dLyCcnt681LBaW9snl28McKZztjUKM/QUvnf7NHnf7NHKxuumrNkR0ywIlzZwHzjmXMY+fvzxzUsVtDBEIoY0jjHREUAD8KPO/2aPO/wBmjlYOunuyD+x9MwR/Z9rgjGPJX/D2H5Uf2TpuUP2C2zH9w+Svy854445qfz/9mjzv9mjl8h/WP7wyHT7O2YNBawxMBtykYXjOcce9WKi87/Zo87/Zo5WS60XuyWiovO/2aPP/ANmizF7WHcloqLzv9mjzv9mizD2ke5LRUXnf7NHnf7NFmHtI9yWiovO/2aKLMPaR7kd7di0ijfbu3ypHwem5gM/rVkdKo6vby3WmSRQAGYFWQZxyGB/pV5fuioV+Zm7S5E+uojEgHFUtFvJL/R7a6m2+ZLGC20YGavGobO0hsbZbeBSsakkAnPU5P6mtE1ytdf8AhzPW5NRiloqRjSBjB6Vj6cdNtroCx0kWq3BKieOBEWTHPJHPrjIrYPSsm10+5jvI5nSCAgkzNC7YlyD/AA4wOTnPXiqjazEy+NQsyqsLqEq8nlqQ4wW/uj39qRL6ye7a3S5ha4XgxhwWH4dazrTy7jV5UifdbwHzQuCP3jZB6joOT9W9qfb6dPFepLsjjVZHdtszMGznohGFPOSQfX1quWK3Fdly21Wxu5mhgu4pJFJBRXBPHU4p66hZPNJCt1CZIgS6BxlR7ioIormKeRVihMTuW37yGwfbHr71TtNImtvIQxo4gzska4k54IztxgE555otDuF2aMOqafcSLHDe28juSFVJAScDJxVrIrDttIuYGhYrADGkAO1j/Bu3dumG4rTj+1m5nEoiFv8AL5JQnef724dPpilJRT91jTfUcl/ZyTSQJdRNLHy6BwSv1HalF7auYwlxExlXegDj5l7keorPtrC4j+yQyRwCO0ORIpJZ/lI6Y4znnk0sVtercWwZIBDA7nIclmBBxxjA60+WPcV2WbLV7HUGZLa6ikdGZSisCflOCcelW3dY1LOwVVGST0AqhZQXNrI8XlwmIzSP5m87sMxbGMds469qmV7lZrlrkQi2UAxFSS2MfNuGPyxUtK+g0Og1GxuZTFBeQSyABiqSAnHriiPUbKWVIo7uF5JM7FWQEtjrge2D+VY+hQTzadp5KwLHbrkFchidpGCCOOvPJzV/T7aeCWdpre3TzZC+6OQkk9s5UdqqUYq6uJNss215HcPOEdGWJtpZXDc45zjp+NEGo2N05S3vIJWUbiEkBIHrxUFvHepdzPJBAqSY+7KSRgem0VBaWFxCLAMkK+QHEgRievTHHPvRaOuoXZastXsdR3C1uopWUkFVYE8HGcelPt7vznuEdDGYH2kkjBGAc/kar2Nvc2jNEY4TEZHfzA53YZiwGMe/rS2kV7Hd3MksMAWYhhtmJIIUDH3R6Umo62DUsW+oWV25S2u4ZmUAkRuGIB6Hil+1Kb1rZVJZYw7EdFycAfjg/lVCw064tF09GWEfZoWjk2Mepxgjjn7vtU8UDxazcS7SY7iNMN2BXII/IjH40NR1sO7GWWsLeTrCbeWFijN+8A6q21l47jg/QirMeo2U0kkcV3C7xAl1WQEqB1zUzL8pwBnHGay9N064tZ42dIokSIoUSVnUk4+6GHyjjoD/ACzR7rv0FqXLHVbHUAfst1FKRnKqwJHOM4qSC/s7pnW3uoZTH98I4O3646VTtre+ghkt1ECA+YUmDEkEklTtxjjPrUVlYXkN8txIqbRCYyGuHclsg55GAOO3/wBam4x11C7L66lYyECO8gclS4CyA5UdT9ODSWOqWWopm1uYpTjJVWBI+oFQabbTWwlWa3gTfI8m6NyxJZiecqOxAp1hFdWwWF4ofKXP7xXO5ueOMf1pNRsxpsvO6xoXdgqqMkk4AFVLHVrHUYvMtrqOQBdxAYZUe/pVsjNZ+nwXdpAtu0UOyNCFcOct6ZGOPzNJWsDLC6nYOcLewMdhk4kH3R1P096d9vtPkIuYj5iF0w4+ZR1I9RVPTraSxtZRcwwRrueRmiYtnJJOflHaotGVJ2kmV/MigJggJBBC9TnI+g+ij1quWOrFdk2n6sNRbalrNGBEshMgAxuzhTz1xg/QiiWx0rxBYqb6wguUOQVnjVijA4Iz2IIPT0rQxjkDrVLSLZ7exPmKVeaWSYqeq72LAH3ANS7NNrQeqMaHwy1qXPh3X7uzVG2tDJILqEMP4drksv4MKkOqeKNMJ/tDRYtRhH/LbTJMPj1MT4/RjWvpEU0dlvuYYYZ5XaSRYVwASe/qcYye5q7Sej0BGcNbtzoU2sNFcRQwxPI8c0RjkAUHIKnBzx+Nea+DvDLfEO6k8Y+KibiGSRls7PcfLVVOOR6AjGO+CTXqeoWUeo6bc2M2fLuYmibHXDAg/wA68t06w+Jvgm0bRNI06y1SxRmNvOzAFQTnoWXvzg5+tIZ1mveOPCvgZksJQFlwCLWyhBKDsSBgCm6V4h0T4iJGdOusJaybrqyubZGMqEEAENnAz3Brk9Pj0n4dRz674yuEv/EeoEyCBAJHUeg7DnqeBxgdOWeHfDeveKtR13xKgk8NDU4BDaeWMMBuQ7scHkJjPGdxxQAl1aWvw81DVnu9IuF024u1niuLazSaOSAgg27FvuDcfxrtvh7ZT2PgOwjuMAyK0yIrbhGjsWVc+wIryvx5p/jLw/o8en6x4qj1GC9cRpaBmaSQA5zyucAgd+9e06DYyaZ4X0+xl/1ltaxxv9QoBprcmfwsh1jVV0iG3neEyRy3EcDENjyw5xu9+cfnVTVfEsWl65YaW9u0jXh5kDYEWTtUn6nirHiWxOo+Hb63UHzDCWjx1Dr8y/qBXLRh/E2h63q8IJeSKJbU9w0Sh+P+2hP5U5SaZNClTnDmlts/na39eR0Wr+JE0q4uofszTfZbI3bkOBxu2henU4J/CtaCdJo1KsNxUErnJGfWuDkm/tXwp4m13nbeRiOIn+5GoHH/AAItWk+k2Oka14cksbdIJJWkjldR80q+UT8x/i5GeaFJ3Lnh6duXZq/4K7OsM0YkEfmIHPRc8/lVSPV7WTWZdLV/38MSyNkjB3E4A5znjNeb6s9tL4Xu9VtbOzh3zM8d3dXG68Z9/YAcH0GeAK6yytrMfEG8laGATmyhdGKgMWJcMR3zjr9KSndoJYSMIuTb0T+9W/zOhmuZI763gWDfHKHLy+YBsxjHynk5z26YqdZY2YqrqWXqAeRXO68R/wAJPpG5zGPs92S6jJX5F5Fc/pEVvpV3o8pg067SaZY7e+sZCkzlgeZUP3h3PPFPn1sRHDKcOa+tv8/8jttW1W30exa8uSSgZUCrjJJIA6/Wo4dZhl1i708gILaGOXzi42tv3YH/AI7Wb47ggm8Mu08SOI54SC6g7f3ig/oSPpVKDRtK1HxpqKTWkE8ENlbiJNoMYB3dB06Dihyd7BTpUnS55X6/p/mdhuAUszADGc9qFdXUMjBgehByDXmCG5m0vQLJpLc2f2q6jIvSxhJR2EatjrxnAPHFdJ4StmtNX1KFbmwMYEZe1sQ/lxPzzzwCR1A9KIzu7Dq4NU4OXNt/nY6p5I4xl3VR0yxxSl1XG5gNxwMnqa5K4gsL3xteQa4sMkUdnG1pHPjZglt7AHjOce9ZdnLHFDprCX/iXwa/IlrIzZUR7HCgE/w5JAo59RRwqlHfW1/vVzuL/ULfTrO4u53+S3jMjqpG7GPT3p1tfW9zaxXCSKFkjEgyw4B9fzrjNZe2vr3xWEMdwselxg4wwDAOfzHFJ9l0SXWvD0Fytt9lbTpCkfAjeTKHBHQ9zg9x60cxawkeXW99/wALndGRAoYuoDYwc9c9KZcXMVvE8kkgURoXYZ5wK8/maC3ivFtGUaTba3amFgf3acr5gB7KG/DmtXU5LPUPF88AaK5VdFlDrkOB84IBpc+gvqaT1en/AA3+Z0umajDqunQX1vkRzoHVTjIzzg471kat4qk0rTTPLYL9pkvfslvAblMSEnAYt/CO5B5FSeCo7ePwjpv2cRgNAjSeXjl8DJOO9cVPZWl3Yxm5topv+KueP50DfK0h3DnscDIq77HPOEY1JLomz0SfVFsNCfVNRjEIhg86ZI3D7cLkhTxu9B0zVSLxLbz6lp9rHFlL60e6EpcYQLt4Pv8AN69qZ4xtoW8D6xAYEaNLGQom3gFVJXA9iBj6VzFvpOk6jrXhW1a1t5bNdKmk8pQPLZsx5yBweSTz3p9TNJW1O4vb2S3hhktrcXXmzIhxKqBVY4LZPXHoOTVkzRLKIzIgc9FLDJ/CvNpbeKztLmytkEdvb+LIFiiX7sYIjbAHYZJ496r6zbWltca1qjppmr20d0zzNJI0F9bMMfKjEdsfLjGaVx+zPSdUvhpulXd+U8xbaF5SgON20Zxmq9jqz3jozWvk272cdyJmmU4LdVK9Rgd+lQeI5BL4K1SVVZQ9hKwDdRlD1rirr/Var/2J8R/9DobsKMU0emLNG7FFkVmHJAOSKUyxiQRmRQ55C55P4VwZ0bT9HuvCN1p9qkFzPMI5pl4aZWhYnef4uRnmuZis573Q9Q1C/udCt7wXMnn3Vz5v2y3kDkLjHIxxgAcii41C+p7DNIY4XdF8xlUkLnG446ZqG3u99hBc3QS2aVFZkaRSEJGdu4cH6jrVacynwzIbhw832I+YwUgFtnJweRz2rghYR31r4cdJNKup49Eh/wCJfqqsI2UhcujYxu4weuKG9RRjdHp29P7w/OivEvK0X/oVtN/8H1FUV7I9o1SG9ubdILGYW5Z/nl6lFx2HrSaRdSyxS21yQZ7R/KkYdG4BB/EEVLqL3i2jfYIUknJAXzGwq57n6VnWuj6jaI1xHqO+8lO+YOgMbnGMY6jgAZFccrqd0j1Y8sqVpNLt3LuqjUJY44NPKxGU4kuG58pe5A7k9B6Vk29zaaP4kSw/tRnjmt2Mi3NzvIkDDHU8Egnj26VvXEbzWckXnGCSSMr5idUJGMjPoaxdL8LWNjuN08V6zR+X88Sgbc5ORzkk9SSTXdSlHkal/X/DHDK/NodCDnFOqpp1mlhZR2scryJHkKXOTjJwPw6fhVuue1noaoQ5xVGx1Brwvm1liCu67mxj5Wx61eqnHZSxXDMt24hLM/lbFxk5J5xnqc01azuJ3GxavbTTpGofbIxVJCBtYj05z2PUc0kOrwTTpAkc3mM7KVKcpjuw7A9j3qG10KGzuEeEqscZyiCFMj23Yzj9fenQ6O0FwlwLyZpg5MjkLmUHop46DtjpV/uxamnmsl9WaS8slgR1huJGXe8fDgIxypzx07jkdKurBKt1LK1y7xyKFWEgbUxnJBxnn3qoujMHtx9um8q2fdDFhcAYK4Jxk8EilHl6jdyePUo5nRVjkVZSRHIy/K5Azx+XfrVWx1k3dxHDiBmZmV0ik3NFjPLDHAOPzIqeHTGhaIfapGhh/wBVEVX5eMDnGTgHj9c0lvpPkJCPtEjSQuWEuFBIJyVPHTn+VV7motSe2uGlubhGyBGwAVlwQPXOec1HBqsF1cGGJJDhmXfgFcjrnByPxxSwWE8N207X0sgfqjIgHGcdBnvUVvpHk3iXMlw0zICFZo1DHjHLAZP+etL3NQ1G6bqb3Dm3mHmzpJKrvEmEUK5AzknBIAqePVIZFtyI5Qbh2RQV5UjOc+nSorbSBayiaO5lDlnaX5VxLuYt8wx2zwRzSWFtJ9vubmW3lhDECNHdSOQNxABOMkDP09zQ+TVoNSf7WW1VrOPGIoRJLkc/MSFx/wB8tn8KZp+pNehy1rLEEd13PjHysR69eKk+xlNVN4mMSwiOTJ5+Ukrj/vpv0pkVg8MzlblzAzs5hKrjLEk84zjJpe7YNRINZtbiWONRIvm58pmAAfjPHORxzzjii21aC7mMUSSnG758AjI6g4PB9jiobPRI7KdXjddkYwiiFAwGO7AZP+etOtdI8i7S5kuGmdF2hmRQx/3mAy1N+z1sGo/TtRa/jYm1liwzrlgMcMV9evFS2F2bk3Eb48y3mMb46dAw/wDHWFNt7GS1mJW6fyC7P5RVcZYknnGepp1jafZjcSMQZbiYyOR07Af+OhRSly62GrkkF5HcXM8Cxyq0BCszxlVbIz8pP3vwqeqlhZyWvnmW4kmaaZpMuSQgJ4VR2AGP1NW6l2voCFopM+9HepGLRSUZpgLRSUtABRRSGgBaKTNFAC0UUUAFFFFABRRTWYIpZjgAZJPagDyf4c2Np4l8W+IPEGsItxqEF2Y4YpRnyFycEA9xgAHtg1s+LPHWqLr3/CL+ELJbzVtoaaZsFIB784yMjk8DPeuBu9Dv/iJ4s1LVPB1oLC0Vykl087Rid+7YHQnrgD3PJrd+G/meBvFkvhnXtPSC+1Ebob4SbhLjooPTB59DngjpgA6Pwt8OJrbVl8ReKNQOrawMFM8xwntj1I7cADsK7yX/AFZpwxTZf9Waa3Jl8LK3aoraztrOAQWsEcEIJISNQqjJyePrVXWtSOk6RNerF5hjxhe3JAyfYZ5rP0vVNYuL+KK4WxuLaRWY3Fm7MEI6A5pupFS5Tz+a2hrrp1mlibBbSFbQgqYAg2EE5PHTrT3tYHeF3hjZoDmIlRmM4xx6ccVhDxbCms3VpLDOYYVXaUtpGbdznIA6dMGtDUPEGn6X5JvHkiWYAqxibAz6nHB9jSVSDV7j533HNoOjvJLIdLszJOCJW8hcuD1zxVhtOsnu4bt7SFriBdsUpjG5B6A9qqW3iCxu7a4niE+23AZ1MDBip6EDGSDjtRoeoC/sJJhdtc7JWUsYDEVx/Dt9s0+aN9CvaSfUvvbQvNFPJEjSwgiNyvKZ64PbOBVeDR9Ltbtry30+1hnbOZUhUMc9ecVnL4y0hySr3G1W2yObdwsZzj5jjirl/r1jp8ywSmWWZl3iOCMyMF9SB2pe0ha9xKo0rJl24t4Lu3eC4hSaJxho5F3Kw9wajttPs7Jt1rawwHYsZMaAfKvQfQZNV9K12x1nzPsTu4iOGYxsoz7EitGrTTV0JSdrJ6FU6ZYNZtZNZQG2YljCYwUJJyTjp15p1nY2mnw+RZ20VvHnOyJAoz+FYkfi2H+1r21lhuPKhKiMpbSFicHORjjnpWjfa9ZWEscL+bJM67xFDEzvt9SAOBUKpBq9x+0bTVyxfaZY6kipfWcF0qHKiaMNj6ZpZbCzntPsU1rDJb4A8lowUwPbpUCa5p8mlvqS3A+zpwxKkFT0wR1zz0qOw1+z1C8Foi3EU5QuEngZCV455HvT54XsHtHorlm30qwtUK29lbwqyeWQkQAK88dOnJ/OsqXwrYtq1tKtnaDT4raSI2vlDaWZlbOMY/hqO38XwPqV5byw3HlwuqxFLaQseOdwxxz0rowdwB9aIyjPYqNeabaZALCzWy+xLawi127fJ8sbMem3pUdppOnWJU2ljbwFVKjy4wuATkjjsSBRqOqWmlRJJdyMiOdoIRm5/AGq1p4l0u+uUt4JnaV+FBicfqRTco3t1J9o9rl2zsLTT4misraK2jZi5WJAoLHqcDvTP7K0/aE+wwbRP9oA8sY83Od/+9nvVvtWTqV7qFtfxQwCLyrmN1iZlPyzAZUHnoRn8qcpKKE5Pdmo6LIhR1DKwwQRkEVUtNH0ywMZs9Pt7cxBlj8uILsDHLAY6ZIGapDxNaW+l2l3fCSJ7g7CqRs2JBwy8e+astrlkmqDTWaQXBTfzE23bjOd2MYpe0j3EpeZO+l2D7t9lA26YXDZjBzKMYc/7QwOfaop9B0i6vlvrjS7SW6XBE7wKXGOnJGaqR+K9KklVBJKI3fYs7RMImb0DYxVi/16z0+5FvIJpZtu8xwRGQqvqcdBS9pC17hzeZfmhiuIHgnjWSKRSrowyGB6giq7aVpzBw1jbt5kAt2zGPmiHRDx93npVS51tH0L+0NO/fNMQlurKRucttAI69c/lTtMvLy7u7pZPLMFviIOqkb5APnPXoDxT503YObsXXsbSQwb7aJvszbocoP3ZxjK+nBxVebQtIuL8X82l2kl2pBE7QKXBHTnGakfUrWPU49OaTFzJGZFTB5Ud89KXUYLi6064t7W5NrNLGUScLuMZI64qr32GmWHRXRkdQysMMDzkHtVG50LSL22htbrS7SeC3AWGOSFWWMAYwoI4GK5I6RaaT4n0iw8PyXLajE4fUpDK7q1uVOTLkkbmONtd7QtSnpsZX/CMeH/APoB6f8A+Aqf4UVq0UybstYo2ilorE9ExPFag6Kd0fmRieEygpvGwSLuyOeMZqGxsvCeokiztNOmYdVWNcj6jrXQEc1zviN9JeLDuP7SXP2Y2w3Tq/bAHOM4znj1ropTduVXXoZyWtzbtLO2sYRDawRwRg52IuBmrFV7JrhrGBrtQs5jUygdA2Of1qYOrEgHJXg+1YO93ctbCnpWHazXY1GI3NxcKHdgAQjQzDBI2FeRgDPPXB61uYqpDplpbOrQwhCgOwZOEz1wOg/CnFpJg0V11G5MqQeVF5xuGR13H5UAzu6emPzFJFqdy2oCCW3WONnZVJDAkDOCGxtOcZxnIFS2thPHqM97cSQyPIixrsjKlVBJxyTnr/KpYtNtoZRIkeCCWUbiQpOckDoDyeg71TcELUgsZr95JjcLB5auwGxju4PHaq9prdxdvGyWreVMCUJjkGwYJBYlcY+h7960TYQGfzth353ffOM9M46Z98U1dNtUk3rHg5JA3napOckDOAeT09aOaPYLMzrPWr2eaFZrWFEkWNjtkJI3g4HIHTac/WtkuAD6jtVdNNtY9u2IDaEC8ngL938smnRWNvDczXUcSrPOFErjq23gUpOLeg1fqVINSuZBBM8MQguv9VhzuXKlhu7dB26e9SR307m13xxqJtwbDHhgCeOOnFSxadawzCWOIBlztySQueuB0GfakXS7VLhZ1iHmKSVYknbnrjnjPcCnePYWpX0i41CdZGuvIKCaVAUJz8rkAYx6CtB2ba2zaXA4BPGfeoksIEn85Uw24sBuOAT1IHQHk84pq2EMMtzcW8aJcXIG9zk7iBgZ+lS2mxq5UsNTvLiK0nnghSK7A2hJCWU7SeeMHofp71La3V/POwkt4UijdkZg5JbHQjj+fv8AizSdGj0+2hWRYXmiUqJI0K8dzgk4J7461cgsYLdi0SkFuTl2OT68mqk4a2ErkNo0v2i7WQAMHBXDkjGOOD0qCy1G7na3+0QQxrcKxTY5JBHrkd/0q5HYQRSGRFYM3U+Yxz+tJHYQRCIJGB5OfL+YnbnrRzR10CzKukXF/PEzXfkFRJIoZGOeHI6Y6cVJZF1ub6MOzBJRtDuWxlFPftk1MlhBHN5qphslh8xwCepA6AnJoisIIZGkjVgz9T5jHPGPWk5J3HqU9N1S7ujbNcQRRrdQmRAjliuMcHIHrU0UzzazcR7iEt4kAXsxbJJ/QAfjU8VhbwiERx7fIBWPk/KD1FOFqovDcgkMyBGHZgCSPyyfzNDlG7shWZQgtrvTy0897JcQxROGRuScMWU/XacH1wKLLVbq4nEb2hUOpZG8uRQp9GLKB+I/KtQjIweaqxaZawEeXFtCghBuOEGOijOF/DFCknfmWoW7FGHW51ijmvLeNY5bV7lfJcsQFC5ByBk/MKkhnvG1OAXCxoskTsBHKSOCvBB6nnqKuLYQIYysY/coY48knCnGR9OB+QpkWlWkEqyxxYdBhDuJ2j0HPA9ulPmj2CzLUhbYdmN2OM9M1R0qa/mtVe6EGCOChOSc9+BWgRVWPTreJy8aFTzj5zhc9cDOBn2qE1ZoZXsr3ULqN5GtoEVS6D94SWZSRnp0OPrSW2o3N00MaxRK5iLzqWP7ps4C+/II/wCAmrcVmltG4t/kJyRuZmAPXOM+pqHTbGW0NxJO8Uk1xJvZooyg6ADgk9hV3jqKzI9Osby2l33V88+IgoGeC2SWb8yAPQCpdKmkltGErb3jlkj3n+IKxAP5CrpGRUFraJaW4hjJwCSSTySTkk+5JJqXK6dx2sNsrma588yxxKqSsiGOTfuA7n0PXjtVmq9jYw6fapbQAhFyck5JJOSSe5J5qzSdr6AgooopDCqGuiJtBv1nnFvE1tIryk4CAqQT+FXq8l+M3ieRXtvDSGa2tZ2V7268tiNueFH971IB7AetAEHwg8b6Fpfh6TRtTvIbGaKZpEeY7VlVsc56ZGO/tUfinxRpPiz4n+GLPTbqNobG6Be752uxZTtX1+7gHplvxrptD0f4ceL9Lt7Swt7W+WxiEfIaOZV9W6NySTnpkmsz4meDdO0bwhDqXh+wjsptKuUnBhXkgkAknqcHaeTxigD1IU2X/VmvMLT4k+JPFd1b2/hLw/lE2m5urzIjHTcAQcD8ycdq9PkBZMd6aJl8LMjWYL+4sPL06WOOfepPm/dZQeQeD1rI03Q7xNci1B7Gz05IlYOtq5PnEjuMAADr611HlPjpR5T+lDhFy5jh9nJ9Dn7mz1a116fUNPgt7hLmJI2EshTyyueehyOah1fTtd1KGyQx6eTBKk8hLuAzqT8oGDxiun8p/Sk8p/Sk6cWrXD2cuxnK+r/2eSYLMXm7hBK3l4z67c5x7Vm6LY65p0k6zxWLRXE8kzMkr7lLc4AK9M10nlP6UeU/pTcU3e4ezl2OR/sPWm0TUrFxZCS9naUMsr4G45IPy9sDFF4LzQ75dR87Tw9zCkUsc8+z5lHVGI5HtXXeU/pUU1klwAJoY5ADkb1Bx+dQ6ato9Reyl2Oe8FLKdLuppdh868kdWjHyMOOVz2yDXR05YGUAKoAHYUvlP6VpBKMUhqnJLY56az1ez1u7vdPgtrhLxYx+9kKGMqCOw5HNZ2peHNUn1AakrJLNLEqTxw3DwgMO6n09jXZeU/pR5T+lZulFq1xOk30OSt/D99Bod3bCC1MtzMrtHNM8isOM5JGc8dRT9D0TULPVhcvGlnbLGVMC3DTByehG77vSuq8p/Sjyn9KapQTT7B7J9jnJLPWLHWb66sILa4jvShzLKUMZVccgA5FblsJhbx/afL87aN/l52574zzip/Kf0o8p/SrilHZj9nLsUNR04ajGqG7urbac5t5ShP1qraaALS6Sf+1NSm2H7ktwWQ/UVs+U/pR5T+lHLG9wdNvoMpMDvzUnlP6UeU/pV3Q+SXYxvEP9mnSZbbULmK2SUHYzEAhhyCPcHmsrw1Zvq+j3OoXtwJLnUIzCXQ/6tANuPY9z9a6mayS4AE0McgHQOoOPzp0dqIUCRRqijoqgAVi4JzuyXTlfY4RfCOqC3FjJGksajHmG+kCMB/sY4rT1jRL66v8Az1sbW4RY1SNhcPDKvrkjgjNdX5T+lHlP6VPsYJWD2T7GXodjdWGkw297MJpkySwOcc8DJ649a0MAdBipPKf0o8p/St1ZKyGqckrWMyCS8l1e5DxolpCqpGSvzOxGSc+nIFaHNP8AKf0o8p/ShWSHyS7GVp2nta6nqd01vBGLuVGDpIzNIAgX5geFxjgCtKn+U/pR5T+lO6Bwk+gyin+U/pRRdByS7E9GayLrXRDeSWdrYXV7PFjeIQoVCRkZZiB0q5YXF3cRs15ZfZHDYCGUPkeuRWVz0nTko8zLfeoIrG1gmeWG2hjkkOXdEALH3PepxS0bEWE7VnwZXWrtQgCGKNiQeS2WHT6Ac1odaYkEcckjqoDSEFz644pp2uIkooqGK6gnlmiikV3gfZIB/C2AcH8CKQyWlpjuEUseijJwM1DYahbalarc2rl4mJAJUqcg4PB56iiztcCzSUVG00azJCW+dwSq+oGM/wAxQBLRVSPU7SS4+zrMplJKgYPJHUA9Dj2q0KbTW4C0UUUgCims21Sx7Cqdvq1jdSIkM4ZpM7PlIDY9CR7U7MLl6iiikAUUUhoAWio45UmXdGwYAkZHqDg/rSRziV5ECsDG20llIB4B49RzQBLRRRQAUUUUAFFIelRwTx3EQlibcpJGfcHB/WgCWkpaiSdJJZI1JLRkBuDwSM9foaAJKWmkgdarW2o2t3KY4Jg7bdwGCNw9RnqOeop2bAt0UUlIBaKZFKk0ayRsGRhkMOhFOoAWiiigAqKa3guYWhnhSWNvvJIoYH8DUtITigDM03w3oujXc93pum29pNcALI0KbcgdsDgfhV65tYL22ltrmJZYZkKSIwyGUjBBp8ciSxq6MGVgCCO4NOoAjtrW3s4Et7aCOCFBhY41Cqo9gKkpaQnFABRTIphMpYKwwxX5lI6HHftTmYKCTwB3oAWimCVTH5incpGQQM5HtSW9xHdQiWIkqSR8ylTkHB4PPUUagSUUtVpL63iS4dnyLYZl2gkrxnoPbmjUCxRVe1vra8Mgt5Q5iIDcHuAR9QQRzVmm01owEopaKQCUUtFACUUtFACUUtFACUUtMllSGJpZGCIgyzHoBQA6ijPGaZBKJ4UlUMA6hgGUqRn1B6UAPopahubmG0t5LidwkUSlmY9gKAJaKqpqVrJDPKsvyW52ysVICkAE9u2atA5GabTW4BRS0x3EaFzkhRk4GT+VIB1FNilWaNJEO5XUMp9QafQAlFLRQAlFLRQBi3WgxS3c14l/e2rTkNIIZtqkgAZxj0Ap3hu5nutLLzTG4CzSJHM2MyIrkAnHsKq6paafqOvQWctrNcyGLfMRcOsccfQZUHBJPGMetb0MMcEKRRRrGiDCqowAPaklqdNSX7tRerdu2g8cU0OhfZuG4DO3POKceBxWNogE2o6tesMu115Ksf7iKAAPxLVajdN9jlbtZGw2Spx1xxXGaZpVzFe2j3el339oxy7ri+Fyvlyjnr82SvIwu0YwK7Mmudi8X2t1rp0uySO4AcI0guUBzjJ2qTlgO+PQ1rRc7SUUKVupi6dp2uw+JYNRl06VN08n2nY67SrZAwTISwHB6DpwO1XrTR203xHdzpo1zOZrgSQTpcAIilQG3ZfJIO7jB61v2eqW97f3VtDLBILbAJSUMc85BUdMEd6S213SL25Fva6lazTN0SOUMTWkq1R/Z6eZPKjm7PS7qK8gku9Kv5NRjuN8t6lyojlXJ9W+7gj5do6UzTNJv7K7srxNJuorl72Vrl/tCECFixAI34IywOAP4T689TBrGmXV21nBf28twpIMSyAsMdePaorDU5brVL2wntPIe1CMG8wMHVt2Dx0+7Q61SzvH8wcUaY6Vn+W6eITI/KS2oVD6FWJb89y/lTLHVpLjUL20ubX7MbRVfcZAwZW3YPt92pF13SJFhZNRtmWdykREo+dh2HqeRXPySi9irpla0iuBdQnybiJdzNJFKUZI+D91uucnsehPSktLNY54pJLCX7WG/eThhhuDyTnkeg7ccDFbWBUCzl72S3CfLGisWz1Jzxj8KfO3cLGNp9rdxaoly9qyNKjfaGVFVQ3BHO4lu/PP4dKsafYRrfTSyWUqHzWaJ3YEKCACBgnGTk1rkCqUOoGeVVFrKInLBZTjHGeozkdO/wClPnlK+gWSKNnaob426qrwWDmSNlOSWbkD8Mnr/smk0uC7txEJbe4kBPImMe2EYb7uD3yB/Wr1rJpcIRrY28YuX2qYwB5jDtx1PWpo7+ylm8qO4jaTnADdcdceuKHJ6qwWMnTbGeG9hlktHWHDiGMsD9lyckHn5s+2cdPepLSzCSxO1jKl4M+bcZGHOCMk5+YHPA7cdKvWWqWeobhBMrFSwK55+U4z+lPXULJmZVuYyQCxw3YdT74pylO+wWRj2GmzRTxvLHIkhUi5YIoEvykfM27Lc8g4z9OaboVtutrCaOzaNzGPPuC4PmrtIAPOTyRgEcYrXi1LTbthDHdQSmQYChgdwIz+PGaswwQ28YjhiSJOu1FAH5CiVSVndC5UZOk2MenyOiae0chkkzKoG3aWJHOfTFSWMMkM16sdpJbpM++NjtwDsAJwCe9XY7+zldkjuY2YAkgN6dfyp0d3bSFAk6MZE3rg/eX1HtUuUtbrcqyMqzszHLCyWUkMm0/anZwfN+XGCc/MckHJ9D06Uumae1nNZOlq8TNAVuGLAksNuN3PPQ4649q0LLUrS/LC3mVypYEA+hxmrLukSNI7BUUZJPQChzlsxJIVjhSQMnHArndO0+5hkdoYZIXlgYPJMBuWQ4xllOHPvjt17VswajZ3TbYLmKQkZG1gcj1Hr1pIdRsbiQRw3UUjnoqsCf8APB/KknKKasDszN0mwltrtZDFJGWU+dhFAZuOWO47jnPOPXpV7SVby7mXnZLcO8YIxgdP1IJ/Gpbe7jnEzq8ZjjfbuVs9ACc+nU0W+o2NyCbe6jkAXeSrZ49fpTnKUr3QJItEZFUrHK3N6jvvcTbs4xwVXH+H4UtjqdrqEe62mVzjJXPIp1tcySJMbmNIWhcq219wxgHOcDsamzV00PQmuN32eTbGJG2nCE43HHTNZdlbyebskS4Fv5LKy3O0lM4+UMOSMA55PQc1oW1/aXn/AB7XEcvG75Gzkev0phnE1xcWoh8zykBbJ+Uk5+X8v5imrq6sG5nWEBZmZUD/ANno0EDI4+c+ufXG0fXdTNK00w3Eim3YQyQkSGVArMxIyDg4bvk4/E1Y0i8icmFdO+wqY/MwAAC2SHHA6gj8cg0+w1cahcyLCsRgQsN/m/NkHH3cdM+9aSc9UkSkirYWDWmlPa21m1tdeQUMowBvAwOc575/wqAaZKttcrHbTKJIW3RoixhnyMHO7lh6/rW1bXsU1vLcF4vKRm+dXyNo7n0p0F9aXIYw3EcgUZJVs8ev0pe0mm3YLIz7HThaakJIbUxp+8QkEY2naV79M7vxJ9c1aaW5u7O7VIJLaVS8cZdhl/RgQTgH86niu7e5DC3lSRlGSAfXp+FNs7iW4t2aSFY5VdkKK+4ZBx1wP5VLcm7tDSSMptO8yK4itLNrWKW3dXRyAHkONpwCeRzlu+R1qxbwtcXU3nWMiRy26o7SYw5GeMA+/WrVpfeZZSXF0iW/ks4kw+5V2k5OcDjj0p739pGBmZSTEZVUHlkHUgU3KWqsCSKmi26WdtHAti9u6xKJGIGCwHTrz39qbqUz3Whal51s9uY0kVPMYfNgfKwIPHPTvUunajcXrOJLJoNiKW3NnDkZ29Owxk++O1WIHh1KxDSRKySAh4pAGwQcEHtwQR+FDbU+ZgtrIzrK0CSl4rB4IWhYTIXU+cxx6E5PB5OOtO0ixW1tN0lnIs/l7XLkMWHOFByeBWjZy2c0LLZvC8cLGMiIjCMOq8dCPSpyMDik5tgomLHbyrol5aLZSxkiXyk3L0JO0Ag8dalt9PjjkmgWzKQTwKXBIwz5Oc89eRk9/Wr1nc/aoSzJsZXZGXOeVOOv4VY2j0oc3qFjL0qKOztvLi06SFhGu/hfmYDoOef5VE0dxLo17btZyrI5lKDcuSWZiuCG4PIrZxRtHpRz63HYzrG1W1vJhDbtDA8aN1GC+W3Z56425PfHWl01Ssl9E6EP9oZiSOHDAEH8sD/gNaGB6UAAVLk2FijLYwW9lMtrbbGMIiAhIVtoBwATwMZOKzrOwmtra7jt4XRGC7AqiItgncAAcA478dfxrfowKam0rA0YotRDb3IsNOaAugUq2Nrc84UN1wTzxnjmm2Fm0Fre25sn+zvzEm1FDZHOFB4/HFbmBRtHpT9o9Rcpi2elwto7Q3ELwSyRKk0kjAszAdc5PQ9Km0dTcF9RkRVeRRGu3ptXv+JyR7YrRlhinjMcsayIeqsMg/hRFDFBGI4Y1jQdFUYA/ChzbT8wsVdWhuJ7B0tiQ5ZSQDgsoIyPxGR/hWXFp5TT7qD7FLLE6qEgULCoOTkqN3HYn6cZroaMClGbSsNq5hQ2V3Fb3SSxPLO7IXmRgvnqMZAGfl4BH9eaJLDFpPHp9lJbKxTKZChwGywC544PPTNbuB6UYFP2jvcXKctc2f2bSZV8qRYvPgMcYCxLnzAG2gNxkHHYfqatSaYJ9Ov7aGxMEMsIEUDFcF8HkAEgdV/Ktue2gukEdxDHKgOdrqGGfxp4RQAAMAdMU3Vdg5TOhht1spYU02RIj1jwo3568Z/nUCw3DaJBbtayhogiyRbwC6jGQCD/AIZ6Vs4FGBU87HYwXsiLWaKCyljtzJGY4VYKRhssQMjbx2yOQfWrlpYQxGe2+yBLYOrRqcbCeDkDPHIz9a0to9KMChzbVgsVLlILTT7jbCCm12ZFH3yck8dySf1qHMun+HlMsbzywWwBRD8zsFxgfU1o4BowKm4WK2nQfZdOt4NhTZGAVMhkKn03Hk/Wp5XWONncgKoJJPYU7FGM0m7u41oU9KV00q1V2JPlL1GMcdPwq5Riih6u4C0UUUAFFFFAHHX63Sa/cxwx3K3VxdW7wSorbDEoAcMemB8/B/vCuvB4rGll8QTyutra2dpGrFRJcOZGYeoVcDH1NN0+61SPXn06+uLe5H2bzt0MJj2HdtAOWOc8/lUrQ7Kic4LbRer6G3nNchc6bbaXfztqP2pLSeRpIbyG4dFhZjkq4BwOScNjHrXU3UU89syW9x9nlONsgQNj8DWVM3iCwgklm+wahFGhZgA0LsAP+BD+VdVFtXs9+n/BPPnqP8O3sl3b3UT3IuvstwYlnGP3i7QwPHGcNj8Kh0rStVstUurieSweK6l811jjYOvyhQASfYfrWppv2Z9PhmtIEhinQShVUD7wz271St7+7k1EQvJAFLsphaNkdVAOCGJw/QdB39qTk7y5VZMdtFcr22ma1Br02otNp/lzqsbokbg7VLEEHPX5qqWvhnUbdLENcWYa2vnumZI2BYNu469fmP5CtxdUDKv+izhmuDBsO3IP97r0wM/SmRazDPqJslhk3BmUtuXgjOcrncBx1I549aftKgWiYFl4T1W21e11CS+gle3lZndzIxlDAg8FtqnB7CtKz03WoNdn1CaexaO4VEkREcEKu7GCT1+ar1hqM91NLHJYyxKkjJ5hKbePo2f0qOHxBaT3AhjBIfIjYOh3nGcAbsjp3ApyqVJXvbYEooqWun61b6zcahcT2TRToqyJHG+7au7GOevzVneHtP8AP8QXMxt7qKxtWL2UNxA0YVpPvkZHY5x6ZNbtvrazyRKbG5jWQKd77MAN90nDdyMVp570nVlFNNbqwcqYtU4IWi1S5by2CTBG35yCwBB78cAe1Mh1RZpUH2aZYpf9VM23a/GfXI4HcCnQ6mk32fEEqi4LAFtvysM5B59j09Kys0VdF2siz066ju45rhbYOgPmSwghpjjHzLjA9e9WNPv57tnEljLCA7qHYrg4YjsxOeKuuxVSQpYgZAHelrBtBuZWnx+bqM7r5q28TExJJEyDc3LEZHPP82pthplzb3glcQxqAdwidiJCf9g8L68VPa6ulyYWNpcQx3H+qeQLhjjOMA5HQ9Rj9KfbambqdolsrhQjlHdtoCkfjzn2z1rRuepOglrb3cMjwnyfszO7hwx3ncScY6DGeuao2uiT2rooKsIFIid7iVs/KQPkJwOvv9BWna3DyyXIdJFMb4VGC9MDoQeQevPrUdpqf2pkH2SeJZELI0m3DY6jgkileSvYdkV4tMuke3YtDmExkgZ52oynt75FXY1u2nuBO0P2dgBFsBDjjncTx16YqLT7+a83eZYywAM43sVwcMRjhic8VLbySedcI53+W428AHBAOP1pScm3cFYq21jdI9tHMYRFaf6to87n+UqMjtwffPtTbOzvreW2VzB5FurIME7mB6H0B4HHP1qe01QXciL9knhWVSyPIFw2Oo4JIqQXEkmpSW6gCOKJWY9yzE4/IKfzFNuSumFkMtI7yGZo2EBt97uGDEudzE4xjAxn1NSA3KPdNP5ZhGDCIlYvjHOfU56Yqray6nDMW1DyvIVH3Ooxgq3DdehU9OxX3os9dtr2byo0YFgTH86Hf+AY4/HFJp7hoQaXZ3MltYtMUVLVMxjymjcttK/MD0HJ6das6bb3tt5wnS2Ad2kBjY5LE554/WnWurpcgO1tNBG0ZlR5duGUYz0JI6jrUcepTyajbQm2mgSVXP71R82AMHgnH0NN8zurBoh9pFqUc9w8qWuJTuAV2JB2gAcjpxTbSyuoGst/k4gtzE+0nknbyOP9n9a0ZJEhiaSRgqIpZiegAqpb6j50oR7WeDeMxmTbh/yJwfY4qeZtMLJDbKK9t8wsIPJQHYwY7m54yMcfrTbaPUke4aVLUeady7HY4baAOo6cUzTbu9vJ5GlgeCJXdQGCYODjqGJz39Ku3lytlZzXLozpChdgmCSAMnGacm07dwVrFO0sbmCezZ/J2wWzRPtJ5JK9OOny/rU1tBJDqN22391PtkD5/ixtI/JQfxqO11dbmcwtaTwlSQTJtwGABxwT2INLYavDfzSQpGUeNd2N6NkdP4WOPxoalrcE0X2B2nbjPbNZ+nwX9vFKk625yzuhjdurMWwcjpzT7e6kNvcyyRS7onb90QoYAAEAYOD19e9NtdTF2dv2WaJni82MSbf3i8ehOOo6460rOzHoQwWuorDdxyi2Hn7mUq7HBIxg8dKd9ivRGiI8UeLUxblJyH4wRx0p2nf2qzk6gYVURKMRjq55bHPQDAHrgmptMvGu7PdIB5kbvFJgYBZWKkj64zTbkri0Ken6deWlzLOREPMjChDNJIQwJIOW7HPoPxqexi1CATCdbb52Z02Ox+YnODkdKtWt19q839xNF5chT96u3djuPUe9T4pSk76jSRm2EV3ax3H2xYfLZnk/dFmPJyRjFM0aElZJnMmFYxQiWMoyxgnAwefx7jFauKKTm7MLDW+UZxn2qpplu9tp+JF2ySO8rLn7pdixGfbOPwq7RST0sBT0mC5gsVF4yNcOS8mxQoBJzjjrjpnvirh6dKKWhu7uBR0yB4opXkjaN5p3kKsckAnjocDjFXqSlobu7ggooopDCiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAoatqKaZpz3JQyOMLHGOsjnhVH1JFQ6NpkllHJc3b+dfXRDTydvZR6KKu3FpDdeV58YfynEiZ7MOhqccCl1NOe0OVddwFZ+u/aX0qWCyhMs9wDEvPCbgRuPsOtaFUozs1eVB5hEkKt1JVSCR+Gfbriri7O/Yya0J7S3FrZQ2y5KxRqgP0GKrQaYIWi3XM8qQHMayEHBwR1xk8E9TWhRSu9QsZdtaTvq813PbiJdgWPEm7J7sR2OMD8KkXSlE8UslzPKIXLxq5U7SQR1xk8E960KKbmwsU47HyrhpEuJlR33tENu0n64z+tNi04wECO5nWNfuxfLtX26ZwPTNXqKOZhZGfHpSRqi+dMfLWNQTt/gOR298VPHalLya4M8zCVVHlMfkTHcD371ZopOTYWKEOmJFJGfOmaOI5iiYjanb0ycA8ZNNj0pYp45BczlYpGdI8rtG7OR0yeprRop88gsinFZNFMXW5mEZYv5Xy7cnk9s9TnrTltnhuJ7hZpZTKBtiZvkTA/h9M96tUUrtjsZGl6XJFbW/2oyhoOViMgdVOMZBxk9Twc4q3a2TWzu32qaQOxYq4TGT9FFXKKbm3cSVilDYPDNJL9suHMn3gwTHTHZRRDYeV9nH2iZhApUbtvzA+vHb2xV2ihyYWKcVk0UxZbibyyzN5Xy7ckkntnqSetENi8M7y/bJ3MnUMExnGM8KKuUUczCxSh04Qm2/0iZvs4IG7b8wPrgfyxThasmoPdK3EkQRlx3BOD/wCPH9Kt0UnJsYx0V0KMMqwwQe4qrBp7W+At3OyIu1FbbgD64yfxzV2ihNoChHpiJHAjTSukMRi2tt+ZTjrx7Dpikj0vZcQztd3MrQAhA7KRgjkHjnoOTzWhRT5pCsMkjWWJo5FDI4Ksp6EGqsGniKRXe4mm8tdsYkIIQfgOT7nP6mrtFJNoZUs7I2hf/SppQ5LbZAuASck8KO9SXdst3aTWzsypKhRivXBGDU9FDbbuBnPpEUm/fLKRISW5HOU2Ht6c/WnQ6b5Nx9oN3O7+X5fzbMAewC1foqueQrIpRae0Ym/0y4fzs7twTg4AyML6CiHT1hmhlEsrGGLygGxgjjk8deBV2ilzMLIaQccdarWFp9jtRHkM5ZndhwCzEsT+Zq3RU+Qypptm1jZrA80k7glnkkOSzE5P0HPA7CrdFFNu7uAUUUUgCiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKAG7u1KOlZOr6bZSK99cXlzZmNOZY7lowAPUZx+lGgzXN94bt5LmaQTSxn97gB8ZO1umM4welK+tjV017PnT8jWqGOAJdSzl2ZpFVcHGFAz0/M1y2uTyaMqx/2vqsk8gGwnYIlycZZ/LwB+tT6PdXUtpbu+oT3V353lvhP3boGILDAxjbznPXj2rpdBqHOno/U5udXsdRkU2OWOZA8bq6HoynINYwu3Se1gNzM0ounSRcZ+T5sFuOBjbg8dahtJn3q0NzM87XTDyGGF8syHJxjpt5Dd/0qPZOxVzdS4hld445Ud4zh1VgSv19KcJUMjRhgXUAsueQD0/kaow3ETazOA45ijUe5BfIptvNGNVuYxcM+5EKhuxy2QOPpU8m47mlmisa1mMlyjyX063JkIe3AyoHPGMcD/a7+tbDAkEZxUyjyuwJ3FzRmsW3W7N4lo1xcn7M7PJIwGJVP3F6c9e390+tJZzytNbl7mZrmRiLiAjKpwc8Y+UA9D3981fs/MLmws0byNGrqXTBZQeRnpQ00aSLGzqHfO1SeWx1xWdZzgardxidpFZUKbh3+bIBx0GBVGOUyXunO91O8zSkzxsvyxny2HTHy8nA9ffrQqeoNnRUxpo1dUZ1DvnapPLY64FKxYIdoy2OB71z8MzNc6e7XM8k7OTNE6/KjeWwx0+Xk4Hr79aUIc1wbsdDuGKQSo3CsGx6GsW1nd5oM3Es0koIu4ZBhYxtOeMfLyAPcHv1qpo1p9mmtJvKgihYMgaCEoxbniQ+mOnuB7VXs7LUVzpVlR2ZVcFkOGAPQ4zz+BFOyKzbGdPtd1GJ2ky4KbvTAzjjpVTT7i5bUV33LTJKGJAY5Ufw7kK/L6dfzpezeo2zbjljmQPG6up6MpyKdmsOxeb7diaWSOJ3l8lV+6/ztktxweRjt/SW1Ny12lo08xNozNLIcfvVP3AePT06bfehwt1Fc1TIoYISMkEgZ7UCVGYqGBI6gHpWfHk67cmQDK28flE9cEtux+IXP0FZ2lxQreQmFIpCUYBxCY5olI/5ac8knHYHPOOtHIFzos0ZFZGk+Vbu8TXc7ymSUGOQ5wN7HPTjI5z3zSaSZJZZHlv5pCksgWNsAbNxAzxz9fp+KcNwua0c0UrOsbqzRttcA52nAOD+BB/Gn5FZGnTgz6hE1w7gS5jZsZ2+WuSDjnBz+VV7Ca9W2tpPtEs9xcWbOyy4x5gC4HQY6n8qfs2FzfzRWBZXDtrdrCl5dSRvbySSJKuPnBQDsMdTwOnFbzruUrkjIxkdRUyjyjTuKCD0ozWFp5a1sJIoLiWa8WNwIZDkKwzjOBx+PWm6ZdXf2gGScSI0RZ18xpGDcdtg2nrx+lW6b18hXN/NJkdetYWlS3Mt00Ul08qvCSXV84bjkgqNjcnC5Pf0qXQFjhto4DczSTKmHjc58sjt04/Gk6drhc2EdXUMpBUjIIOc0tZuhljZyjnyxczCLP90OcY9vT2xV+ZGkidFkaNmUgOuMr7jNQ1Z2GhJLiGKIzSSoka9XZgAPxp6OroHRgysMgg8EVwGnSRW/h250+6n1C4uDBOjWj2xZI2yxByE7/U9ataHeXNmYLOa8v3t5NMEjO1scwSDjC/J6Z4Oeg9a6ZYaydmSpnbUZFcRpN7rEui3V4l9e3OoQwvttZrbYvU7SPlG5sDPB5zinxXWpXS3EGl6pf3ANm8jTT24QxTDG1RlR15yuDil9XabV1p6hzo7TNGa4XStV8R3txJLdLdWkVvYvKoMQYS5GEJGMl/vEgY6DgVZ8J6jqVzqskNzcXVxEINzM4ygfcPVFKnH8PNE8NKKbbWgKaZ2JNNWVHzsYNjg4NRXpVbKYtv2+W2fLGWxjsO5rEs0Nqtw1oltLMtudsttCU6fdVlyQT+XToKwUbopux0WaM1ipcrEkstve3N1iFmMZGcNxznHyn/Z/TimaXdSvPdwS3BaJYldJBIXGTu3YYqOny8DOKr2bs2F0buaQsFGTwPWsfTY5rrTyzajO07x7ScAeWexxjqP1qrdGTUNKvmm8wxw2zwNFIuVeUDk4xzg4we+aPZ62uK50KyI33WDfQ07Nc7aR21rBOT5cU5hYtPZQbNq5GBjn5sn3qS1ub0RXRuJZPtCwgpGFyoX++OuWPJI+g9y3TDmN7NGaw5J5IrW4bT7ye6cRg4YbgvPJBCnnGflwenSqzXV5Hp16y3e4RxB0aKQzMrZ5GSoH/Aef1oVJvqHMdLkYpM5rEG+eG6hgubqaJrcku64IY9ApIHJGcjtx0zU+mvAmnlBeyvtiG9mOTHxjGccH260nCyHc0opo5k3xOrrkjKnI44NPzWNBcuuit5UrmWNyGYJlwm8/NjHJ289PzqJ5pVgu1tr2d4VjVkmOGKvk5AbHPbjt+PB7N3sK5vZo6Vn2BeO8uLczyTIqo6tIcnJznn04HHvV9s44qGrOw7iJIkmdjBgDg4OefSn1Q0cEaXDuADnJYDpnJz+tX6GrOwIKKKKQwooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKAMO98Q6GRNZXkoZslHgeFiWI7Bcc9O1L4Zglt9KYPC1vG80jwwsMGNCxKjHb6dq1z1ycU7IpW1NXUjycsV+P8AwDGu7XWr95bd57W0s3JBkh3NMU9OQApI781f03S7XSrUWtoHWFfuqzs2Ppk8Vapa0c248vQw5Ve4mMc1UXUbV7hYA7b3YqpMbBWIzkBsYOMH8quHoaxbOO8+2RbrWe3ClmlzKrxNkH7vJYHJ9AOtKMU1qNmwCOufajIz71iQW1vLqb2cQt3toJftRC4JWQ54x9ctn6CorXT7hdaW4NlKgEru7ymIqMg/dZfnJOeh4HPoKrkXcVzdjmjl3bGB2sVb2IqQMDxkVj2VmtnqEoTSgC8rMLpFjACn8d2e2MVSs9MuYLxPNguJHjLF5gIQsuQc8/eOfQ9+/GaOSLvqF2dJkE9RTsVzdnpb24t5F0rypI0hzgx5BDEPyG9CD7ituOa4e8mha2ZIUVSk28EOT1GOox70pRS2YJ3JwQeh5o468Vi2dlItzArWBiliJM12SmJuDnGDuOSQcEDGPpTbW3uYri0i/s1gttK4M+5MbGDYxznHIyMD8afIu4XNqOZJVJRgwBIOPUHBp5AxWTYWq2V68aaSEJdz9qURhdpJIHB3egxirgllkuLmGe12W6KNsrOCsoI547Y96mUVfQaLIIzgEZoyPUZrndGti8VjJb2UcIhAZ7lHVhKCpG3g56kZB4GO+BVnSrULdzPLo727mRnSWQxsAPQbWJHc9O5qnBK+ok7msku95F2Muw4yRw3GePz/AEp+Qeh5rJsGnS5uQ2jT28Uzb8locE45yFc8kj/Go9OszbGxK6U8DGN1nbMeV/3sMc5I4xnHtScV3C5rxyJMhZHDDJXj1Bwf1qnpkVvFJc+StwrbwJPPdmJOByMk9sVDp9sLK7eJNJ8v53P2lRGFKliwAwd3cDGO1Otbi6e7uPN0m5iSTkM7xEcKBjhyecUWSukwNHZG0okwpcAgNjkA9efwH5U37RGLn7PnMmzftA6DOP8AP0NZGmWbWzWLLpT277HWZt0eV/3sNzkjjGce1Xo0aPW5yyHbNAm18cfKWBH/AI8D+NDiu47hZ6va3s/kxGQPsLYdCvRtrDnuD1HbI9auhgehFR/Z4kYyLCnmDJBAAOT1598CsTSdOmi1HzXspIlCMrGbyj1I4Upyw46sM/rRaLu1oK7NyKaOZN8bBhkjI9jj+lP4Pf8A+tWPplq1i0sEWlLE4L4uMIEcFiQODu9OoFV9Jtrq2vhK1hPHE0TK4YQLhuCMBDyOoGSfw603BXdmFzXgsreC5e4Qu0rgjLyM2ATkgZPA6dPQVPFPHOgeJgynoRWNolkI/NFxo7WzmSRleTy2G1mJCjaxxwenTrUujWv2FmtxpXkEFg1wojCyDPGMHcfxApNLXUEzXxikyD0OaJDiNjtL8fdHf2rE0S0+zrI0ujSW0wZ2V3MZJBYkKpVjjgjjgVKStcZsRSeZv+Rl2tt+Ydfce1OYgKSBnA6DqaydL+0Rm7jOky2kcjGSPc8YX7qjHyMcEkE1DotjLZzuws5o0WIqPNEW5jxgKUPI4PLe3vVcq11Fc2LOWGS0ieFdkbICi4xgY44qYuAM5GMZrB02yktpB9tsi4lgAeeQp+5GOYzz09wMevrUmk20U8hc+VJFZhraFk2kMvc8e2F+ob1puK11BNlux1e11F9tv5jZiEuShA2kkD88Z+nNWoJY7mBZoySrjIyMEexFOWGOLJSNU3YztGM4GP5VS0aF4rBmcECWaWVQRyFZyw4+hFS0nqhrzNAYPSjbWfoUJjsnme0Fo9zK0zRhiTyeCc9CRjI7VpUmrOwIbtFLilpKQwxRtoooAMUYoooAbJEJY2jJYBhglSVP5jpUNpZQ2MHkwb9m4t87ljknJ5Jz1qxRRfSwWDFG2iigAxUN3ZxXtu1vNu2PjO1ip656jmpqKE7O6AbHGI41QFiFGBuJJ/M9adiiigAxSbfelooAMUYpaKAI44Y4gRGiqCSxCjHJ6mpKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKAOVGoQ393He6tfQ2FnCwe3tJZVR3I6PJz+IXt356JJ4ut31+KKzF1d262zs621sz5bcoB6dAM89Oa3bfRtMtObfTraI+qRKD/KnJp8UWpS34LGWSNY8E8KoJPH4mpszs9rRu/de2n9frcls5muLZZnhkgLc+XKAGX64Jqeo4pY5Q3lur7WKttOcEdqkqjjdnsIelVYLoXFzPEpGIiB0IOffI6e4q0elUobW5jv5Lh54mSRQpQREEAZxzuPr6U1bqJlaLU431aSztrYDYQJHZWXJ5zj5cH8TWqBVOC2njvZp2niZJSPkERBGBgc7v6VdHSnOzegIrSXIW+jtVTcxQyMc/dAOB+ZP6GqsGo3T3ot5rBo08x0MgbcAQAVPToy557EYqd7V11hLtBlXh8qTnpg5U/q36VbIAHNGiDUqJqdo0ccglOJZDEp2MMsM5HT2P5UsOpWk9x5EcpLfwnYwVv91iMN+BNU7SP7RqlxJsmWBOUSWIqN54Zhn2H6t60WWiCzeEBo2SA/ISrb8YIHO7GeeuPwFU4wSFdluPU7SW5NtHI3mAkDMbBSR1AYjBx7GoLXUbm6vREbB44iXPmOSMKp2qcY6sckD0HvSW+lPFeLcGWIEElzFGUMmc/eGce+cdfStPHek+Vbaj1DiqkGo2l1M0MchZucZRgr+u1iMN+Gaesdwbifzpke3cARxqmGT1yc85+gqjZ6ILRolJiZIgVU7W3kYI/vYBweoH5UJRs7sG2Tpq2nCVYUcgscIBE2H4z8pxhh7jNTRX9tM8Qjkz5yb4/lI3D64/Ss8wXFre6dCztNDExA2W5GBtKgs2SPT0qaHTbmKS3zdR+VBv2gRfMcggHOe2fSqcYb3Emy1BqFtcXD28bv5idQ8bLn1IJGG/DNFrcSzTXEUsaq0LgAqxIYEZHYetUbLR5bW8guGuI28qJo2Pltukzj5iSx54q1bWlzDdzSyXETrMQSqxFSMAAc7j6Umoq9mCb6joNStLm4aCOQswzyY2CtjrhiMH8DTvtinUGtFBJjiEkh/ugkhR75w35VVtNKkt7pJ2kiBUEP5MZQSZ7kZI96nS1eLWZbsYMc8Co3+yylsfmGP5e9JqPQNRun6tbalkRCQFWYfPGy9DjqRipLfUrW6mMUUhLDkZRlDj1UkYYe4zUdvYzwb4TLG1u7yMRsO47iTjOeMZ9Kgs9H+yyRNuibyQQrbG3HjGeWwD+H5U7Q1DUtQarZ3MrRxSMzAFh+7YBgOpUkYYcjpnrTNO1a21JD5KyKQWyHiZejEdSMdqistKe1uY5mljyqFW8qMoJCcckZwOnYd6ms7W4tCYzLG0O93A2HcdzE4znHGfShqHQFcls7kXUcmVCvHI0brnOCP8Rg/jRZ3Qu0kO3a0cjRuuc4IP8Ahg/jUenWrW4uJZFCyXM5lYA5xwFH/jqil022e3Fw8mN9xM0pAOQOgH6AVLUdRq5cPSqttdfaLm6iCbRbyCPdn7x2q3/swq0elUrG3e2ub3KYSWbzEIPXKqD+oP50lbUC3I6xxtI5wqgkn0FYNl4ts9UsZ5bEB7mISMIJGK5CkjO7B64B/Gt8jiueg0HU7W3ns4dThS0kaZlU2pZv3hJwTuwQC3YCtKfI0+bcTv0LOkeJdO1a2WSOdFmEAmlj5+QY5wcDcAeMipLXxNot7MIbbUInfazdwMDryeM98dcc1StPDt9ZzWUkepQ5s7NrVQbU/NnGG+//ALK8fX1osPDU8Gl3emXd9FPb3KyDMdt5bhnJJOdxz19K0lGhdtP+vuEnItJ4n0SWGdxfxGOFdzkgj5em4ZHK+4yKng1fSvtEFrBcxeZcrviRR94etZy+Gri5lVtUvorhYraS3jWK38vKuACW+Y5OB0GBUXh3wamg35vTfy3TmEo3mL/GSCzDk4yFUY9qHGhyv3nf+vILyOkmlSCJpZDhEBZjjOAKrW+p2l0sjRy/JGNzFlKjb6gkcj3HFT3MZmtpIlYKXQqGIzjI9KpSaY08HkyTKUNsYG2pg5OORk+3T9awjytalO/QkXV7Iwyy+ayrENzb4nU49QCMke44qcXkJuEgDnzHQuo2noOvPTvVGDRwnmeb5JDwtESqtkg4zyWOBx0/Wl0vSG0+d5WuDMzoN3y4y5++3XjOBx2xVNQ6MV2aU0ghheVgcIpY4GTxVGz1KS4bMtuIoTH5iyrKHXHHBPY857j3q7OkklvIkUnlSMpCvjO09jjvWYNG3tMZnjQTQtEwt49m/djLHk5PHH1NSuW2o3ctW+qWl1I0ccjblBOHjZcgY5GQMjkcinW+o29yshjZ8xDLK0TKceuCASOOoqI217NDJHLcxLujKK0UZBBPfO7j6D86istLltLqWZZIV8yMIEWM8EE8kluetO0bPUV2TR6xYzK7xzFlRN7MI2wB35x1Hp1oudVhhhLRAyyeSZlTBXco68kcUWkEmn2RSZ1lVBx5URBPrxk5qnZWbXGn3SktGZQ0MXnREGOMZABGRnqT+XpTtC7fQNS1FqT7JZLmFY4olLNJHJ5g46g4FTJqVq7OomHyRCViQQAh6Ek8dqrw6fcWyuIJ7eEFWwsduQoc4+YjdzjHt1qOLRTFbT2yTgQTpyNnzCTu2c9P9nGOOOKGoO4lcsw6tZTCTbKV8tdzCVGjIX1+YDj36Ui6xZG3knMrIkX398TKVHqQRnHv0plxYXF9byQXc0e1lAHlxkEEEEHk+o6VVn09rewum2qzyQmNfIiZm578k/y/OhKD6jdy6urWjwyyo7kRDLKYmDY9QCMke44p9rqMN5bGeLzNqgFt0TKemehHP4ZqG3tJZZBdXEoZzCY0CxFNobBOQSeeB9MVLbw3kUJjkmhO1AqERnr6n5v0/Wk1HoCbH296ktkbp3VYwWO7kAAEjnOCDxz71Gur2RtpLgyskcIzJ5kbIVHqQQDj3xiov7Omayltpp0bdIZEZIyNrb94yNxyM4ptxp1xdw3AluIxJNF5SlYztUHqcZ5P8qdoX1Yaly1voLxWMLMdhwQyFT+RA496ZFeNcLdNDGW8l2jXJxvYDn6c8fhTo4JFvZJ2kUq8aIFC4IwSc5z71FawTWcd2ioHzK8sQzjdu+bB9PmJH5UrR1sO7LFrcpdWsVymQkqBxkYOCKLS7gvoFuLaVZYmyA69Dg4P61BbwTWejpbxbXnjhwCThWfH8s1LYxTQWkUVxL50yoA8gULubucCk7a2BXLDZCnAyccVDaTm4tklK7Sw5AOcH61MThScZ46VU06A21msbIEYkuwznliSf50tLB1LlFFFIYUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAUUUUAFFFFABXP6nqWpjxDFY6dbGVVgLyF/ljDMcLubGeADwOTkV0FNIq4SUXdq4mrnKaOdehbUXhFlPtvX82HDIWOFJ2tkgde4/GuntZXmt45JIXgdlBaNyMqfQ44rL0s+T4g1i2zhWaKdV/3l2k/mlbIx2q60uaW3b8iIKyA9KyYb25a+jhkkjTc7gxtCykqM42tnBPAJ9vStY9Ko2+lRW0iFZp3SLPlxu+VXt9T1PUms4tJO5buNGpsdo+ySBzcGApuGR33demOfpUcespLqP2IRMr+YycsoIwD820nODjgjPUU+3spf7VmvJ4YkygSMpIWPXkkYABPH5U+PS40nSQzTyCNi8aO+VVjnn17nvVe4LUZYX11czTLLZmNEkZBIHBHH41Bb+IrW5nSKLa3mkiMrKpJxyMgHIB//AF4q4mnpHdNMk0yqzb2iDfIW9emfwzikj0xIpAyXFwEGdsQf5Vz6d/wzgUXh2DUr22svO8e+wliWQIdzMp2h87eh9q1CQBVGPSIYkRBJMQiooJbnCEle3uanjtFju5bkSzFpVVSjOSi49B296UuRv3Rq/Urw6mZmiY2rrDOSIpSwOeMjI6gEDj9cUsOped9m/wBHdRcFlyWHysueD/3yadBpcUEquJJmSPJjiZspGcY4H0Pfp2pkekQx3CTLNPiJ2eOMv8qk5zx+J60/cDUXT7y5ut3nWZiUO6ht4I4Yj19quuSEJA3EdB61WjsFjuTKs84UsW8rd8mT1Pr39cU5bXyrie4SSV3mA+R5DsXA7D+HPfFS7N6Arla21Y3At3ks5IY7k4RnZTzjPIB4zg4/pT7bUZrmd4xYyosblHdmXAI9Oee351DpmkG3hhNzkyQjCIJmdFOMEjIHqfp2qzaaeLOV3W5uJA5JKyMCMnv0qpcmthK4Ws0kk10HV1KSAKrFcAbRjGPXrz61HaajJdGLfZyQrMhZCzKemOCAe+eP6U6DTBBM8ou7ly/3g7gg8Yz0p0OnJCLcCeZhbghdz9QfXjml7o9RmnXlzdBzNaGIB3XdvBHDEY4PtTrPzUmuo5J3n2yDYXCggEA44Ap0dgsVwZVnnCli3lbvkBOST69SeppsGm+RM0ou7ly/3g7gg8Yz0obi27C1GWepPdGLfZyQLMpZGdlPT1wfy/pUiTySapLACBFDEpPHJZif5Bf1pIdNjg+z4mmb7MCF3PnOfXjmpRabb9rpWxviCOuOuDlT+rfmPSh8vQauUrX+07WZpL+dZLdI3DNgDG1sq/HqpwR2K8daSy16C+mWKNVzIpZMSqx47EA8HH4VquiuhRlBVhgg9CKpwacIG+W5uCoUqiM+Qg9uMn8c0Xi73QrPoRWurGdEkmtZLeOSEyqzsDwMZyAeOuaYt7dSapaI8EsEUsbko20g4xjOOQ3tnHNTxaXDEsC+ZKywRmMB2yGU+vHPSmx6TFHcRXBuLl2hyIw8mQFPUe/brzx1qrw1sGpf7VRs9Rlu2P8AoMsaKzIzsy43KSDjnkZHWrzDcpGSCR1Haqlppy2YcLcXEgbJxIwOCSSSOOuSazVraj1EsJ3lN15okDRzbdj4O0bVOBjqOc888moLDWE1GVoUjaJthY/Ou5OcYZeoP4EVNb6WltJM4ubiTzvvh3yCcAZ6dcAUQaXHDIJDNPKyoY0MjAlFOM449hyc9Kr3NRalbSdTku7faEe4MKYkmyoDOP4ccc4x2xzU8OptceQI7V900RkILD93js3vnj8D6U6LS47Z0lgaTfHHs2l+JO43ccnJ60mmWUlvJczXEcaSzybsRuWAXsOQO5J+pNNuDu0gVyPT4tUWXdfzoy+UOEA5ckk/gOAPXkmrGmzyXFqTNjzI5HjYjoSrEZ/HGat4qtZWn2S28rfuYszs5H3mYkk/maltNO+47C2ly9wZg9tLD5chRTJj94B/EME8H3qxVTTNPTTbQQIzOSzO8jdXdjlifqTVuk7X0BC0UUUhhSUtFACUUtFACUUtFABRRRQAUUUUAJS0UUAJRS0UAJRS0UAJS0UUAFJS0UAFFFFABRRRQAUUUUAFFFFABRSUwzRrKsTOodwSqk8nHWgCSiiigAooooAKKKKACiiigApMUtRrPE8rxI6s8ZAcA8rnkZoAdtG4nHJ71UjJXV5VCsQ8KsTngEFv1P8AT6VcqNIESd5hne6hSSewzjj8TTQiSjFLRSGJRS0UAJRilooASloooAKSlooASilooAKTFLRQAlFLRQAlFLRQAlLRRQAUlLRQAlFLRQAlGKWigBKKWigBKWiigAooooASloooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooASk2jOT1FOooASloooAKKKKACiiigAooooAKox7jrc5BXYLeMH1zufH9f0q9UawxpI7oiqznLEDluMc007XAfS0UUgCiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiikoAWmkgDJpabL9w0IUnZXE81fX9KPNX1/Sq+cVn6br2m6td3lrZXQlmspPLnXaRtPI79RkHkelXyo5fbSNjzV9f0o81fX9Kgop8qD28ifzV9f0o81fX9KgopcqD28ifzV9f0o81fX9Kgoo5UHt5E/mr6/pR5q+v6VBR0o5UHt5E/mr6/pR5q+v6VnHUbYaqNM8w/ajAZ9m0/c3bc56de1WqOVB7aRP5q+v6Ueavr+lQUU+VB7eRP5q+v6Ueavr+lQUUcqD28ifzV9f0o81fX9KgopcqD28ifzV9f0o81fX9Kgoo5UHt5E/mr6/pR5q+v6VBRRyoPbyJ/NX1/SjzV9f0qCijlQe3kT+avr+lHmr6/pUF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