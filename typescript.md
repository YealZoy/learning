# 安装typescript
npm install -g typescript
此时会安装typescript，并且会将tsc命令添加到系统的环境变量中

# 编译代码
tsc greeter.ts
其结果是得到一个包含相同的代码greeter.js。

# 基础类型
## 布尔值
```javascript
let isDone:boolean = false;
```

## 数字
```javascript
let decLiteral: number = 6;
let hexLiteral: number = 0xf00d;
let binaryLiteral: number = 0b1010;
let octalLiteral: number = 0o744;
```

## 字符串
```javascript
let name:string = 'bob';
name="smith"
```

还可以用 *模版字符串*，可以定义多行文本和内嵌表达式。这种字符串是被反引号包围（`\``）



