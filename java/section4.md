# java运算符
## 自增自减运算
+ 自增(++)自减(--)运算符是一种特殊的算术运算符，在算术运算符中需要连个操作数来进行运算，而自增自减运算符是一个操作数
+ 前缀自增自减法(++a;--a)先进行自增或者自减运算，再进行表达式运算
+ 后缀自增自减法(a++;a--)先进行表达式运算，再进行自增或者自减运算

## instalceof运算符
该运算符用于操作对象实例，检查该对象是否是一个特定类型(类类型或接口类型)
`(Object reference variable) instanceof (class/instance type)`

如果运算符左侧变量所指的对象，是操作符右侧类或接口(class/interface)的一个对象，那么结果为真
```java
String name = "James";
boolean result = name instanceof String;
```


