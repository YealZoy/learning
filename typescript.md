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

还可以用 *模版字符串*，可以定义多行文本和内嵌表达式。这种字符串是被反引号包围（<code>`</code>）,并且以${expro}嵌入表达式
```javascript
let name:string="Gene";
let age:number = 37;
let sentence:string = `Hello,my name is ${name}.
    I'll be ${age + 1} years old next month
`;
```

## 数组
```javascript
let list :number[] = [1,2,3];
let list2:Array<number> = [1,2,3]
```

## 元组

```javascript
let x : [string,number];
x = ['hello',1];
```

当访问一个已知索引的元素会得到正确的类型
```javascript
console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'
```

当访问一个越界的元素，会使用联合类型代替
```javascript
x[3] = 'world'; // OK, 字符串可以赋值给(string | number)类型

console.log(x[5].toString()); // OK, 'string' 和 'number' 都有 toString

x[6] = true; // Error, 布尔不是(string | number)类型
```

## 任意值
```javascript
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean  
```

## 空值
```javascript
function warnUser(): void {
    alert("This is my warning message");
}
```

声明一个void类型的变量没有什么大用，因为你只能为它赋予undefined和null：
```javascript
let unusable: void = undefined;
```

## Null和undefined
```javascript
// Not much else we can assign to these variables!
let u: undefined = undefined;
let n: null = null;
```

默认情况下`null`和`undefined`是所有类型的子类型。 就是说你可以把 `null`和`undefined`赋值给`number`类型的变量。

## Never
`never`类型表示的是那些永不存在的值的类型。

## 类型断言
类型断言有两种形式。 其一是“尖括号”语法：
```javascript
let someValue: any = "this is a string";

let strLength: number = (<string>someValue).length;
```

另一个为as语法：
```javascript
let someValue: any = "this is a string";

let strLength: number = (someValue as string).length;
```

# 变量声明
## `var`声明
## `let`声明
```javascript
let hello:string = 'world';
```
块级作用域
重定义及屏蔽

## const声明
```javascript
const numLivesForCat = 9;
```

它们与let声明相似，但是就像它的名字所表达的，它们被赋值后不能再改变

## 解构
### 解构数组
```javascript
let input = [1,2];
let [first,second] = input;
console.log(first);//1
console.log(second);//2
```

在数组里使用...语法创建剩余变量：
```javascript
let [first, ...rest] = [1, 2, 3, 4];
console.log(first); // outputs 1
console.log(rest); // outputs [ 2, 3, 4 ]
```

### 对象解构
```javascript
let o = {
    a: "foo",
    b: 12,
    c: "bar"
}
let { a, b } = o;
```

# 接口


