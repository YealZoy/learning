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
## 可选属性
```javascript
interface squareConfig{
    color?:string;
    width?:number;
}
```

## 只读属性
```javascript
interface Point{
    readonly x:number;
    readonly y:number;
}
```

# 类
```javascript
class Greeter {
    greeting: string;
    constructor(message: string) {
        this.greeting = message;
    }
    greet() {
        return "Hello, " + this.greeting;
    }
}

let greeter = new Greeter("world");
```

## 继承
```javascript
class Animal {
    name:string;
    constructor(theName: string) { this.name = theName; }
    move(distanceInMeters: number = 0) {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }
}

class Snake extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 5) {
        console.log("Slithering...");
        super.move(distanceInMeters);
    }
}

class Horse extends Animal {
    constructor(name: string) { super(name); }
    move(distanceInMeters = 45) {
        console.log("Galloping...");
        super.move(distanceInMeters);
    }
}

let sam = new Snake("Sammy the Python");
let tom: Animal = new Horse("Tommy the Palomino");

sam.move();
tom.move(34);
```

## 修饰符
### public
TypeScript里，成员都默认为 public。
```javascript
class Animal {
    public name: string;
    public constructor(theName: string) { this.name = theName; }
    public move(distanceInMeters: number) {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }
}
```

### private
```javascript
class Animal {
    private name: string;
    constructor(theName: string) { this.name = theName; }
}

new Animal("Cat").name; // Error: 'name' is private;
```

### protected
`protected`修饰符与`private`修饰符的行为很相似，但有一点不同，`protected`成员在派生类中仍然可以访问。
```javascript
class Person {
    protected name: string;
    constructor(name: string) { this.name = name; }
}

class Employee extends Person {
    private department: string;

    constructor(name: string, department: string) {
        super(name)
        this.department = department;
    }

    public getElevatorPitch() {
        return `Hello, my name is ${this.name} and I work in ${this.department}.`;
    }
}

let howard = new Employee("Howard", "Sales");
console.log(howard.getElevatorPitch());
console.log(howard.name); // error
```

# 函数
```javascript
// Named function
function add(x, y) {
    return x + y;
}

// Anonymous function
let myAdd = function(x, y) { return x + y; };
```

## 函数类型
```javascript
function add(x: number, y: number): number {
    return x + y;
}

let myAdd = function(x: number, y: number): number { return x+y; };
```

```javascript
let myAdd: (x:number, y:number)=>number =
    function(x: number, y: number): number { return x+y; };
```

## 推断类型
```javascript
// myAdd has the full function type
let myAdd = function(x: number, y: number): number { return x + y; };

// The parameters `x` and `y` have the type number
let myAdd: (baseValue:number, increment:number) => number =
    function(x, y) { return x + y; };
```

## 可选参数和默认参数
```javascript
function buildName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}

let result1 = buildName("Bob");  // works correctly now
let result2 = buildName("Bob", "Adams", "Sr.");  // error, too many parameters
let result3 = buildName("Bob", "Adams");  // ah, just right
```

## 剩余参数
可以使用 arguments来访问所有传入的参数
```javascript
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + " " + restOfName.join(" ");
}

let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");
```

# 装饰器
在TypeScript里，当多个装饰器应用在一个声明上时会进行如下步骤的操作：
+ 由上至下依次对装饰器表达式求值。
+ 求值的结果会被当作函数，由下至上依次调用。

```javascript
function f() {
    console.log("f(): evaluated");
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("f(): called");
    }
}

function g() {
    console.log("g(): evaluated");
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("g(): called");
    }
}

class C {
    @f()
    @g()
    method() {}
}
```

在控制台里会打印出如下结果：
```javascript
f(): evaluated
g(): evaluated
g(): called
f(): called
```

