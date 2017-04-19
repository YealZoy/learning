# java修饰符
java修饰符分为两类:
+ 访问修饰符
+ 非访问修饰符
修饰符用来定义类，方法或者变量，通常放在语句的最前端

# 访问控制修饰符
java中，可以使用访问控制符莱保护对类，变量，方法和构造方法的访问。java有4种不同的访问权限
+ 默认的,也称为default,在同一包内可见，不使用任何修饰符
+ 私有的,以private修饰符指定，在同一类可见
+ 共有的，以public修饰符指定，对所有类可见
+ 受保护的，以protected修饰符指定，对同一包内的类和所有子类可见
<table>
    <thead>
        <tr>
            <td>修饰符</td>
            <td>当前类</td>
            <td>同一包内</td>
            <td>子孙类</td>
            <td>其他包</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>public</td>
            <td>Y</td>
            <td>Y</td>
            <td>Y</td>
            <td>Y</td>
        </tr>
        <tr>
            <td>protected</td>
            <td>Y</td>
            <td>Y</td>
            <td>Y</td>
            <td>N</td>
        </tr>
        <tr>
            <td>default</td>
            <td>Y</td>
            <td>Y</td>
            <td>N</td>
            <td>N</td>
        </tr>
        <tr>
            <td>private</td>
            <td>Y</td>
            <td>N</td>
            <td>N</td>
            <td>N</td>
        </tr>
    </tbody>
</table>

# 访问控制和继承
+ 父类中声明为public的方法在子类中必须为public
+ 父类中声明为protected的方法在子类中要么声明为protected,要么声明为public,不能声明为private
+ 父类中声明为private的方法，是不能被继承的

# 非访问修饰符
+ static修饰符，用来创建类方法和类变量
+ final修饰符，有来修饰类，方法和变量，final修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的
+ abstract修饰符，用来创建抽象类和抽象方法
+ synchronized和volatile修饰符，主要用于线程的编程

## static修饰符
+ 静态变量:static关键字用来声明独立于对象的静态变量，无论一个类实力话多少个对象，它的静态变量只有一份拷贝。静态变量也被称为类变量。局部变量不能被声明为static变量。
+ 静态方法：static关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。
对类变量和方法的访问可以直接使用classname.variablename和classname.methodname的方式访问

## final修饰符
+ final变量：能被显式地初始化并且只能初始化一次。被声明为final的对象的引用不能指向不同的对象，但是final对象里的数据是可以改变。也就是说final对象的引用不能改变，但是里面的值可以改变
+ final方法：类中的final方法可以被子类继承，但是不能被子类修改
+ final类：不能被继承

## abstract修饰符
+ 抽象类：不能用来实例化对象，声明抽象类的唯一目的是为了将来对该类进行扩充(一个类不能同时被abstract和final修饰。如果一个类包含抽象方法，那么该类一定要声明为抽象类)
+ 抽象方法: 是一种没有任何实现的方法，该方法的具体实现由子类提供，抽象方法不能声明fianl和static,任何继承抽象类的子类必须实现父类所有的抽象方法，除非该子类也也是抽象类，如果一个类包含若干个抽象方法，那么该类必须声明为抽象类。抽象类可以不包含抽象方法

## synchronized修饰符
synchronized关键字声明的方法同一时间只能被一个线程访问。synchronized修饰符可以应用于四个访问修饰符

## transient修饰符
序列化的对象包含被transient修饰的实例变量时，java虚拟机(jvm)跳过该特定的变量，该修饰符包含在定义的变量的语句中，用来预处理和变量的数据类型

## volatile修饰符
volatitle修饰的成员变量在每次被线程访问时，都强制从共享内存中重新读取该成员变量的值。而且，当成员变量发生变化时，会强制线程将变化值回写到共享内存。这样在任何时刻，连个不同的线程总是看到某个成员变量的同一个值