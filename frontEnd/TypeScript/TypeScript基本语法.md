```
npm install typescirpt -g

tsc  intes.ts

tsc --init 

vscode -> 终端 -> 运行任务 -> typescript -> tsc watch
```

[TOC]

## 1：typescript中的数据类型：

### 1.1 布尔类型：boolean

`var flag:boolean = true`

### 1.2 数字类型

```
let num:numer = 123

let decLiteral: number = 6;
let hexListeral: number = 0xf00d;
let binaryLiteral: number = 0b1010;
let octalLiteral: number = 0o744;
```

### 1.3 字符串类型

```
let str:string = '123'
let name: string = "bbb";
```

### 1.4 数组类型 

```
let arr:Array<number> = [1,2,3]

let list: number[] = [1,2,3]
let list: Array<number? = [1,2,3]
```

### 1.5 元组类型

```
let x: [string, number];
x = ['hello', 10] √
x = [10, 'hello'] ×
```

### 1.6 枚举类型

```
enum Color{red, green, blue}
let c: Color = Color.Blue
```

### 1.7 任意类型

```
let x:any = 1
```

### 1.7 null和undefined

### 1.8 void 类型

### 1.9 never类型

```
let x: never;
let y: number;

// 编译错误，数字类型不能转为 never 类型
x = 123;

// 运行正确，never 类型可以赋值给 never类型
x = (()=>{ throw new Error('exception')})();

// 运行正确，never 类型可以赋值给 数字类型
y = (()=>{ throw new Error('exception')})();

// 返回值为 never 的函数可以是抛出异常的情况
function error(message: string): never {
    throw new Error(message);
}

// 返回值为 never 的函数可以是无法被执行到的终止点的情况
function loop(): never {
  while (true) {}
}
```



### 2.0 运算符

算术运算符

```
+ - * / % ++ --
```

关系运算符

```
==   !=  >   <   >=  <=
```

逻辑运算符

```
&&  ||  !
```

位运算符

```
&  |  ~   <<  >>   >>>
```

赋值运算符

```
+= -+ *= /= =
```

三元运算符

```
? :
```

类型运算符

```
typeof，  instanceof
```

其他运算符

```
// 负号运算符
-x
// 连接运算符
+ 
```

### 3.0 条件语句

```
if else if else swtich
```

### 4.0 循环

for循环

```
for(let i; i< 10; i++) {}
```

for...in循环	，用于一组值得集合或者列表进行迭代输出

```
for(let i in list) {}

for(let j in "a b c"){}
```

for...of ,  forEach , every, some循环

```
for(let item of arr){}

list.every((val, idex, arr) => {})
```

while循环

```
while(true) {}
```

do...while() 

请注意，条件表达式出现在循环的尾部，所以循环中的 statement(s) 会在条件被测试之前至少执行一次。

```
do { } while(true)
```

break语句

continue语句

无限循环

```
for(;;){} 
while(true){}
```

### 5.0 函数

函数是一组一起执行一个任务的语句。

```
// 函数返回值
function add():string {}
// 带参数函数

// 可选参数
// 可选参数必须跟在必需参数后面。 如果上例我们想让 firstName 是可选的，lastName 必// // 选，那么就要调整它们的位置，把 firstName 放在后面。如果都是可选参数就没关系
function build(first: string, last?: string) {}

// 默认参数
function discount(price:number, rate:number = 0.5) {}

// 剩余参数
// 有一种情况，我们不知道要向函数传入多少个参数，这时候我们就可以使用剩余参数来定义。
// 剩余参数语法允许我们将一个不确定数量的参数作为一个数组传入。
function buildName(first:string, ...restParam:string[]) {
	return firstName + " " + restOfName.join(" ");
}
let buildName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");

// 匿名函数
var res = function([arguments]) {}
var res1 = function(a:number, b:number){}

//匿名函数自调用
(function(){})()

// 构造函数
// TypeScript 也支持使用 JavaScript 内置的构造函数 Function() 来定义函数：
// 参数说明：
// arg1, arg2, ... argN：参数列表。
// functionBody：一个含有包括函数定义的 JavaScript 语句的字符串。
var res = new Function(arg1[,arg2[, ...argN],] functionBody)
var myFunction = new Function("a", "b", "return a * b"); 

// 递归函数
// 递归函数即在函数内调用函数本身。
function factorial(number) {
    if (number <= 0) {         // 停止执行
        return 1; 
    } else {     
        return (number * factorial(number - 1));     // 调用自身
    } 
}; 

// Lambda 函数
// Lambda 函数也称之为箭头函数。
(x:number) => {}

// 函数重载
// 重载是方法名字相同，而参数不同，返回类型可以相同也可以不同。
// 每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。
function disp(string):void;
function disp(number):void;
// 如果参数类型不同，则参数类型应设置为 any。
// 参数数量不同你可以将不同的参数设置为可选。
```



