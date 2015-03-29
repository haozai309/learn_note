# Basic of Java



Java vs. C++
 * Java has virtual machine
 * Java has gabage collection, C/C++ could manage memory directly

JDK & JRE
 * development kit & runtime environment
 * java, javac, JVM, class library


Java:
  没有指针，但reference实现指针的功能，或reference可以称作安全指针。

  包：解决名字冲突，通过import导入，如import util.*;

  Outlint: Operator -> control flow -> init
        -> package -> 复用    -> 多态
        -> 接口    -> 内部类  -> 持有对象 (list/stack/set/map/queue)
        -> String  -> 类型    -> 泛型
        -> 数据    -> 容器    -> Java I/O
        -> 枚举    -> 注解    -> 并发  -> Swing/SWT


Code temple:
```
 package ...

 import ...

 public class AXXX { ... }
```

Import:
 * Class is loaded when firstly used, not when imported
 * Class冲突时，使用 package.name，如java.util.Date & java.sql.Date
 * import aaa.bbb.*; 仅包含当前的一层，不包含*.**


Identifier: begin with letter, $ and _, followed with letter, $, _, number

boolean vs. Boolean
 * primitive type vs. wrapper class, the latter cann't be changed
 * if (0) {...} // wrong, only support boolean type
 * 自定义类的equals()默认比较引用，深度比较需要重写此方法

Operator
 * c = d;   // c is object, 浅复制，仅引用地址
 * fun(c);  // c is object, 传递对象的引用
 * + - * / = % < > >= <= == != && || !

Variable:
  * Member of class, has default value (0/null ...)
    * Static: class loaded
    * Non-static, loaded before execute
  * automatic: local, no default value (if used before init, error occured)

Flow:
 * if, else, while, do, return, break, continue
 * switch, case, break, default


重载
 * 仅参数列表不同，构造器和方法
 * static方法属于类，non-static方法属于对象
 * 静态static方法中不能调用非静态non-static方法

类
 * 变量定义先后决定了初始化顺序，static变量仅一次
 * 一个构造器可以调用另一个，但不能调用两个，且需置顶
 * 在类的内部，只在必要处加this

构造器
 * 无参构造器和有参构造器
 * 无1, 2，系统创建1；仅有2，系统不会创建1 (若使用1，编译器报错)

权限
 * public -> package -> protected -> private


Error
 * Runtime error：数组下标越界


JNI: Java native interface

