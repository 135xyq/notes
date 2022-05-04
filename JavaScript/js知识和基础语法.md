# js知识和基础语法  
----------
## 浏览器组成：
- shell：
- 内核（核心）：
    - 渲染引擎（语法规则和渲染）
    - js引擎
    - 其他模块

google发布的Chrome，引擎号V8（C语言），能直接将就是代码转化为机械码。

计算机中的同步和异步与现实生活中相反  
异步：同时执行（link标签的加载）  
同步：先干一件再干另一件

### JavaScript：
解释性语言:一行一行执行，不生成文件；  
单线程:同一时间只能干一件事  
ECMA标准

js执行队列：
轮转时间片

js三大部分：
ECMAScript, DOM,BOM


### 编译语言和解释语言：
- 编译（c c++ ）：     
        优点：快  
        缺点：不跨平台，移植性不好
- 解释(javascript php)：   
        优点：跨平台，移植性好
        不足：稍微慢

java既不是编译型语言，也不是解释性语言（oak语言）

| 主流浏览器 |    内核|
| :----------:| :------:|
| IE   |trident |
| Chrom | webkit / blink|
| firefox |  Gecko|
| Opera   | presto |
| Safari  | webkit|
|

### js引入：
```javaScript
<script  type="text/javaScript"></script>
<script  type="text/javaScript" src=""></script>
```

**当一个script标签既引入外部js又有内部js时内部的失效**

 javascript是面向对象语言

var  单一类型

### 数据类型： 
1. 原始值 (存储在栈中，栈与栈之间的赋值是拷贝)：Number   Boolean String undefined(未赋值的)  null(占位置)
2. 引用值（存储在堆中， ）：array object function

### 代码错误：代码错误只会影响当前代码块
1. 低级错误（语法错误）
2. 逻辑错误

赋值顺序：自右向左  
计算顺序：自左向右

NaN不等于任何数，包括自己。

undefined , null , NaN ," " , 0 , false 转为布尔值都为 false

&&运算符（假设有两个值比较）（可用作短路语句），如果第一个值为false，直接输出第一个（结束执行），否则输出第二个值 。

||运算符（假设有两个值比较）：只有两个都为假时才返回假。前一个为真时后一个条件直接忽略（不执行）

```javaScript
never - ending loop：死循环
while ("never - ending loop") {
    document.write(i);
}
```

`document.write() 可在页面中显示` 
`console.log() :控制台输出`

#### switch - case语句选择： 
case里面的类型不要求一致

continue :终止本次循环，开始下次的循环

```js
const a = 2;
switch (a) {
    case 1:
        console.log(1);
        break;
    case 2:
        console.log(2);
        break;
    case 3:
        console.log(3);
        break;
    default:
        console.log("default")
}
```

数组里面的每个元素不用类型一样  
length ：数组长度

### 对象：
```javaScript
var 对象名 = {
属性名（key）：属性值（value）,(属性之间用逗号分开)
}
```
取出：对象名.属性名

typeof(变量名)  /  typeof  变量名:返回数据的类型：
返回值有：

- number ， 
- string , 
- boolean , 
- object , 
- undefined , 
- function


数据null返回object

### 类型转换：
#### （显式类型转换）：
- Number（）：转为数字，null转为数字是0 ，undefined转为数字为NaN,  根据常识不能转为数字的显示为NaN ，true转为1 ， false转为 0 。
- parseInt （参数1）： 转为整数型 ，不能转true和false（为NaN）；parseInt （参数一，参数二）：参数一：要转换的数，参数二：将数据看成什么进制（2,10,16（取值为2 - 36））转为10进制。转换原理：直接读取数值，遇到非数值部分截断。
- parseFloat（）：转为浮点型，转换原理：直接读取数值，遇到除第一个小数点以外的非数值部分截断。
- 参数名.toString（）：转为字符串,undefined 和null 不能使用；参数名.toString（参数1）：参数1 是进制，将参数转为目标进制。
- String（）：转为字符串。
- Boolean（）：转为布尔类型。
- toFixed（参数值）：保留 参数值位 小数

#### （隐式类型转换）：
- isNaN（）：判断是否为NaN ，先调用Number（），再调用此方法。
- ++ / -- / + / -  :先调用Number（），再计算，（都变成数字类型）。
- \+ :当两端有一个为字符串时，调用String（）,
-  \*\/ % / / - :先调用Number（），再计算，（都变成数字类型）。
- \> / < / >= <= :转为其他的类型
- == / != :转为其他的类型（null == undefined 结果为true  ，NaN == NaN 结果为false）。

- ===  / !==： 不发生类型转换的判断，直观判断左右是否相等。（NaN=== NaN 结果为false）。

当一个变量未定义就使用时只有调用typeof(变量) （显示为undefined）不会报错，其他情况都报错。

alert() :网页弹出框

## 函数

高内聚，低耦合。

解释性语言输出不了地址。

### 定义方法：
1. 函数声明
```javaScript
function 函数名（）{
	函数体
}
```

