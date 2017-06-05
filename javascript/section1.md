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

# <script>元素
