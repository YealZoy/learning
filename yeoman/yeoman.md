# yeoman安装
`npm install -g yo`

# 组织自己的生成器
+ 创建一个文件夹，文件夹的名字是`generator-name` （name是你的生成器）
+ 在生成器的文件夹里创建`package.json`文件,其中`name`的属性为`generator-`，`keywords`属性必须是`yeoman-generator`，`files`属性是个数组字符串，值为文件夹目录，项目必须依赖`yeoman-generator`
```javascript
{
  "name": "generator-bksx",
  "version": "1.0.0",
  "description": "北控三兴web前端生成器",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [
    "yeoman-generator"
  ],
  "repository": {
    "type": "git",
    "url": "https://github.com/YealZoy/generator-bksx.git"
  },
  "author": "郑玉燕",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/YealZoy/generator-bksx/issues"
  },
  "homepage": "https://github.com/YealZoy/generator-bksx#readme",
  "dependencies": {
    "yeoman-generator": "^1.0.0"
  }
}

```

# 文件夹结构
+ 当调用`yo name`命令时，默认调用的是app生成器，对于的逻辑位置放在`/app`文件夹下
+ 当调用`yo name:subcommond`命令时,必须要有对于的`subcommond/`文件夹

如果文件结构如下，则该生成器暴露`yo name`和`yo name:router`两个命令
```
├───package.json
├───app/
│   └───index.js
└───router/
    └───index.js
```

如果你不想把所有的代码放在跟目录下,Yeoman提供了另外的一种方式：可以放在`generators/`目录下
```
├───package.json
└───generators/
    ├───app/
    │   └───index.js
    └───router/
        └───index.js
```

# 继承generator
结构写好了，需要开始写实际的逻辑代码   

Yeoman提供了基础生成器供你继承，这些基础生成器提供了很多方便的方法供你调用。
基本写法
```javascript
var generators = require('yeoman-generator');
module.exports = generators.Base.extend();
```
如果你的生成器需要name参数（比如yo name:router foo中的foo），想将它赋给this.name的话：
```javascript
var generators = require('yeoman-generator');
module.exports = generators.NamedBase.extend();
```

> 上面两种方式都能用于创建app生成器或者子生成器，Base多用于app生成器，NamedBase多用于需要指定文件名的子生成器
