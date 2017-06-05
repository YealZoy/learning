# java"白皮书"的关键术语
+ 简单性
+ 面向对象
+ 网络技能
+ 健壮性
+ 安全性
+ 体系结构中立
+ 可移植性
+ 解释型
+ 高性能
+ 多线程
+ 动态性

# 安装库源文件和文档
+ 确保jdk已经安装，在jdk/bin目录在执行路径中
+ 打开shell窗口
+ 进入jdk目录
+ 建立一个子目录src
```
mkdir src
cd src
```
+ 执行命令;
```
jar xvf ../src.zip
```

# 数据类型
在java中，一共有8种基本类型，其中有4种整型，2种浮点型，一种用于表示Unicode编码的字段但愿的字符类型char和一种表示真值得boolean类型

## 整型
<table>
    <thead>
        <tr>
            <td>类型</td>
            <td>存储需求</td>
            <td>取值范围</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>byte</td>
            <td>8位(1字节)</td>
            <td>-2^7 ~ 2^7-1</td>
        </tr>
        <tr>
            <td>short</td>
            <td>16位(2字节)</td>
            <td>-2^16 ~ 2^16-1</td>
        </tr>
        <tr>
            <td>int</td>
            <td>32位(4字节)</td>
            <td>-2^32 ~ 2^32-1</td>
        </tr>
        <tr>
            <td>long</td>
            <td>64位(8字节)</td>
            <td>-2^64 ~ 2^64-1</td>
        </tr>
    </tbody>
</table>

## 浮点类型
<table>
    <thead>
        <tr>
            <td>类型</td>
            <td>存储需求</td>
            <td>取值范围</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>float</td>
            <td>32位(4字节)</td>
            <td>有效位数6~7</td>
        </tr>
        <tr>
            <td>double</td>
            <td>64位(8字节)</td>
            <td>有效数为15位</td>
        </tr>
    </tbody>
</table>

所有的浮点数值计算都遵循IEEE754规范。表示溢出和出错情况的三个特殊浮点数值
+ 正无穷大
+ 负无穷大
+ NaN(不是一个数字)

***常量Double.POSITIVE_INFINITY,Double.NEGATIVE_INFINITY和Double.NaN分别表示这3个特殊的值***
```java
if(x == Double.NaN)//is never true
//所有"非数值"的值都认为是不相同的
if(Double.isNaN(x))
```

***浮点数值不是用于禁止出现舍入误差的金融计算中。例如，命令System.out.println(2.0-1.1)将打印出0.89999999999999，而不是人们想象的0.9，其主要原因是浮点数值采用二进制系统表示，而在二进制系统中无法精确的表示分数1/10。就好像十进制无法精确的表示1/3一种。如果需要在数值计算中不含有任何误差，就应该使用BigDecimal类***

## char类型
char类型用于表示单个字符。通常用来表示字符常量。Unicode编码单元可以表示为十六进制值，其范围从\u0000到\ufff。
特殊转义字符
<table>
    <thead>
        <tr>
            <td>转义序列</td>
            <td>名称</td>
            <td>Unicode值</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>\b</td>
            <td>退格</td>
            <td>\u0008</td>
        </tr>
        <tr>
            <td>\t</td>
            <td>制表</td>
            <td>\u0009</td>
        </tr>
        <tr>
            <td>\n</td>
            <td>换行</td>
            <td>\u000a</td>
        </tr>
        <tr>
            <td>\r</td>
            <td>回车</td>
            <td>\u000d</td>
        </tr>
        <tr>
            <td>\"</td>
            <td>双引号</td>
            <td>\u0022</td>
        </tr>
        <tr>
            <td>\'</td>
            <td>单引号</td>
            <td>\u0027</td>
        </tr>
        <tr>
            <td>\\</td>
            <td>反斜杠</td>
            <td>\u005c</td>
        </tr>
    </tbody>
</table>

## boolean类型
boolean(布尔类型)有两个值：false和true

# 变量
在java中，每一个变量属于一种类型(type)。在声明变量时，变量所属的类型位于变量名之前
```java
double salary;
int vacationDays;
long earthPopulation;
boolean done;
```

变量名必须是一个以字母开头的由字母或数字构成的序列(字母包括A~Z,a~z,_,$),区分大小写

### 变量初始化
```java
int vacationDays;
vacationDays =3;
```

# 常量
在java中，利用关键字final指示常量
```java
public class Constans{
    public static void main(String[] args){
        final double CM_PRE_INCH = 2.54;
    }
}
```

关键字final表示变量只能被赋值一次。一旦被赋值之后，就不能够再改变了。常量名使用全大写。

# 关系运算符与boolean运算符
+ 使用两个`==`检测是否相等
+ 使用`!=`检测是否不相等
+ 还有`>`,`<`,`>=`,`<=`
+ `&&`,`||`
+ `condition ? expression1:expression2`