### 6.0 Number

```
Number.MAX_VALUE
Number.MIN_VALUE
Number.NEGATIVE_INFInITY
Number.POSITIVE_INFINITY
Number.NAN

var num = 1234;
num.toExponential()
num.toFixed()
num.toLocalString()
num.toPercision()
num.toString()
num.valueOf()
```

toLocaleString() 与 toString() 的区别：

**1.toLocaleString()，当数字是四位数及以上时，从右往左数，每三位用分号隔开，并且小数点后只保留三位；而toString()单纯将数字转换为字符串。**

**2.toLocaleString()，当目标是标准时间格式时，输出简洁年月日，时分秒；而toString()输出国际表述字符串。**

```
var num = new Number(1777.123488); 
console.log(num.toLocaleString());  // 输出：1,777.123
console.log(num.toString());  // 输出：1777.123488

var dateStr = new Date();
console.log(dateStr.toLocaleString());  // 输出：2022/2/15 16:48:35
console.log(dateStr.toString());  // 输出：Tue Feb 15 2022 16:48:58 GMT+0800 (中国标准时间)
```



### 7.0 String

```
var str = new String("this is string")
// string对象属性
str.constructor
str.length
str.prototype.emial = function() {}
// string对象方法
str.charAt(0)
str.charAt(1)
str.charCodeAt(0)
str.concat()
str.indexOf()
str.lastIndexOf()
str.localeCompare() // 用本地特定的顺序来比较两个字符串。
str.match() // 查找找到一个或多个正则表达式的匹配。
str.replace() // "zara ali".replace(/(\w+)\s(\w+)/, "$2, $1");  => ali, zara
str.search() // 检索与正则表达式相匹配的值
str.slice() // 提取字符串的片断，并在新的字符串中返回被提取的部分。
str.split() 
str.substr()  // 从起始索引号提取字符串中指定数目的字符。
str.substring() // 提取字符串中两个指定的索引号之间的字符。
str.toLocaleLowerCase() // 根据主机的语言环境把字符串转换为小写，只有几种语言（如土耳其语）具有地方特有的大小写映射。
str.toLocaleUpperCase()
str.toLowerCase() //把字符串转换为小写
str.string()
str.toUpperCase() // 把字符串转换为大写。
str.valueOf() // 返回指定字符串对象的原始值。
```

​	

### 8.0 Array数组

