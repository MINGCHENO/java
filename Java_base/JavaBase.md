### Java 8 / Java 7 为我们提供了什么新功能
#### 所有解答来自google
[java8新特性详情见连接](https://www.jianshu.com/p/5b800057f2d8)
1. Lambda表达式和函数式接口
Lambda表达式（也称为闭包）是Java 8中最大和最令人期待的语言改变。它允许我们将函数当成参数传递给某个方法，或者把代码本身当作数据处理. 
Lambda的设计者们为了让现有的功能与Lambda表达式良好兼容，考虑了很多方法，于是产生了函数接口这个概念。函数接口指的是只有一个函数的接口，
这样的接口可以隐式转换为Lambda表达式。java.lang.Runnable和java.util.concurrent.Callable是函数式接口的最佳例子。在实践中，
函数式接口非常脆弱：只要某个开发者在该接口中添加一个函数，则该接口就不再是函数式接口进而导致编译失败。为了克服这种代码层面的脆弱性，
并显式说明某个接口是函数式接口，Java 8 提供了一个特殊的注解@FunctionalInterface（Java 库中的所有相关接口都已经带有这个注解了）.

2. 接口的默认方法和静态方法

3. 方法引用
方法引用使得开发者可以直接引用现存的方法、Java类的构造方法或者实例对象

4. 重复注解
允许在同一个地方多次使用同一个注解

5. 更好的类型推断
在很多场景下编译器可以推导出某个参数的数据类型，从而使得代码更为简洁

6. 拓宽注解的应用场景
7. Streams
8. Date/Time API(JSR 310)
9. Nashorn JavaScript引擎
10. 对Base64编码的支持

### 请简述一下 Ajax 的原理及实现步骤
AJAX即“Asynchronous Javascript And XML”（异步 JavaScript 和 XML），是指一种创建交互式网页应用的网页开发技术。
通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新.

get 请求
1. 创建一个XMLHttpRequest对象
2. 调用该对象的open方法
3. 如果是get请求，设置回调函数onreadystatechange = callback
4. Send

post 请求
1. 创建一个XMLHttpRequest对象
2. 调用该对象的open方法
3. 调用setRequestHeader(“Content-Type”, “application/x-www-form-urlencoded”);
4. 设置回调函数onreadystatechange = callback
5. Send

### 请简述 Servlet 的生命周期及其相关的方法
init()方法   service()方法  destroy()方法
Servlet的生命周期是由Servlet容器来控制的，它始于装入Web服务器的内存时，并在终止或重新装入Servlet时结束。这项操作一般是动态执行的,并实现javax.servlet.Servlet接口.
![servlet生命周期见图](https://img-blog.csdn.net/20130825201025734?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvaGFwcHlsZWU2Njg4/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
1. 加载和实例化Servlet
当启动Servlet容器时，容器首先查找一个配置文件web.xml，这个文件中记录了可以提供服务的Servlet。每个Servlet被指定一个Servlet名，也就是这个Servlet实际对应的Java的完整class文件名。Servlet容器会为每个自动装入选项的Servlet创建一个实例。所以，每个Servlet类必须有一个公共的无参数的构造器。
2. 初始化
Servlet被实例化后，Servlet容器将调用每个Servlet的init方法来实例化每个实例，执行完init方法之后，Servlet处于“已初始化”状态.Servlet在启动后不立即初始化，而是收到请求后进行。在web.xml文件中用<load-on-statup> ...... </load-on-statup>对Servlet进行预先初始化。当客户端第一次访问服务器时加载Servlet实现类，创建对象并执行初始化方法。
3. 请求处理
服务器创建特定于请求的一个“请求”对象和一个“响应”对象。调用service方法，这个方法可以调用其他方法来处理请求。Servlet对象的生命周期中service方法可能被多次调用.
4. 卸载servlet
当服务器不再需要Servlet实例或重新装入时，会调用destroy方法释放掉所有在init方法申请的资源.
一个Servlet实例一旦终止，就不允许再次被调用，只能等待被卸载。
Servlet一旦终止，Servlet实例即可被垃圾回收，处于“卸载”状态，如果Servlet容器被关闭，Servlet也会被卸载，一个Servlet实例只能初始化一次，但可以创建多个相同的Servlet实例。如相同的Servlet可以在根据不同的配置参数连接不同的数据库时创建多个实例。

### volatile 修饰符的有过什么实践
对一个共享变量使用Volatile关键字保证了线程间对该数据的可见性，即不会读到脏数据.

Java 中可以创建 volatile 类型数组，不过只是一个指向数组的引用，而不是整个数组。如果改变引用指向的数组，将会受到 volatile 的保护，但是如果多个线程同时改变数组的元素，volatile 标示符就不能起到之前的保护作用.

一个典型的例子是在类中有一个 long 类型的成员变量。如果你知道该成员变量会被多个线程访问，如计数器、价格等，你最好是将其设置为 volatile。为什么？因为 Java 中读取 long 类型变量不是原子的，需要分成两步，如果一个线程正在修改该 long 变量的值，另一个线程可能只能看到该值的一半（前 32 位）。但是对一个 volatile 型的 long 或 double 变量的读写是原子。

一种实践是用 volatile 修饰 long 和 double 变量，使其能按原子类型来读写。double 和 long 都是64位宽，因此对这两种类型的读是分为两部分的，第一次读取第一个 32 位，然后再读剩下的 32 位，这个过程不是原子的，但 Java 中 volatile 型的 long 或 double 变量的读写是原子的。volatile 修饰符的另一个作用是提供内存屏障（memory barrier），例如在分布式框架中的应用。简单的说，就是当你写一个 volatile 变量之前，Java 内存模型会插入一个写屏障（write barrier），读一个 volatile 变量之前，会插入一个读屏障（read barrier）。意思就是说，在你写一个 volatile 域时，能保证任何线程都能看到你写的值，同时，在写之前，也能保证任何数值的更新对所有线程是可见的，因为内存屏障会将其他所有写的值更新到缓存.

volatile 变量提供顺序和可见性保证，例如，JVM 或者 JIT为了获得更好的性能会对语句重排序，但是 volatile 类型变量即使在没有同步块的情况下赋值也不会与其他语句重排序。 volatile 提供 happens-before 的保证，确保一个线程的修改能对其他线程是可见的。某些情况下，volatile 还能提供原子性，如读 64 位数据类型，像 long 和 double 都不是原子的，但 volatile 类型的 double 和 long 就是原子的.

### transient变量有什么特点
我们都知道一个对象只要实现了Serilizable接口，这个对象就可以被序列化，java的这种序列化模式为开发者提供了很多便利，我们可以不必关系具体序列化的过程，只要这个类实现了Serilizable接口，这个类的所有属性和方法都会自动序列化.java 的transient关键字为我们提供了便利，你只需要实现Serilizable接口，将不需要序列化的属性前添加关键字transient，序列化对象的时候，这个属性就不会序列化到指定的目的地中.

1. 一旦变量被transient修饰，变量将不再是对象持久化的一部分，该变量内容在序列化后无法获得访问。

2. transient关键字只能修饰成员变量，而不能修饰局部变量和方法和类。注意，本地变量是不能被transient关键字修饰的。变量如果是用户自定义类变量，则该类需要实现Serializable接口。

3. 被transient关键字修饰的变量不再能被序列化，一个静态变量不管是否被transient修饰，均不能被序列化

4. Java中，对象的序列化可以通过实现两种接口来实现，若实现的是Serializable接口，则所有的序列化将会自动进行，若实现的是Externalizable接口，则没有任何东西可以自动序列化，需要在writeExternal方法中进行手工指定所要序列化的变量，这与是否被transient修饰无关。因此第二个例子输出的是变量content初始化的内容，而不是null.

### 基础类型(Primitives)与封装类型(Wrappers)的区别在哪里
1. 传递方式不同
封装类是引用类型。

基本类型（原始数据类型）在传递参数时都是按值传递，而封装类型是按引用传递的(其实“引用也是按值传递的”，传递的是对象的地址)。由于包装类型都是不可变量，因此没有提供改变它值的方法，增加了对“按引用传递”的理解难度。
int是基本类型，直接存放数值；Integer是类，产生对象时用一个引用指向.
2. 默认值不同
基本类型跟封装类型的默认值是不一样的。如int i,i的预设为0；Integer j，j的预设为null,因为封装类产生的是对象，对象默认值为null。
3. 封装类可以有方法和属性
封装类可以有方法和属性，利用这些方法和属性来处理数据，如Integer.parseInt(Strings)。基本数据类型都是final修饰的，不能继承扩展新的类、新的方法。
4.  存储位置
  * 基本类型在内存中是存储在栈中，引用类型的引用（值的地址）存储在栈中，而实际的对象（值）是存在堆中。
  * 虽然基本类型在栈上分配内存效率高，但是在堆栈上分配内存可能有内存泄漏的问题.
  * 基本数据类型的好处就是速度快（不涉及到对象的构造和回收），封装类的目的主要是更好的处理数据之间的转换。
  * JDK5.0开始可以自动封包了，基本数据类型可以自动封装成封装类。
