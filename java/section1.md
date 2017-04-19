# java基础语法
+ 大小写敏感
+ 类名：类名首字母应该大写
+ 方法名：所有方法名应该小写
+ 源文件名：源文件名必须和类名相同
+ 主方法入口：所有的Java 程序由public static void main(String []args)方法开始执行。

# java标识符
+ 所有的标示符都应该以字母(A-Z或者a-z),美元符($),或者下划线(_)开始   不能以数字开头
+ 首字符之后可以是字母(A-Z或者a-z),美元符($),下划线(_)或数字的任何字符
+ 关键字不能做标识符
+ 标识符大小写敏感

# java修饰符
+ 访问控制修饰符:default,public,protected,private
+ 非访问控制修饰符:final,abstract,strictfp

# java变量
+ 局部变量
+ 类变量(静态变量)
+ 成员变量(非静态变量)

# java关键字
<table>
    <thead>
        <tr>
            <td>关键字</td>
            <td>描述</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>abstract</td>
            <td>抽象方法，抽象类的修饰符</td>
        </tr>
        <tr>
            <td>assert</td>
            <td>断言条件是否满足</td>
        </tr>
        <tr>
            <td>boolean</td>
            <td>布尔类型数据</td>
        </tr>
        <tr>
            <td>break</td>
            <td>跳出循环或者label代码</td>
        </tr>
        <tr>
            <td>byte</td>
            <td>8-bit 有符号数据类型</td>
        </tr>
        <tr>
            <td>case</td>
            <td>switch语句的一个条件</td>
        </tr>
        <tr>
            <td>char</td>
            <td>16-bit Unicode字符数据类型</td>
        </tr>
        <tr>
            <td>class</td>
            <td>定义类</td>
        </tr>
        <tr>
            <td>const</td>
            <td>未使用</td>
        </tr>
        <tr>
            <td>continue</td>
            <td>不执行循环体剩余部分</td>
        </tr>
        <tr>
            <td>default</td>
            <td>switch语句中的默认分支</td>
        </tr>
        <tr>
            <td>do</td>
            <td>循环语句,循环体至少执行一次</td>
        </tr>
        <tr>
            <td>double</td>
            <td>64-bit 双精度浮点数</td>
        </tr>
        <tr>
            <td>else</td>
            <td>if条件不成立时执行的分支</td>
        </tr>
        <tr>
            <td>enum</td>
            <td>枚举类型</td>
        </tr>
        <tr>
            <td>extends</td>
            <td>表示一个类是另一个类的子类</td>
        </tr>
        <tr>
            <td>final</td>
            <td>表示一个值在初始化之后就不能再改变了e<br/>表示方法不能被重写</td>
        </tr>
        <tr>
            <td>float</td>
            <td>32-bit单精度浮点数</td>
        </tr>
        <tr>
            <td>for</td>
            <td>for循环语句</td>
        </tr>
        <tr>
            <td>goto</td>
            <td>未使用</td>
        </tr>
        <tr>
            <td>if</td>
            <td>条件语句</td>
        </tr>
        <tr>
            <td>implements</td>
            <td>表示一个类实现了接口</td>
        </tr>
        <tr>
            <td>import</td>
            <td>导入类</td>
        </tr>
        <tr>
            <td>instanceof</td>
            <td>测试一个对象是否是某个类的实例</td>
        </tr>
        <tr>
            <td>int</td>
            <td>32位整型数</td>
        </tr>
        <tr>
            <td>interface</td>
            <td>接口，一种抽象的类型，仅有方法和常量的定义</td>
        </tr>
        <tr>
            <td>long</td>
            <td>64位整型数</td>
        </tr>
        <tr>
            <td>native</td>
            <td>表示方法非java代码实现</td>
        </tr>
        <tr>
            <td>new</td>
            <td>分配新的类实例</td>
        </tr>
        <tr>
            <td>package</td>
            <td>一系列相关类组成一个包</td>
        </tr>
        <tr>
            <td>protected</td>
            <td>表示字段只能通过类或者其子类访问</td>
        </tr>
        <tr>
            <td>public</td>
            <td>表示共有属性或方法</td>
        </tr>
        <tr>
            <td>return</td>
            <td>方法返回值</td>
        </tr>
        <tr>
            <td>short</td>
            <td>16为数字</td>
        </tr>
        <tr>
            <td>static</td>
            <td>表示在类级别定义，所有实例共享</td>
        </tr>
        <tr>
            <td>strictfp</td>
            <td>浮点数比较使用严格的规则</td>
        </tr>
        <tr>
            <td>super</td>
            <td>表示基类</td>
        </tr>
        <tr>
            <td>switch</td>
            <td>选择语句</td>
        </tr>
        <tr>
            <td>synchronized</td>
            <td>表示同一时间只能由一个线程访问的代码块</td>
        </tr>
        <tr>
            <td>this</td>
            <td>表示调用当前实例/调用另一个构造函数</td>
        </tr>
        <tr>
            <td>throw</td>
            <td>抛出异常</td>
        </tr>
        <tr>
            <td>throws</td>
            <td>定义方法可能抛出异常</td>
        </tr>
        <tr>
            <td>transient</td>
            <td>修饰不要序列化的字段</td>
        </tr>
        <tr>
            <td>try</td>
            <td>表示代码块要做异常处理和finally配合表示抛出异常都执行finally中德代码</td>
        </tr>
        <tr>
            <td>void</td>
            <td>标记方法不返回任何值</td>
        </tr>
        <tr>
            <td>volatile</td>
            <td>标记字段可能被多个线程同时访问，而不做同步</td>
        </tr>
        <tr>
            <td>while</td>
            <td>while循环</td>
        </tr>
    </tbody>
</table>

# 继承
在java中，一个类可以由其他类派生，如果创建一个类，而且已经存在一个具有你所需要的属性或方法，那么可以将创建的类继承该类。  
利用继承的方法，可以重用已存在类的方法和属性，而不用重写代码，被继承的类称为超累，派生类成为子类(subclass)

# 接口
在Java中，接口可理解为对象间相互通信的协议。接口在继承中扮演着很重要的角色。
接口只定义派生要用到的方法，但是方法的具体实现完全取决于派生类。