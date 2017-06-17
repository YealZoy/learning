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

调用typeof null会返回"object", 因为特殊值null被认为是一个空的对象引用，typeof是操作符，不是函数

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

# 引用类型
## object类型
创建object有两种方式
```javascript
//-----------------方式一
var person = new Object();
person.name = "郑玉燕";
person.age = 27;

//-----------------方式二
var person = {
    name:"郑玉燕",
    age:27
}
```

## Array类型
创建Array的方式有两种
```javaScript
//-----------方式一
var colors = new Array();
var colors = new Array(20);
var colors = new Array('red','blue');
//------------方式二
var colors = ['red','blue'];
```

### 检测数组
```javaScript
if(value instanceod Array){
    //对数组进行操作
}
//instanceof操作符的问题在于，它假定只有一个全局执行环境。如果网页包含多个框架，那实际上就存在两个以上不同全局执行环境，从而存在两个以上不用版本的Array构造函数。如果从一个框架传入一个数组，那么传入的数组与在第二个框架中原生创建的数组分别具有各自不同的构造函数。为了解决这个问题es5新增了Array.isArray()方法
if(Arrar.isArray(value)){
    //对数组进行操作
}
```

### 数组转换方法
调用toString()方法会返回数组中每个值得字符串形式拼接而成的以一个逗号分隔的字符串
join()方法，可传入一个参数，返回值为以传入参数的分隔符拼接的字符串

### 找方法（后进先出）
+ push():可以接受任意数量的参数，把它们逐个添加到数组末尾，并返回修改后的数组长度
+ pop():从数组末尾移除最后一项，减少数组的length,然后返回移除的项

### 队列方法(先进先出)
+ shift():移除数组中的第一个项并返回该项
+ unshift():在数组前端添加任意个项并返回数组的长度

### 重排序
+ reserve():翻转数组项的顺序
+ sort():默认情况下按升序排列数组项,sort()方法会调用每一个数组项的toString()转型方法，然后比较得到的字符串，以确定如何排序，sort()方法可以接收一个比较函数作为参数，比较函数接收两个参数，如果第一个参数应该位于第二个之前则返回一个负数，如果两个参数相等则返回0,如果第一个参数应该位于第二个参数之后则返回一个正数。

### 操作方法
+ concat():这个方法会先创建当前数组的一个副本，然后将接收到的参数添加到这个副本的末尾，最后返回新构建的数组。在没有给concat()方法传递参数的情况下，它只是复制当前数组，并返回副本。如果传递给concat()方法的是一个或多个数组，则该方法会将这些数组中的每一项添加到结果数组中。如果出传递的不是数组，这些值就会被简单地添加到结果数组的末尾。
+ slice():基于当前数组中的一个或多个项创建一个新数组。slice()方法可以接收一个或两个参数，既要返回项的起始和结束位置。在只有一个参数的情况下，slice()方法返回从该参数指定位置开始 到当前数组末尾的所有项。如果有两个参数，该方法返回起始和结束位置之间的项，但不包括结束位置的项。
+ splice():有多种用途
    * 删除:可以删除任意数量的项，只需指定两个参数：要删除的第一项的位置和删除项的个数
    * 插入：可以指定位置插入任意数量的项，只需提供3个参数：起始位置、0(要删除的项数)和要插入的项
    * 替换:可以向指定的位置插入任意数量的项，且同时删除任意数量的项，只需指定3个参数：起始位置、要删除的项数和要插入的任意数量的项

### 位置方法
es5提供了两个位置方法,indexOf()和lastIndexOf()。这两个方法都接收了两个参数，要查找的项和（可选的）表示查找起点位置的索引。其中,indexOf()方法从数组的开头(位置0)开始向后查找，lastIndexOf()方法则从数组的末尾开始向前查找，这两个方法都返回要查找的项在数组中的位置，或者在没有找到的情况下返回-1。在比较第一个参数与数组中的每一项时，会使用全等操作符