2. 命名函数表达式
```javaScript
var 函数名 = function 函数名{
	函数体
}
```
3. 匿名函数表达式（函数表达式）
```javaScript
var 函数名 = function {
	函数体
}

```

##### 调用方法：
`函数名（）;`  
`函数名（参数，参数）：参数不需要指明类型。`

定义函数的参数不要求与使用函数时传递的参数一样多，从前到后依次传，多的部分舍弃。

每个函数里面都有一个 arguments(类似于数组，参数列表，用来存放传递过来的实参，可以当成正常数组使用)。
当形参比实参多时：arguments 和 形参 多出来的部分不再满足映射（两个同时变化）。  
可以通过 函数名.length  来求出形参的个数。

```javascript
function w(x, y) {
    // document.write("a" + "<br>");
    // document.write("xyq" + "<br>");
    // document.write(x + y);
    arguments[2] = 4;
    console.log(arguments);
}
w(1, 2, 3);
```

return 函数返回值。

```javascript
银行金额输出：
        var n = window.prompt("input");
        function transform(number) {
            switch (number) {
                case '1':
                    return '壹';
                case '2':
                    return '贰';
                case '3':
                    return '叁';
                case '4':
                    return '肆';
                case '5':
                    return '伍';
                case '6':
                    return '陆';
                case '7':
                    return '柒';
                case '8':
                    return '捌';
                case '9':
                    return '玖'
            }
        }
        function change(number) {
            switch (number) {
                case 2:
                    return '拾';
                case 3:
                    return '佰';
                case 4:
                    return '仟';
                case 5:
                    return '万';
                case 6:
                    return '拾万';
                case 7:
                    return '佰万';
                case 8:
                    return '千万';
                case 9:
                    return '亿';
                case 1:
                    return;
            }
        }
        function write(n) {
            var i;
            var result = "";
            for (i = 0; i < n.length; i++) {
                if (n[i] == '0') {
                    continue;
                } else {
                    result += transform(n[i]);
                    if (n.length - i > 1) {
                        result += change(n.length - i);
                    }
                }
            }
            result += '元整';
            return result;
        }
        console.log(write(n));
```

### 递归(规律：先执行的最后执行完)：
1. 找规律
2. 找出口

函数变量作用域：里层可以访问外层，外层不能访问里层


#### js执行三部曲：
- 语法分析
- 预编译
- 解释执行

#### 预编译的结果：
- 函数声明整体提升
- 变量  声明提升（只是声明了变量，不能使用里面的值）

imply global暗示全局变量：即任何变量，如果变量未经声明就赋值，此变量就为全局对象所有。  
全局对象（window)  
一切声明的全局变量，全是window 的属性，即 var a = 123  =====>  window.a =123;  
window就是全局

### 全局的预编译过程：
1. 创建GO对象（全局的执行期上下文） GO === window
2. 找形参和变量声明，将变量和形参名作为GO属性名，值为undefined 。 
3. 在函数体里面找函数声明（函数表达式不行），值赋予函数体 

### 函数体里的预编译过程：（预编译发生在函数执行的前一刻）
1. 创建AO对象（执行期上下文）
2. 找形参和变量声明，将变量和形参名作为AO属性名，值为undefined。 
3. 将实参值与形参统一  
4. 在函数体里面找函数声明（函数表达式不行），值赋予函数体 
```javaScript
function fn(a) {
    console.log(a);
    var a = 123;
    console.log(a);
    function a() {}
    console.log(a);
    var b = function() {}
    console.log(b);
    function d() {}
}
fn(1);
输出：
ƒ a() {}
123
123
ƒ () {}

function test(a, b) {
    console.log(a);
    c = 0;
    var c;
    a = 3;
    b = 2;
    console.log(b);
    function b() {}
    function d() {}
    console.log(b);
}
test(1);
答案
1
2
2
```
函数可以看成特殊的对象 

### 函数里面的属性：
#### 可访问的：
- name 
- prototype
#### 不可访问的（隐式属性）：
- [[scope]] :存放作用域

但凡内部的函数保存到外部，一定生成了闭包。  
闭包会导致作用链不释放，造成内存泄漏。

### 匿名函数
针对初始化功能的函数（立即执行函数）：  
执行完一次就销毁，其他和普通函数一样。

#### 普通的
```javaScript
(function() {
	函数体
}())
```
#### 带参数的
```javaScript
(function(形参) {
	函数体
}(实参))
```
#### 带返回值的
```javaScript
var 变量名 = (function() {
	函数体
}());
```

只有表达式才能被执行符号执行。  
被执行符号执行的函数名字会被直接放弃（丢弃），相当于变成了立即执行函数。


嵌套函数将内部函数保存到外部，一定会生成闭包，保存到外部的函数可以调用原来所处位置的变量。

多个函数和一个函数形成闭包，则多个函数的变量共用。

函数不执行（只定义）就不会运行函数内部的语句，什么时候执行函数，函数再运行内部语句。

