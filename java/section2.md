# Java对象和类
java作为一种面向对象语言，支持一下基本概念：
+ 多态
+ 继承
+ 封装
+ 抽象
+ 类
+ 对象
+ 实例
+ 方法
+ 重载

## Java中的类
```java
public class Dog{
    String breed;
    int age;
    String color;
        void barking(){
    }
     
    void hungry(){
    }
     
    void sleeping(){
    }
}
```
一个类可以包含的类型变量
+ 局部变量：在方法，构造方法或者语句块中定义的变量称为局部变量。变量声明和初始化都在方法中，方法结束后，变量就会自动销毁

+ 成员变量：成员变量定义在类中，方法体之外的变量，这种变量在创建对象的时候实例化，成员变量可以被类中方法和特定类的语句块访问

+ 类变量：变量声明在类中，方法体之外，但必须声明为`static`类型

## 构造方法
>  每个类都有构造方法。如果没有显式地为类定义构造方法，Java编译器将会为该类提供一个默认构造方法。
>  在创建一个对象的时候，至少要调用一个构造方法。构造方法的名称必须与类同名，一个类可以有多个构造方法。

```java
public class Puppy{
    public Puppy(){
    }
 
    public Puppy(String name){
        // 这个构造器仅有一个参数：name
    }
}
```


## 创建对象
对象是根据类创建的。在Java中，使用关键字new来创建一个新的对象。创建对象需要以下三步：
+ 声明：声明一个对象，包括对象名称和对象类型
+ 实例化：使用关键字new来创建一个对象
+ 初始化：使用new创建对象时，会调用构造方法初始化对象
```java
public class Puppy{
   public Puppy(String name){
      //这个构造器仅有一个参数：name
      System.out.println("小狗的名字是 : " + name ); 
   }
   public static void main(String []args){
      // 下面的语句将创建一个Puppy对象
      Puppy myPuppy = new Puppy( "tommy" );
   }
}
```

## 访问实例变量和方法
```java
/*实例化对象*/
ObjectRefernce = new Constructor();
/*访问其中变量*/
ObjectRefernce.variableName;
/*访问类中方法*/
ObjectRefernce.MethodName();
```

## 源文件声明规则
+ 一个源文件只有一个public类
+ 一个源文件可有读个非public类
+ 源文件名应该和public类的类名保持一致
+ 如果一个类定义在某个包中，那么package语句应该在文件的首行
+ 如果源文件包含import语句，那么应该放在package语句和类定义之间。如果没有package语句，那么import语句应该在源文件最前面
+ import语句和package语句对源文件中定义的所有类都有效，在同一个源文件中，不能给不同类不同的包声明

## java包
包主要用来对类和接口进行分类

# java基本数据类型
java的两大数据类型:
+ 内置数据类型
+ 引用数据类型

## 内置数据类型
java语言提供了八种基本类型：六种数字类型(4个整型，两个浮点型)，一种字符类型，还有一种布尔类型
### byte
+ byte数据类型是8位，有符号的，以二进制补码表示正整数
+ 最小值-128(-2^7)
+ 最大值127(2^7 - 1)
+ 默认值是0
+ byte类型用在大型数组中节约空间，主要代替整数

### short
+ short数据类型是16位，有符号的以二进制补码表示的整数
+ 最小值-32768(-2^15)
+ 最大值32767(2^15 -1)

### int
+ int数据类型是32位，有符号的以二进制补码表示的整数
+ 最小值-2147483648(-2^31)
+ 最大值2147483647(2^31 - 1)
+ 一般的整型变量默认为int类型
+ 默认值是0

### long
+ long数据类型是64位，有符号的以二进制补码表示的整数
+ 最小值(-2^63)
+ 最大值(2^63-1)
+ 默认值是0L

### float
+ float数据类型是单精度，32位
+ 默认是0.0f

### double
+ double数据类型是双精度，64位
+ 浮点数的默认类型为double类型
+ 默认值是0.0d

### boolean
+ boolean数据类型表示一位的信息
+ 只有两个取值：true和false
+ 默认值是false

### char
+ char类型是一个单一的16位unicode字符


