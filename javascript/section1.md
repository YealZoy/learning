# javaScript实现
+ 核心(ECMAScript)
+ 文档对象模型(DOM)
+ 浏览器对象模型(BOM)

# DOM级别
+ DOM1级由两个模块组成DOM核心(DOM Core)和DOM HTML,DOM核心规定的是如何映射基于XML的文档结构，以便简化对文档中任意部分的访问和操作。DOMHTML模块则在DOM核心的基础上加以扩展，添加了针对HTML的对象和方法
+ DOM2级在原来DOM的基础上又扩充了(DHTML一直都支持的)鼠标和用户界面事件，范围，便利(迭代DOM文档的方法)等细分模块
    + DOM视图(DOM Views):定义了跟踪不同文档视图的接口
    + DOM事件(DOM Events):定义了事件和处理事件的接口
    + DOM样式(DOM Style):定义了基于css为元素应用的样式接口
    + DOM遍历和范围(DOM traversal and range):定义了遍历和操作文档树的接口
+ DOM3引入以统一方式加载和保存文档的方法——在DOM加载和保存(DOM Load and save)模块中定义;新增了验证文档的方法——在DOM验证(DOM Validation)模块中定义

# 浏览器对象模型(BOM只处理浏览器窗口和框架)
+ 弹出新浏览器窗口的功能
+ 移动、缩放和关闭浏览器窗口的功能
+ 提供浏览器详细信息的navigator对象
+ 提供浏览器所加载页面的详细信息的location对象
+ 提供用户显示器分辨率详细信息的screen对象
+ 对cookies的支持
+ 像XMLHttpRequest和IE的ActiveXobject这样的自定义对象

# script标签元素定义了6个属性
+ async:可选。表示应该立即下载脚本，但不妨碍页面中的其他操作，比如下载其他资源或等待加载其他脚本。只对外部脚本文件有效
+ chartset:可选。表示通过src属性指定的代码的字符集
+ defer:可选。表示脚本可以延迟到文档完全被解析和显示之后再执行。只对外部脚本文件有效
+ language:可选。已废弃，原来用于表示编写代码使用的脚本语言(如JavaScript,JavaScript1.2或VBscript)
+ src:可选。表示包含要执行代码的外部文件(也称MIME类型)。虽然`text/javascript`和`text/ecmascript`都已经不被推荐使用。实际上，服务器在传送javascript文件时使用的MIME类型通常是`application/x-javascript`，但在type中设置这个值却可能导致脚本被忽略

# javascript在XHTML中的用法
```html
<script type="text/javascript">
    function compare(a,b){
        if(a < b){
            alert("A is less than B");
        }else if(a > b){
            alert("A is greater than B");
        }else{
            alert("A is equal to B")
        }
    }
</script>
```
*这段代码在XHTML中不适用，小于号在XHTML中将被当作开始一个新标签的规则来解析。但作为标签来讲，小于号后面不能跟空格，因此就会导致语法错误*
```html
<script type="text/javascript">
    function compare(a,b){
        if(a &lt; b){
            alert("A is less than B");
        }else if(a > b){
            alert("A is greater than B");
        }else{
            alert("A is equal to B")
        }
    }
</script>
```
*不好理解*

```html
<script type="text/javascript">
//<![CDATA[
    function compare(a,b){
        if(a < b){
            alert("A is less than B");
        }else if(a > b){
            alert("A is greater than B");
        }else{
            alert("A is equal to B")
        }
    }
//]]>
</script>
```

