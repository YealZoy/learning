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

# 关键字和保留字
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