```
var sites:string[] = ["d", "c", "df"]
var arr:number[] = new Array(4)
//数组解构
var ar:number = [2,3]
var [x, y] = ar;

// 数组迭代
// 我们可以使用 for 语句来循环输出数组的各个元素：

// 多维数组
一个数组的元素可以是另外一个数组，这样就构成了多维数组（Multi-dimensional Array）。
var arry:number[][] = [1,2,3][11,22,33]

// 数组在函数中的使用
// 作为参数传递给函数
// 作为函数的返回值
// 数组方法
arr.concat()
arr.splice()
arr.slice() // 选取数组的的一部分，并返回一个新数组。
arr.push()
arr.pop()
arr.shift()
arr.unshift()
arr.split()
arr.filter()
arr.find() // 检测数值元素，并返回符合条件所有元素的数组。
arr.every() // 检测数值元素的每个元素是否都符合条件。
arr.some() // 检测数组元素中是否有元素符合指定条件
arr.forEach()
arr.indexOf() // 搜索数组中的元素，并返回它所在的位置。如果搜索不到，返回值 -1，代表没有此项。
arr.join()
arr.lastIndexOf() // 返回一个指定的字符串值最后出现的位置，在一个字符串中的指定位置从后向前搜索。
arr.map()
arr.reduce() // 将数组元素计算为一个值（从左到右）。
arr.reduceRight() // 将数组元素计算为一个值（从右到左）。	
arr.reverse()
arr.sort() // 对数组的元素进行排序。
arr.toString() // 把数组转换为字符串，并返回结果。
```

### 9.0 Map对象

```
let map = new Map()
// 初始化 Map，可以以数组的格式来传入键值对：
let arrMap = new Map([['key1', 'value1'], ['key2', 'value2']])

map.clear() – 移除 Map 对象的所有键/值对 。
map.set() – 设置键值对，返回该 Map 对象。
map.get() – 返回键对应的值，如果不存在，则返回 undefined。
map.has() – 返回一个布尔值，用于判断 Map 中是否包含键对应的值。
map.delete() – 删除 Map 中的元素，删除成功返回 true，失败返回 false。
map.size – 返回 Map 对象键/值对的数量。
map.keys() - 返回一个 Iterator 对象， 包含了 Map 对象中每个元素的键 。
map.values() – 返回一个新的Iterator对象，包含了Map对象中每个元素的值 。

// 迭代 Map
// Map 对象中的元素是按顺序插入的，我们可以迭代 Map 对象，每一次迭代返回 [key, value] 数组。

TypeScript使用 for...of 来实现迭代：
let nameSiteMapping = new Map();
 
nameSiteMapping.set("Google", 1);
nameSiteMapping.set("Runoob", 2);
nameSiteMapping.set("Taobao", 3);
 
// 迭代 Map 中的 key
for (let key of nameSiteMapping.keys()) {
    console.log(key);                  
}
 
// 迭代 Map 中的 value
for (let value of nameSiteMapping.values()) {
    console.log(value);                 
}
 
// 迭代 Map 中的 key => value
for (let entry of nameSiteMapping.entries()) {
    console.log(entry[0], entry[1]);   
}
 
// 使用对象解析
for (let [key, value] of nameSiteMapping) {
    console.log(key, value);            
}
```



### 10.0元组

我们知道数组中元素的数据类型都一般是相同的（any[] 类型的数组可以不同），如果存储的元素数据类型不同，则需要使用元组。

元组中允许存储不同类型的元素，元组可以作为参数传递给函数。

创建元组的语法格式如下

var tuple_name = [value1,value2,value3,…value n]

// 访问元组
元组中元素使用索引来访问，第一个元素的索引值为 0，第二个为 1，以此类推第 n 个为 n-1，语法格式如下:tuple_name[index]

// 元组运算
我们可以使用以下两个函数向元组添加新元素或者删除元素：
push() 向元组添加元素，添加在最后面。
pop() 从元组中移除元素（最后一个），并返回移除的元素。

// 更新元组
元组是可变的，这意味着我们可以对元组进行更新操作：

```
var mytuple = [10, "Runoob", "Taobao", "Google"]; // 创建一个元组
console.log("元组的第一个元素为：" + mytuple[0]) 
 
// 更新元组元素
mytuple[0] = 121     
console.log("元组中的第一个元素更新为："+ mytuple[0])
```

// 解构元组
我们也可以把元组元素赋值给变量，如下所示：

```
var a =[10,"Runoob"] 
var [b,c] = a 
console.log( b )    
console.log( c )
```

### 11 联合类型

