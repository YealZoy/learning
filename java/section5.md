# java Number & Math类
所有的包装类(Interger,Long,Byte,Double,Float,Short)都是抽象类Number的子类
![](https://github.com/YealZoy/learning/blob/master/images/number1.png)

# java继承
继承的特性:
+ 子类拥有父类非private的属性，方法
+ 子类可以拥有自己的属性和方法，即子类可以对父类进行扩展
+ 子类可以用自己的方式实现父类的方法
+ java的继承是单继承，但是可以多重继承，单继承就是一个子类只能继承一个父类
+ 提高了类之间的耦合性

## 继承关键字
+ extends
+ implements

```java
public interface A {
    public void eat();
    public void sleep();
}
 
public interface B {
    public void show();
}
 
public class C implements A,B {
}
```

+ super:通过super关键字来实现对父类成员的访问,用来引用当前对象的父类
+ this:指向自己的引用

```java
public class SuperDemo {
    public static void main(String []args) {
        new SubClass().showMessage();
    }
}
 
class SuperClass {
    int i = 50;
}
 
class SubClass extends SuperClass {
    int i =100;
    public void showMessage() {
        System.out.printf("super.i = %d, this.i = %d\n", super.i, this.i);
    }
}
```

## 构造器
子类不能继承父类的构造器（构造方法或者构造函数），但是父类的构造器带有参数的，则必须在子类的构造器中显式地通过super关键字调用父类的构造器并配以适当的参数列表。
如果父类有无参构造器，则在子类的构造器中用super调用父类构造器不是必须的，如果没有使用super关键字，系统会自动调用父类的无参构造器。

# java重写与重载
## 重写
重写是子类对父类的允许访问的方法的实现过程进行重新编写，返回值和形参都不能改变，即外壳不变，核心重写

方法重写的规则
+ 参数列表必须完全与被重写方法的相同
+ 返回类型必须完全与被重写方法的返回类型相同
+ 访问权限不能比父类中被重写的方法的访问权限更低
+ 父类的成员方法只能被它的子类重写
+ 声明为final的方法不能别重写
+ 声明为static的方法不能被重写，但是能够被再次声明
+ 子类和父类在同一个包中，那么子类可以重写父类所有方法，除了声明为private和final方法
+ 子类和父类不在同一个包中，那么子类只能够重写父类的声明为public和protected的非final方法。
+ 重写的方法能够抛出任何非强制异常，无论被重写的方法是否抛出异常。但是，重写的方法不能抛出新的强制性异常，或者比被重写方法声明的更广泛的强制性异常，反之则可以。
+ 构造方法不能被重写。
+ 如果不能继承一个方法，则不能重写这个方法。

# 重载(Overload)
重载(overloading) 是在一个类里面，方法名字相同，而参数不同。返回类型可以相同也可以不同。
每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。
最常用的地方就是构造器的重载。
+ 被重载的方法必须改变参数列表(参数个数或类型或顺序不一样)；
+ 被重载的方法可以改变返回类型；
+ 被重载的方法可以改变访问修饰符；
+ 被重载的方法可以声明新的或更广的检查异常；
+ 方法能够在同一个类中或者在一个子类中被重载。
+ 无法以返回值类型作为重载函数的区分标准。