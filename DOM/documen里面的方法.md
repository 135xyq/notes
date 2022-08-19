# document 里面的方法

---

document：整个页面

querySelector('选择器')：可以按 CSS 的选择器选择方式（选出一个）

```html
<div>
    <strong></strong>
</div>
<div>
    <span>
        <strong class="demo">123</strong>
    </span>
</div>
<script>
	var strong = document.querySelector("div > span strong");
</script>

<!-- 可以选择出有123的strong标签          -->
```

querySelectorAll('选择器'):可以按 CSS 的选择器选择方式（选出一组）

```html
<div>
    <strong></strong>
</div>
<div>
    <span>
        <strong class="demo">123</strong>
    </span>
</div>
<script>
	var strong = document.querySelectorAll("div > span strong");
</script>

<!-- 可以选择出有123的一组strong标签    -->
```

querySeclect 和 querySelectAll 是静态的，选择后更新DOM，选择结果不会更新（选出来的是副本）

```html
<div id="box1">
	<p>1</p>
</div>
<script>
	console.log(document.querySelectorAll("#box1 p"));
	console.log(document.getElementsByTagName("p"));
	const p = document.createElement("p");
	p.innerHTML = "2";
	box1.appendChild(p);
</script>


<!-- 输出 -->
<!--
0: p

和

0: p
1: p -->
```

### 遍历节点树：（包含所有节点）

-   parentNode:父节点
-   childNodes：子节点集合
-   firstChild：第一个子节点
-   lastChild：最后一个子节点
-   nextSibling：后一个兄弟节点
-   previousSibling：前一个兄弟节点

### 遍历元素节点树：（只有元素节点）

-   parentElement：返回当前元素的父元素节点
-   children：只返回当前元素的元素子节点
-   node.childElementCount === node.children.length：当前元素节点的子元素个数
-   firstElementChild：第一个元素节点
-   lastElementChild：最后一个元素节点
-   nextElementSibling：后一个兄弟元素节点
-   previousElementSibling：前一个兄弟元素节点

### 节点的四个属性

-   nodeName：元素的标签名，以大些形式表示，只读
-   nodeValue：Text 节点或 Comment 节点的文本内容，可读写
-   nodeType：该节点的类型，只读
-   attributes：Element 节点的属性集合

### 注意：

1. getElementById 方法定义在 Document.prototype 上，即 Element 节点上不能使用。

2. getElementsByName 方法定义在 HTMLDocument.prototype 上，即非 html 中的 document 以外不能使用(xml document,Element)

3. getElementsByTagName 方法定义在 Document.prototype 和 Element.prototype 上

4. HTMLDocument.prototype 定义了一些常用的属性，body,head,分别指代 HTML 文档中的\<body\>\<head\>标签。

5. Document.prototype 上定义了 documentElement 属性，指代文档的根元素，在 HTML 文档中，他总是指代\<html\>元素

6. getElementsByClassName、querySelectorAll、querySelector 在 Document,Element 类中均有定义

### dom 的基本操作

#### 增

```javascript
// 增加元素节点;
document.createElement();
var div = document.createElement("div");

// 增加文本节点;
document.createTextNode();
var text = document.createTextNode("hello");

// 注释节点
document.createComment();
var comment = document.createComment("This is a Comment");

// 文档碎片节点;
document.createDocumentFragment();
```

#### 插

```javascript
// PARENTNODE.appendChild();插入节点（剪切操作）
var div = document.getElementsByTagName('div')[0];
var text = document.createTextNode("这里在div中插入一个文本节点");
var span = document.createElement('span');
div.appendChild(text);
div.appendChild(span);


// PARENTNODE.insertBefore(a, b);在父集中将a插在b前面
var div = document.getElementsByTagName('div')[0];
var strong = document.getElementsByTagName('strong')[0];
var span = document.createElement('span');
div.insertBefore(span, strong);

var div = document.getElementsByTagName('div')[0];
var strong = document.getElementsByTagName('strong')[0];
var text = document.createTextNode("在strong前面插入一个文本节点");
div.insertBefore(text, strong);
```

#### 删

```javascript
// parent.removeChild();父节点调用方法删除子节点（剪切）
var div = document.getElementsByTagName('div')[0];
var strong = document.getElementsByTagName('strong')[0];
div.removeChild(strong);
// 删除div下面的strong标签

// parent.remove();子节点自己调用方法删除自己（销毁）
var strong = document.getElementsByTagName('strong')[0];
strong.remove()
// 删除div下面的strong标签

```