联合类型（Union Types）可以通过管道(|)将变量设置多种类型，赋值时可以根据设置的类型来赋值。

**注意**：只能赋值指定的类型，如果赋值其它类型就会报错。

```
var val:string|number 
val = 12 
console.log("数字为 "+ val) 
val = "Runoob" 
console.log("字符串为 " + val)

// 也可以将联合类型作为函数参数使用：
function disp(name:string|string[]) { 
        if(typeof name == "string") { 
                console.log(name) 
        } else { 
                var i; 
                for(i = 0;i<name.length;i++) { 
                console.log(name[i])
                } 
        } 
} 
disp("Runoob") 
console.log("输出数组....") 
disp(["Runoob","Google","Taobao","Facebook"])

// 联合类型数组
var arr:number[]|string[]; 
var i:number; 
arr = [1,2,4] 
console.log("**数字数组**")  
 
for(i = 0;i<arr.length;i++) { 
   console.log(arr[i]) 
}  
 
arr = ["Runoob","Google","Taobao"] 
console.log("**字符串数组**")  
 
for(i = 0;i<arr.length;i++) { 
   console.log(arr[i]) 
}

```



### 12 接口

接口是一系列抽象方法的声明，是一些方法特征的集合，这些方法都应该是抽象的，需要由具体的类去实现，然后第三方就可以通过这组抽象方法调用，让具体的类执行具体的方法。

TypeScript 接口定义如下：

```

接口中我们可以将数组的索引值和元素设置为不同类型，索引值可以是数字或字符串。interface interface_name { 
}

// 以下实例中，我们定义了一个接口 IPerson，接着定义了一个变量 customer，它的类型是 IPerson。customer 实现了接口 IPerson 的属性和方法。
interface IPerson { 
    firstName:string, 
    lastName:string, 
    sayHi: ()=>string 
} 
 
var customer:IPerson = { 
    firstName:"Tom",
    lastName:"Hanks", 
    sayHi: ():string =>{return "Hi there"} 
} 

// 需要注意接口不能转换为 JavaScript。 它只是 TypeScript 的一部分。

// 联合类型和接口
interface RunOptions { 
    program:string; 
    commandline:string[]|string|(()=>string); 
} 
 
// commandline 是字符串
var options:RunOptions = {program:"test1",commandline:"Hello"}; 
console.log(options.commandline)  
 
// commandline 是字符串数组
options = {program:"test1",commandline:["Hello","World"]}; 
console.log(options.commandline[0]); 
console.log(options.commandline[1]);  
 
// commandline 是一个函数表达式
options = {program:"test1",commandline:()=>{return "**Hello World**";}}; 
 
var fn:any = options.commandline; 
console.log(fn());


// 接口和数组
// 接口中我们可以将数组的索引值和元素设置为不同类型，索引值可以是数字或字符串。

// 设置元素为字符串类型：
interface namelist { 
   [index:number]:string 
} 
// var list2:namelist = ["Google","Runoob","Taobao"]

```

接口继承
接口继承就是说接口可以通过其他接口来扩展自己。Typescript 允许接口继承多个接口。继承使用关键字 extends。

单接口继承语法格式：

```
Child_interface_name extends super_interface_name
```

多接口继承语法格式：继承的各个接口使用逗号 **,** 分隔。

```
Child_interface_name extends super_interface1_name, super_interface2_name,…,super_interfaceN_name
```



### 13类

TypeScript 是面向对象的 JavaScript。

类描述了所创建的对象共同的属性和方法。

TypeScript 支持面向对象的所有特性，比如 类、接口等。

TypeScript 类定义方式如下：

```
class class_name { 
    // 类作用域
}
```

定义类的关键字为 class，后面紧跟类名，类可以包含以下几个模块（类的数据成员）：

- **字段** − 字段是类里面声明的变量。字段表示对象的有关数据。
- **构造函数** − 类实例化时调用，可以为类的对象分配内存。
- **方法** − 方法为对象要执行的操作。