# 文档模式
```html
<!--标准模式，可以通过下面任何一种文档类型开启-->

<!--HTML 4.01 严格型-->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"
    "http://www.w3.org/TR/html4/strict.dtd">

<!--XHTML 1.0 严格型-->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
    "http://www.w3.org/TR/html4/strict.dtd">

<!--HTML 5-->
<!DOCTYPE html>


<!--对于标准模式，可以通过使用过渡型(transitional)或框架集型(frameset)文档类型来触发-->
<!--HTML 4.01 过渡型-->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"
    "http://www.w3.org/TR/html4/loose.dtd">

<!--HTML 4.01 框架集型-->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN"
    "http://www.w3.org/TR/html4/frameset.dtd">

<!--XHTML 1.0 过渡型-->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">


<!--XHTML 1.0 框架集型-->
<!DOCTYPE HTML PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN"
    "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

# 标识符
指变量、函数、属性的名字，或者函数的参数
+ 第一个字符必须是一个字母，下划线 (_)或一个美元符($)
+ 其他字符可以是字母，下划线，美元符或数字

# 关键字
<table>
    <tr>
        <td>break</td>
        <td>do</td>
        <td>instance</td>
        <td>typeof</td>
    </tr>
    <tr>
        <td>case</td>
        <td>else</td>
        <td>new</td>
        <td>var</td>
    </tr>
    <tr>
        <td>catch</td>
        <td>finally</td>
        <td>return</td>
        <td>void</td>
    </tr>
    <tr>
        <td>continue</td>
        <td>for</td>
        <td>switch</td>
        <td>while</td>
    </tr>
    <tr>
        <td>debugger*</td>
        <td>function</td>
        <td>this</td>
        <td>with</td>
    </tr>
    <tr>
        <td>default</td>
        <td>if</td>
        <td colspan="2">throw</td>
    </tr>
    <tr>
        <td>delete</td>
        <td>in</td>
        <td colspan="2">try</td>
    </tr>
</table>

# 保留字
<table>
    <tr>
        <td>abstract</td>
        <td>enum</td>
        <td>int</td>
        <td>short</td>
    </tr>
    <tr>
        <td>boolean</td>
        <td>export</td>
        <td>interface</td>
        <td>static</td>
    </tr>
    <tr>
        <td>byte</td>
        <td>extends</td>
        <td>long</td>
        <td>super</td>
    </tr>
    <tr>
        <td>char</td>
        <td>final</td>
        <td>native</td>
        <td>synchronized</td>
    </tr>
    <tr>
        <td>class</td>
        <td>float</td>
        <td>package</td>
        <td>throws</td>
    </tr>
    <tr>
        <td>const</td>
        <td>goto</td>
        <td>private</td>
        <td>transient</td>
    </tr>
    <tr>
        <td>debugger</td>
        <td>implements</td>
        <td>protected</td>
        <td>volatile</td>
    </tr>
    <tr>
        <td>double</td>
        <td>import</td>
        <td colspan="2">public</td>
    </tr>
</table>

# 数据类型
ECMAScript有5种简单数据类型(基本数据类型)：Undefined、Null、Boolean、Number、String,还有一种复杂数据类型Object

# typeof操作符
+ "undefined"——如果这个值为定义
+ "boolean"——如果这个值是布尔值
+ "string"——如果这个值是字符串
+ "number"——如果这个值是数值
+ "object"——如果这个值是对象或null
+ "function"——如果这个值是函数
调用typeof null会返回"object",因为特殊值null被认为是一个空的对象引用，typeof是操作符，不是函数

# undefined
undefined类型只有一个值，即特殊的undefined。在使用var声明变量但未对其他加以初始化时，这个变量的值就是undefined

# Null类型
Null类型只有一个值，即特殊的nul。null值表示一个空对象指针，所以typeof操作符检测null值时会返回"object"
undefined是派生自null
```javascript
alert(null == undefined);//true
```

# Boolean
各类型转换规则
<table>
    <thead>
        <tr>
            <td>数据类型</td>
            <td>转换为true的值</td>
            <td>转换为false的值</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Boolean</td>
            <td>true</td>
            <td>false</td>
        </tr>
        <tr>
            <td>String</td>
            <td>任何非空字符串</td>
            <td>""(空字符串)</td>
        </tr>
        <tr>
            <td>Number</td>
            <td>任何非零数字值(包括无穷大)</td>
            <td>0和NaN</td>
        </tr>
        <tr>
            <td>Object</td>
            <td>任何对象</td>
            <td>null</td>
        </tr>
        <tr>
            <td>undefined</td>
            <td>不适用</td>
            <td>undefined</td>
        </tr>
    </tbody>
</table>

# 字符串
字符串的特点:字符串是不可变的，一旦创建，它们的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串，然后再用另一个包含新值的字符串填充该变量

# Object类型
对象就是一组数据和功能的集合。对象可以通过执行new操作符后跟要创建的对象类型的名称来创建。而创建Object类型的实例并为其添加属性和方法，可以创建自定义对象。
Object的每个实例都具有下列属性和方法
+ constructor:保存着用于创建当前对象的函数。
+ hasOwnProperty(propertyName):用于检查给定的属性在当前对象实例中(而不是在实例的原型中)是否存在。其中，作为参数的属性名(propertyName)必须以字符串形式制定
+ isPrototypeOf(object):用于检查传入对象是否是当前对象的原型
+ propertyIsEnumerable(propertyName):用于检查给定的属性是否能够用for-in语句来枚举
+ toLocaleString():返回对象字符串的表示,该字符串与执行环境的地区对应
+ toString():返回对象字符串表示。
+ valueOf():返回对象的字符串、数值或布尔值表示。通常与toString()方法的返回值相同

# 复制变量值
在从一个变量向另一个变量赋值基本类型的值，会在变量对象上创建一个新值，然后把该值复制到为新变量分配位置上
```javascript
var num1 = 5;
var num2 = num1;
```

num1中保存的值时5。当使用num1的值来初始化num2时，num2也保存了值5。但num2中的5与num1中的5是完全独立的，该值只是num1中的5一个副本。此后，两个变量可以参与任何操作而互不影响。  
复制前的变量对象
<table>
    <tr>
        <td>  </td>
        <td>   </td>
    </tr>
    <tr>
        <td>   </td>
        <td>   </td>
    </tr>
    <tr>
        <td>num1</td>
        <td>5<br/>(Number类型)</td>
    </tr>
</table>

————————————————————————————————————————————————  

复制后的变量对象
<table>
    <tr>
        <td>   </td>
        <td>  </td>
    </tr>
    <tr>
        <td>num2</td>
        <td>5<br/>(Number类型)</td>
    </tr>
    <tr>
        <td>num1</td>
        <td>5<br/>(Number类型)</td>
    </tr>
</table>

当一个变量向另一个变量复制引用类型的值时，同样也会将存在存储变量对象中的值复制一份放到为新变量分配的空间中。不同的是，这个值的副本实际上是一个指针，而这个指针指向存在堆中的一个对象。复制操作结束后，两个变量实际上将引用同一个对象。因此改变其中一个变量，就会影响另外一个变量  
![](https://github.com/YealZoy/learning/blob/master/images/copy.jpg)

# 传递参数
所有函数的参数都是按值传递的。也就是说，把函数外部的值复制给函数内部的参数，就和把值从一个变量复制到另一个变量一样。
```javascript
function addTen(){
    num += 10;
    return num;
}
 var count = 20;
 var result = addTen();
 alert(count);//20
 alert(result);//30

//----------------------------
function setName(obj){
    obj.name = "Nicholas";
}

var person = new Object();
setName(person);
alert(person.name);//Nicholas
```

# 检测类型