```javaScript
var num = 100;
function test() {
    console.log(num);
}
num = 200;
test();
输出200
```
### ， 也可以作为运算符，返回后面的计算值。
例：
```javaScript
var a = (1 -1 , 1 + 1);

a 的值为2
```
```javaScript
var f = (
    function f() {
        return "1";
    },
    function g() {
        return 2;
    }
)();
console.log(typeof f);
输出值为 number
```
```javaScript
 var x = 1;
 if (function f() {}) { //立即执行函数
     x += typeof f;
 }
console.log(x);
输出 ： 1undefined

```

## 对象

### 对象创建方法：
1. plainObject   对象字面量 / 对象直接量  
每个属性之间用 ， 分隔开
```javaScript
var 对象名 = {
    属性名 ： 属性值，
    方法名 ： function(){
          this.属性名; //调用属性  
    }
}
```
2. 构造函数
    1. 系统自带的构造函数  Object()
    可以增，删，查，改 ，属性和方法
    `var 对象名 = new Object();`
    2. 自定义(函数名使用大驼峰 （首字母全大写）)
```javaScript
function 函数名(参数){
    this.属性名 = 属性值;
    this.方法名 = function(){
   }
}
var 对象名 = new 函数名(参数);
```
 例：
```javaScript
function Car() {
    this.name = "BMW";
    this.height = "1400";
    this.lang = "49000";
    this.run = function() {
          console.log("I am Running!")
     }
}
var car = new Car();
```

### 构造函数内部原理：
1. 在函数体最前面隐式的加上this = {}
2. 执行this.xxx = xxx
3. 隐式的返回this

当构造函数返回一个引用值类型时，使用new创建会得到返回的对象。

当一个对象的属性未定义就使用不会报错，会返回undefined。

对象属性使用：
对象名. 属性名  / 对象名. 方法名

this 第一人称可以用来指代对象。

#### 给对象增加属性和方法：
对象名.属性名 = "属性值" / 对象名. 方法名 = function() { }

#### 给对象改变属性和方法：
对象名.属性名 = "属性值" / 对象名. 方法名 = function() { }

#### 删除对象属性和方法：
delete 对象名.属性名    /    delete  对象名. 方法名 


#### 原始值类型的变量没有属性和方法。

### 包装类：
创建一个数字型对象（可以有方法和属性）  
var 对象名 = new Number(数字);

例：
```javaScript
var num = new Number(123);
//创建一个字符串型对象（可以有方法和属性）
var  对象名 = new String(字符串);
```
例：
```javaScript
var str = new String('abc');
//创建一个布尔型对象（可以有方法和属性）
var 对象名 = new Strng(布尔类型);
```
例：  
```javascript
var bool = new Boolean(true);
```

想操作原始值属性，系统会自动将其包装为对象，再删除对象。

## 原型： 
用法：函数名.prototype.属性名 = 属性值；  
function对象的一个属性，他定义了构造函数制造出的对象的公共祖先。通过该构造函数产生的对象，可以继承该原型的属性和方法，原型也是对象（可以按照对象操作）。
利用原型特点和概念，可以提取共有属性。

```javaScript
Car.prototype.height = "1400";
Car.prototype.lang = "49000";
function Car(name) {
    this.name = name;
    this.run = function() {
        console.log("I am Running!")
    }
}
var car = new Car("BWM");
var car1 = new Car("AoDi");
```
#### 不能通过对象修改原型。  
函数名.prototype.属性 = 属性值;//修改属性

delete 函数名.prototype.属性;  //删除

例：
```javaScript
delete Car.prototype.height;
```

对象名.constructor；   可以找出对象的构造函数。

charCodeAt()  方法可找出字符串的每一位。
```javaScript
Person.prototype.name = 'xyq';
	function Person() {
}
var person = new Person();
Person.prototype.name = 'hsz';
console.log(person.name);
输出为 hsz

Person.prototype.name = 'xyq';
function Person() {
}
var person = new Person();
// Person.prototype.name = 'hsz';
Person.prototype = {
    name: 'hsz'
}
console.log(person.name);
输出为xyq
会重新创建一个对象，更改地址了
```

#### 绝大多数对象最终都继承自Object.prototype
```javaScript
var obj = Object.create(null);
可以创建一个没有继承Object的对象
```
```javaScript
Math.floor(number) ;  向下取整（舍弃小数部分）
Math.ceil(number); 向上取整（整数部分加一）
```

可正常计算的范围：小数点前16位 ，后16位

### call / apply方法 ：
改变this的指向（可以借别人的方法来封装自己的功能）
#### call需要把实参按照形参的个数传进去，apply只能传一个arguments(数组)
```javaScript
function Person(name, age) {
    this.name = name;
    this.age = age;
}
var person = new Person('XYQ', 21);
var obj = {}
Person.call(obj, 'xyq', 21);

obj会变成{name: "xyq", age: "21"}


function Person(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
}
function Student(name, age, sex, tel, grade) {
    Person.call(this, name, age, sex);
    this.tel = tel;
    this.grade = grade;
}

可以生成Student函数有（name, age, sex, tel, grade）属性

function Person(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
}
function Student(name, age, sex, tel, grade) {
    Person.apply(this, [name, age, sex]);
    this.tel = tel;
    this.grade = grade;
}

可以生成Student函数有（name, age, sex, tel, grade）属性

```