**创建类的数据成员**

以下实例我们声明了类 Car，包含字段为 engine，构造函数在类实例化后初始化字段 engine。

this 关键字表示当前类实例化的对象。注意构造函数的参数名与字段名相同，this.engine 表示类的字段。

**创建实例化对象**

```
var object_name = new class_name([ arguments ])

// 类实例化时会调用构造函数，例如：
var obj = new Car("Engine 1")
```

**类的继承**

TypeScript 支持继承类，即我们可以在创建类的时候继承一个已存在的类，这个已存在的类称为父类，继承它的类称为子类。

类继承使用关键字 **extends**，子类除了不能继承父类的私有成员(方法和属性)和构造函数，其他的都可以继承。

**TypeScript 一次只能继承一个类，不支持继承多个类，但 TypeScript 支持多重继承（A 继承 B，B 继承 C）。**

```
// 需要注意的是子类只能继承一个父类，TypeScript 不支持继承多个类，但支持多重继承，如下实例：

TypeScript
class Root { 
   str:string; 
} 
 
class Child extends Root {} 
class Leaf extends Child {} // 多重继承，继承了 Child 和 Root 类
 
var obj = new Leaf(); 
obj.str ="hello" 
console.log(obj.str)
```

**继承类的方法重写**

类继承后，子类可以对父类的方法重新定义，这个过程称之为方法的重写。

其中 super 关键字是对父类的直接引用，该关键字可以引用父类的属性和方法。

**static 关键字**

static 关键字用于定义类的数据成员（属性和方法）为静态的，静态成员可以直接通过类名调用。

```
class StaticMem {  
   static num:number; 
   
   static disp():void { 
      console.log("num 值为 "+ StaticMem.num) 
   } 
} 
 
StaticMem.num = 12     // 初始化静态变量
StaticMem.disp()       // 调用静态方法
```

**instanceof 运算符**

instanceof 运算符用于判断对象是否是指定的类型，如果是返回 true，否则返回 false。

```
class Person{ } 
var obj = new Person() 
var isPerson = obj instanceof Person; 
console.log("obj 对象是 Person 类实例化来的吗？ " + isPerson);
```

**访问控制修饰符**

TypeScript 中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。TypeScript 支持 3 种不同的访问权限。

- **public（默认）** : 公有，可以在任何地方被访问。
- **protected** : 受保护，可以被其自身以及其子类访问。
- **private** : 私有，只能被其定义所在的类访问。

**类和接口**

类可以实现接口，使用关键字 implements，并将 interest 字段作为类的属性使用。

```
interface ILoan { 
   interest:number 
} 
 
class AgriLoan implements ILoan { 
   interest:number 
   rebate:number 
   
   constructor(interest:number,rebate:number) { 
      this.interest = interest 
      this.rebate = rebate 
   } 
} 
 
var obj = new AgriLoan(10,1) 
console.log("利润为 : "+obj.interest+"，抽成为 : "+obj.rebate )
```



### 14 对象

对象是包含一组键值对的实例。 值可以是标量、函数、数组、对象等，如下实例：

```
var object_name = { 
    key1: "value1", // 标量
    key2: "value",  
    key3: function() {
        // 函数
    }, 
    key4:["content1", "content2"] //集合
}
```

**TypeScript 类型模板**

```
var sites = { 
   site1:"Runoob", 
   site2:"Google" 
};
// 这时如果我们想在对象中添加方法，可以做以下修改：

sites.sayHello = function(){ return "hello";}
// 如果在 TypeScript 中使用以上方式则会出现编译错误，因为Typescript 中的对象必须是特定类型的实例。

// TypeScript
var sites = {
    site1: "Runoob",
    site2: "Google",
    sayHello: function () { } // 类型模板
};
sites.sayHello = function () {
    console.log("hello " + sites.site1);
};
sites.sayHello();
```

**鸭子类型(Duck Typing)**

