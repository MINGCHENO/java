## Java 8 / Java 7 为我们提供了什么新功能
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

## 请简述一下 Ajax 的原理及实现步骤
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