# 数学函数与常量
Math类提供了一些常用的三角函数
+ Math.sin
+ Math.cos
+ Math.tan
+ Math.actan
+ Math.atan2
Math类提供了两个用于表示Pi和e常量的近似值
+ Math.PI
+ Math.E
*不必在数学方法名和常量名前添加前缀`Math`,只要在源文件的顶部加上*
```java
import static java.lang.Math.*;
System.out.println("the square root of \u03c0 is" + sqrt(PI));
```

# 数值类型之间的转换
数值之间的合法转换  
![../images/number2.png]()  
当使用上表面两个数值进行二元操作时，先要将两个操作数转换为同一种类型，然后再进行计算。
+ 如果两个操作数中有一个是double类型，另一个操作数就会转换为double类型
+ 否则，如果其中一个操作数是float类型，另一个操作数将会转换为float类型
+ 否则，如果其中一个操作数是long类型，另一个操作数将会转换为long类型
+ 否则，两个操作数都将被转换为int类型

# 强制类型转换
在必要的时候，int类型的值将会自动地转换为double类型。但另一方面，有时也需要将double转换成int。在转换的过程中，有可能会丢失一些信息。在这种情况下需要通过强制类型转换(cast)实现这个操作。强制类型转换的语法格式是在圆括号中给出想要的转换目标类型，后面紧跟待转换的变量名。
```java
double x = 9.997;
int nx = (int) x;
```
变量nx的值为9。强制类型转换通过截断小数部分浮点值转换为整型

# 枚举类型
```java
enum Size {SMALL,MEDIUM,LAGRE,EXTRE_LAGRE}
Size s = Size.MEDIUM;
```

# 字符串
```java
String e = "";//空串
String greeting = "Hello";

//子串
String s = greeting.substring(0,3);//Hel，从0开始，但不包含3

//拼接
String explective = "Expletive";
String PG13 = "delete";
String message = explective + PG13;
```
当将一个字符串与一个非字符串的值进行拼接时，后者被转换成字符串
```java
int age = 13;
String rating = "PG" + age;
```

# 检测字符串是否相等
```java
s.equal(t);
```
一定不能使用`==`运算符检测两个字符串是否相等！这个运算符只能够确定两个字符串是否放置在同一个位置上。如果字符串放置在同一个位置上，它们必然相等。
*如果虚拟机始终将相同的字符串共享，就可以使用==运算符检测是否相等。但实际上只有字符串常量是共享，而`+`或`substring`等操作产生的结果并不是共享的。*

# 空串与Null串
空串""是长度为0的字符串
```java
if(str.length()==0)或
if(str.equals(""))
```

```java
if(str==null)
//检查一个字符串既不是null也不为空串
if(str != null && str.length() != 0)
```

# 代码点与代码单元
java字符串由char序列组成
```java
String greeting = "hello";
int n = greeting.length();//5
//实际长度，代码点数量
int cpCount = greeting.codePointCount(0,greeting.length());

//调用s.chartAt(n)将 
char first = greeting.charAt(0);//h
char last = greeting.charAt(4);//o

//得到第i个代码点
int index = greeting.offsetByCodePoints(0,i);
int cp = greeting.codePointAt(index);
```


# 字符串API
+ char charAt(int index) 返回给定位置的代码单元
+ int codePointAt(int index) 返回给定位置开始或结束的代码点
+ int offsetByCodePoints(int startIndex,int cpCount) 返回从startIndex代码点开始，位移cpCount后的代码点索引
+ int compareTo(String other) 按照字典顺序，如果字符串位于other之前，返回一个负数；如果字符串位于other之后，返回一个整数；如果两个字符串相等，返回0
+ boolean endsWith(String suffix) 如果字符串以suffix结尾，返回true
+ boolean equals(Object other) 如果字符串与other相等，返回true
+ boolean equalsIgnoreCase(String other) 如果字符串与other相等(忽略大小写)
+ int indexOf(String str)
+ int indexOf(String str,int fromIndex)
+ int indexOf(int cp)
+ int indexOf(int cp,int fromIndex) 返回与字符串str或代码点cp匹配的第一个子串的开始位置。这个位置从索引0或fromIndex开始计算。如果在原始串中不存在str,返回-1
+ int lastIndexOf(String str)
+ int lastIndexOf(String str,int fromIndex)
+ int lastIndexOf(int cp)
+ int lastIndexOf(int cp,int fromIndex) 返回与字符串str或代码点cp匹配的最后一个子串的开始位置。这个位置从原始串尾端或fromIndex开始计算
+ int length() 返回字符串的长度
+ int codePointCount(int startIndex,int endIndex)返回startIndex和endIndex-1 之间的代码数量。没有配成对的代用字符将计入代码点
+ String replace(CharSequence oldString,charSequence newString) 返回一个新字符串。这个字符串用newString代替原始字符串中所有的oldString。可以用String或StringBuilder对象作为CharSequence参数
+ 