#### 替换

```javascript
// parent.replaceChild(new, origin);（剪切）
var div = document.getElementsByTagName('div')[0];
var strong = document.getElementsByTagName('strong')[0];
var text = document.createTextNode("将strong标签替换成为一个文本");
div.replaceChild(text, strong);
// Element节点的一些属性

// innerHTML（取写HTML）
var div = document.getElementsByTagName('div')[0];
div.innerHTML;
// 将div里面的东西查找出来

var div = document.getElementsByTagName('div')[0];
div.innerHTML = "将div原来的东西覆盖掉";
// 将div里面的东西替换

var div = document.getElementsByTagName('div')[0];
div.innerHTML = "将div原来的东西覆盖掉";
div.innerHTML += "再加一点东西！";
// 在原来的div后面再添加一点东西

// innerText（取写文本，老版本火狐不支持（提供TextContent一样））

var div = document.getElementsByTagName('div')[0];
div.innerText;
// 将div里面的文本取出来

var div = document.getElementsByTagName('div')[0];
div.innerText = "123";
// 将div里面的所有东西替换成123
```

### Element 节点的一些方法

#### ele.setAttribute() ;设置属性

```javascript
var div = document.getElementsByTagName('div')[0];
div.setAttribute('class', 'class1');
// 给div添加名为class1 的 class属性

var div = document.getElementsByTagName('div')[0];
div.setAttribute('id', 'only');
// 给div添加一个名为only的 id属性
```

#### ele.getAttribute() ;获取属性

```javascript
var div = document.getElementsByTagName("div")[0];
div.getAttribute("id");
// 获取div的id;
```

document.getElementsByTagName(\*);可以把所有标签取出来

## 日期对象

日期对象是系统提供好的。

`var date = new Date();`

setInterval(函数，时间间隔);循环执行（每隔一段时间执行函数），都会返回一个数字唯一标识

```javascript
setInterval(function () {
	console.log("aaa");
}, 1000);

// 每隔1000毫秒执行一次function;
```

setTimeout(函数，时间间隔);推迟一段时间在执行，仅执行一次

```javascript
setTimeout(function () {
	console.log("推迟1000毫秒执行，仅执行一次。");
}, 1000);
```

```javascript
// clearInterval(数字); 停止执行;

var timer = setInterval(function () {
	console.log("aaa");
}, 1000);
clearInterval(timer);
// 可以停止setInterval的执行;
```

```javascript
// clearTimeout(数字); 停止执行;

var timer = setTimeout(function () {
	console.log("隔1000毫秒执行，仅执行一次。");
}, 1000);
clearTimeout(timer);
// 清除setTimeout的执行;
```

全局对象 window 上的方法，内部函数 this 指向 window

#### 注意 ：

setInterval(“字符串”,1000);会每隔一段时间执行字符串里面的代码（当成 js 代码）

## 浏览器窗口

### 查看滚动条的滚动距离：

```window.pageXOffset/pageYOffset```
IE8 及 IE8 以下不兼容

`document.body.scrollLeft/scrollTop`
`document.documentElement.scrollLeft/scrollTop`

兼容性比较混乱，用时取两个值相加，因为不可能存在两个同时有值。

### 查看视口的尺寸：

`window.innerWidth/innerHeight`  
IE8 及 IE8 以下不兼容

`document.documentElement.clientWidth/clientHeight`

标准模式下，任意浏览器都兼容

`document.body.clientWidth/clientHeight`

适用于怪异模式下的浏览器

### 浏览器的渲染模式：

1. 标准模式：
2. 怪异模式（混扎模式）：可支持老版本，启动方法（删除\<!DOCTYPE html\>）

### 查看元素的几何尺寸:

`domEle.getBoundingClientRect();`

兼容性很好。

该方法返回一个对象，对象里面有 left,top,right,bottom 等属性。left 和 top 代表该元素左上角的 X 和 Y 坐标，right 和 bottom 代表元素右下角的 X 和 Y 坐标
height 和 width 属性。
老版本 IE 并未实现。

返回的结果并不是“实时的”。

#### 查看元素的尺寸：

`dom.offsetWidth，dom.offsetHeight`

#### 查看元素的位置：

`dom.offsetLeft, dom.offsetTop`

对于无定位父级的元素，返回相对文档的坐标。对于有定位父级的元素，返回相对于最近的有定位的父级的坐标。

`dom.offsetParent`