鸭子类型（英语：duck typing）是动态类型的一种风格，是多态(polymorphism)的一种形式。

在这种风格中，一个对象有效的语义，不是由继承自特定的类或实现特定的接口，而是由"当前方法和属性的集合"决定。

> 可以这样表述：
>
> "当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。"

在鸭子类型中，关注点在于对象的行为能做什么，而不是关注对象所属的类型。



### 15命名空间

命名空间一个最明确的目的就是解决重名问题。

命名空间定义了标识符的可见范围，一个标识符可在多个名字空间中定义，它在不同名字空间中的含义是互不相干的。这样，在一个新的名字空间中可定义任何标识符，它们不会与任何已有的标识符发生冲突，因为已有的定义都处于其他名字空间中。

TypeScript 中命名空间使用 **namespace** 来定义，语法格式如下：

```
namespace SomeNameSpaceName {    
	export interface ISomeInterfaceName {      }     
	export class SomeClassName {      }   
}
```

以上定义了一个命名空间 SomeNameSpaceName，如果我们需要在外部可以调用 SomeNameSpaceName 中的类和接口，则需要在类和接口添加 **export** 关键字。

要在另外一个命名空间调用语法格式为：

```
SomeNameSpaceName.SomeClassName;
```

如果一个命名空间在一个单独的 TypeScript 文件中，则应使用三斜杠 /// 引用它，语法格式如下：

```
/// <reference path = "SomeFileName.ts" />
```

以下实例演示了命名空间的使用，定义在不同文件中：

IShape.ts 文件代码：

```
namespace Drawing { 
    export interface IShape { 
        draw(); 
    }
}
```

Circle.ts 文件代码：

```
/// <reference path = "IShape.ts" /> 
namespace Drawing { 
    export class Circle implements IShape { 
        public draw() { 
            console.log("Circle is drawn"); 
        }  
    }
}
```

Triangle.ts 文件代码：

```
/// <reference path = "IShape.ts" /> 
namespace Drawing { 
    export class Triangle implements IShape { 
        public draw() { 
            console.log("Triangle is drawn"); 
        } 
    } 
}
```

TestShape.ts 文件代码：

```
/// <reference path = "IShape.ts" />   
/// <reference path = "Circle.ts" /> 
/// <reference path = "Triangle.ts" />  
function drawAllShapes(shape:Drawing.IShape) { 
    shape.draw(); 
} 
drawAllShapes(new Drawing.Circle());
drawAllShapes(new Drawing.Triangle());
```

**嵌套命名空间**

命名空间支持嵌套，即你可以将命名空间定义在另外一个命名空间里头。

```
namespace namespace_name1 { 
    export namespace namespace_name2 {
        export class class_name {    } 
    } 
}
```

成员的访问使用点号 **.** 来实现



16 模块

TypeScript 模块的设计理念是可以更换的组织代码

模块是在其自身的作用域里执行，并不是在全局作用域，这意味着定义在模块里面的变量、函数和类等在模块外部是不可见的，除非明确地使用 export 导出它们。类似地，我们必须通过 import 导入其他模块导出的变量、函数、类等。

两个模块之间的关系是通过在文件级别上使用 import 和 export 建立的。

模块使用模块加载器去导入其它的模块。 在运行时，模块加载器的作用是在执行此模块代码前去查找并执行这个模块的所有依赖。 大家最熟知的JavaScript模块加载器是服务于 Node.js 的 CommonJS 和服务于 Web 应用的 Require.js。

此外还有有 SystemJs 和 Webpack。

模块导出使用关键字 **export** 关键字，语法格式如下：

```
// 文件名 : SomeInterface.ts 
export interface SomeInterface { 
   // 代码部分
}
```

要在另外一个文件使用该模块就需要使用 **import** 关键字来导入:

```
import someInterfaceRef = require("./SomeInterface");
```

实例：

IShape.ts 文件代码：

```
/// <reference path = "IShape.ts" /> 
export interface IShape { 
   draw(); 
}
```