返回最近的有定位的父级，如无，返回 body, body.offsetParent 返回 null

### 让滚动条滚动：

window 上有三个方法

-   scroll(),
-   scrollTo(),
-   scrollBy();

三个方法功能类似，用法都是将 x,y 坐标传入。即实现让滚动轮滚动到当前位置。

区别：scrollBy()会在之前的数据基础之上做累加。

### 脚本化 CSS

`dom.style.prop（获取的是行间样式表）`

可读写行间样式，没有兼容性问题，碰到 float 这样的关键字属性，前面应加 css

`eg:float — > cssFloat`

复合属性必须拆解，组合单词变成小驼峰式写法

写入的值必须是字符串格式

查询计算样式

```javascript
// window.getComputedStyle(ele,null);（展示的值和默认值）

var div = document.getElementsByTagName('div')[0];
window.getComputedStyle(div,null);

```

计算样式只读

返回的计算样式的值都是绝对值，没有相对单位

IE8 及 IE8 以下不兼容
可以用 ```getComputedStyle（ele,伪元素名）```来获取伪元素的属性

```javascript

var div = document.getElementsByTagName("div")[0];
window.getComputedStyle(div, "after");

```

#### 查询样式

```ele.currentStyle```

- 计算样式只读
- 返回的计算样式的值不是经过转换的绝对值
- IE 独有的属性


```javascript

var div = document.getElementsByTagName("div")[0];
div.currentStyle.width;

```


元素名.className = "class 名";可以改元素的 class

### 事件：

#### 绑定事件：

1. `ele.onxxx = function (event) {}`  

兼容性很好，但是一个元素只能绑定一个处理程序

基本等同于写在 HTML 行间上。（在行间不用写 function 直接写执行语句就行）
程序 this 指向是 dom 元素本身

```javascript
var div = document.getElementsByTagName("div")[0];
div.onclick = function () {
	函数体;
};
```

2. `obj.addEventListener(事件类型, 处理函数, false);`

IE9 以下不兼容，可以为一个事件绑定多个处理程序。
程序 this 指向是 dom 元素本身

```javascript

var div = document.getElementsByTagName('div')[0];
div.addEventListener('click', function() {
    console.log("a");
}, false)
div.addEventListener('click', function() {
    console.log("b");
}, false)

```

```html
<ul>
    <li>a</li>
    <li>a</li>
    <li>a</li>
    <li>a</li>
</ul>
<script>
    var i = 0
    var lis = document.getElementsByTagName('li');
    for (i = 0; i < lis.length; i++) {
        (function(i) {
            lis[i].addEventListener('click', function() {
                console.log(i + 1);
            }, false)
        }(i))
    }
</script>
<!-- 点击每个li展示其序号（注意闭包的应用） -->
```

3. `obj.attachEvent(‘on’ + type, fn);`

IE 独有，一个事件同样可以绑定多个处理程序,IE 独有
程序 this 指向是 window

```javascript
var div = document.getElementsByTagName("div")[0];
div.attachEvent("onclick", function () {
	console.log("a");
});
```

### 解除事件处理函数

**注:若绑定匿名函数，则无法解除**

1. `ele.onclick = false/''/null;`

```javascript
var div = document.getElementsByTagName("div")[0];
div.onclick = function () {
	console.log("a");
};
div.onclick = null;
```

2. `ele.removeEventListener(type, fn, false)`;

```javascript
function f() {
	console.log("a");
}
var div = document.getElementsByTagName("div")[0];
div.addEventListener("click", f, false);
div.removeEventListener("click", f, false);

// 若为:
var div = document.getElementsByTagName("div")[0];
div.addEventListener(
	"click",
	function f() {
		console.log("a");
	},
	false
);
// 则无法解除事件绑定;
```

3. `ele.detachEvent(‘on’ + type, fn);`

```javascript
function f() {
	console.log("a");
}
var div = document.getElementsByTagName("div")[0];
div.attachEvent("onclick", f);
div.detachEvent("onclick", f);
```

### 事件处理模: 事件冒泡、捕获

一个事件只能执行一个事件模型

#### 事件冒泡：

结构上（非视觉上）嵌套关系的元素，会存在事件冒泡的功能，即同一事件，自子元素冒泡向父元素。（自底向上）（从子元素到父元素）

#### 事件捕获：

结构上（非视觉上）嵌套关系的元素，会存在事件捕获的功能，即同一事件，自父元素捕获至子元素（事件源元素）。（自顶向下）

##### 触发方式:

elem.addEventListeren('type',function(){} ,true);
IE 没有捕获事件

触发顺序，先捕获，后冒泡

focus，blur，change，submit，reset，select 等事件不冒泡

#### 取消冒泡和阻止默认事件：

##### 取消冒泡：

```event.stopPropagation();```

W3C 标准

```javascript

document.onclick = function () {
	console.log("你正在点击整个文档！");
};
var div = document.getElementsByTagName("div")[0];
div.onclick = function (e) {
	//可以加一个参数，代表当前事件的监听，是一个对象
	e.stopPropagation();
	console.log("点击div时不再冒泡！");
};
```

但不支持 ie9 以下版本

IE 独有
```event.cancelBubble = true;```

```javascript


document.onclick = function () {
	console.log("你正在点击整个文档！");
};
var div = document.getElementsByTagName("div")[0];
div.onclick = function (e) {
	// e.stopPropagation();
	e.cancelBubble = true;
	console.log("点击div时不再冒泡！");
};
```

##### 阻止默认事件:

默认事件 — 表单提交，a 标签跳转，右键菜单等

1. `return false;` 以对象属性的方式注册的事件才生效

```javascript
document.oncontextmenu = function() {
    return false;
}
// 可以阻止右键出菜单

<a href="javascript:void(false)">demo</a>
//  可以阻止a标签的跳转
```

2. `event.preventDefault();` W3C 标注，IE9 以下不兼容

```javascript
document.oncontextmenu = function (e) {
	e.preventDefault();
};
```

3. `event.returnValue = false;` 兼容 IE

```javascript
document.oncontextmenu = function (e) {
	e.returnValue = false;
};
```

#### 事件对象：

event || window.event 用于 IE  
事件源对象:
`event.target`火狐独有的

`event.srcElement` IE 独有的

这俩 chrome 都有

#### 事件委托：

利用事件冒泡，和事件源对象进行处理

##### 优点：

1. 性能 不需要循环所有的元素一个个绑定事件

2. 灵活 当有新的子元素时不需要重新绑定事件

```html
<ul>
   <li>1</li>
   <li>2</li>
   <li>3</li>
   <li>4</li>
   <li>5</li>
   <li>6</li>
   <li>7</li>
   <li>8</li>
   <li>9</li>
   <li>10</li>
</ul>
<script>
	var ul = document.getElementsByTagName('ul')[0];
    ul.onclick = function(e) {
        var event = e || window.event; //考虑事件的兼容性
        var target = event.target || event.srcElement;//考虑源事件的兼容性
        console.log(target.innerText);
    }
</script>
    <!-- 可以为所有的li添加事件，将li的事件委托给ul -->
```

#### 鼠标事件：

-   click、鼠标点击（包括按下和弹起）
-   mousedown、鼠标按下
-   mousemove、鼠标移动
-   mouseup、鼠标弹起
-   contextmenu、鼠标右键产生菜单
-   mouseover == mouseenter、鼠标进入区域
-   mouseout == mouseleave、鼠标移出区域

只有 mouseup 和 mousedown 能区分鼠标左右键
用 button 来区分鼠标的按键，0/1/2

```javascript
document.onmousedown = function (e) {
	if (e.button == 2) {
		console.log("按下的是鼠标右键！");
	} else if (e.button == 0) {
		console.log("按下的是鼠标左键!");
	} else {
		console.log("按下的是中间滚动轮!");
	}
};
```

DOM3 标准规定:click 事件只能监听左键,只能通过 mousedown 和 mouseup 来判断鼠标键

#### 键盘事件

-   keydown 按下
-   keyup 弹开
-   keypress

触发顺序：keydown > keypress > keyup

##### keydown 和 keypress 的区别

keydown 可以响应任意键盘按键(charcode 始终为 0), keypress 只可以响应字符类键盘按键(charcode 对应 ACICC 码)

keypress 返回 ASCII 码，可以转换成相应字符
操作型按键用 keydown（可以使用 which 属性）
字符型按键用 keypress

#### 文本操作事件：

-   input,只要文本有变化就触发
-   focus,聚焦时触发
-   blur,失去焦点触发
-   change，失去焦点比较前后两个状态，如果内容改变则触发，内容不变则不触发

#### 窗体操作类(window 上的事件)

-   scroll 滚动条滚动

```javascript
window.onscroll = function () {
	console.log(this.pageXOffset + " " + this.pageYOffset);
};
```

load,整个页面加载完才能触发