Circle.ts 文件代码：

```
import shape = require("./IShape"); 
export class Circle implements shape.IShape { 
   public draw() { 
      console.log("Cirlce is drawn (external module)"); 
   } 
}
```

Triangle.ts 文件代码：

```
import shape = require("./IShape"); 
export class Triangle implements shape.IShape { 
   public draw() { 
      console.log("Triangle is drawn (external module)"); 
   } 
}
```

TestShape.ts 文件代码：

```
import shape = require("./IShape"); 
import circle = require("./Circle"); 
import triangle = require("./Triangle");  
 
function drawAllShapes(shapeToDraw: shape.IShape) {
   shapeToDraw.draw(); 
} 
 
drawAllShapes(new circle.Circle()); 
drawAllShapes(new triangle.Triangle());
```



### 17声明文件

TypeScript 作为 JavaScript 的超集，在开发过程中不可避免要引用其他第三方的 JavaScript 的库。虽然通过直接引用可以调用库的类和方法，但是却无法使用TypeScript 诸如类型检查等特性功能。为了解决这个问题，需要将这些库里的函数和方法体去掉后只保留导出类型声明，而产生了一个描述 JavaScript 库和模块信息的声明文件。通过引用这个声明文件，就可以借用 TypeScript 的各种特性来使用库文件了。

但是在 TypeScript 中，我们并不知道 $ 或 jQuery 是什么东西：

需要使用 declare 关键字来定义它的类型，帮助 TypeScript 判断我们传入的参数类型对不对：

```
declare var jQuery: (selector: string) => any;

jQuery('#foo');
```

declare 定义的类型只会用于编译时的检查，编译结果中会被删除。

**声明文件**

声明文件以 **.d.ts** 为后缀，例如：

```
demo.d.ts
```

声明文件或模块的语法格式如下：

```
declare module Module_Name {
}
```

TypeScript 引入声明文件语法格式：

```
/// <reference path = " demo.d.ts" />
```

实例:

以下定义一个第三方库来演示：

```
var Runoob;  
(function(Runoob) {
    var Calc = (function () { 
        function Calc() { 
        } 
    })
    Calc.prototype.doSum = function (limit) {
        var sum = 0; 
 
        for (var i = 0; i <= limit; i++) { 
            sum = sum + i; 
        }
        return sum; 
    }
    Runoob.Calc = Calc; 
    return Calc; 
})(Runoob || (Runoob = {})); 
var test = new Runoob.Calc();
```

如果我们想在 TypeScript 中引用上面的代码，则需要设置声明文件 Calc.d.ts，代码如下：

```
declare module Runoob { 
   export class Calc { 
      doSum(limit:number) : number; 
   }
}
```

声明文件不包含实现，它只是类型声明，把声明文件加入到 TypeScript 中：

```
/// <reference path = "Calc.d.ts" /> 
var obj = new Runoob.Calc(); 
// obj.doSum("Hello"); // 编译错误
console.log(obj.doSum(10));
```



### 18 KeyOf关键字

`keyof` 是 TypeScript 中的关键字，用于从对象类型中提取键类型。

**keyof带有显式键**

当用于具有显式键的对象类型时，`keyof` 使用这些键创建联合类型。

```
interface Person {
  name: string;
  age: number;
}
// `keyof Person` 这里创建了"name"和"age"的联合类型，不允许使用其他字符串
function printPersonProperty(person: Person, property: keyof Person) {
  console.log(`Printing person property ${property}: "${person[property]}"`);
}
let person = {
  name: "Max",
  age: 27
};
printPersonProperty(person, "name"); // 打印 person 属性名称: "Max"
```

**`keyof` 带索引签名**

`keyof` 也可以与索引签名一起使用来提取索引类型。

```
type StringMap = { [key: string]: unknown };
// `keyof StringMap` 在这里解析为 `string`
function createStringPair(property: keyof StringMap, value: string): StringMap {
  return { [property]: value };
}
```

