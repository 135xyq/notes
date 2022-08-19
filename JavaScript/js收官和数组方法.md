# js 数组方法

---

## label 标签

for 里面写上要关联内容的标识
添加事件时触发 label 时和 label 他关联的内容都触发，但触发内容事件时只触发自身

```html
<label for="demo">uesrname:</label> <input type="text" id="demo" />
```

## 属性和特性：

特性属于属性
特性：系统上自带的一些属性
元素的特性是与 dom 对象一 一映射的
不是特性的属性不是一 一映射的

## 图片的预加载和懒加载

### 预加载：

图片加载完之后才展现，不一行一行加载展现出来

### 懒加载：

浏览到才开始加载

## Math.random()

区间范围 ： [ 0 , 1 )

## 数组方法

### forEach ：

- 循环遍历，两个参数为一个函数（（三个参数）第一个是数组中的元素，第二个是索引，第三个是数组本身），第二个参数代表this的指向（可省略（默认为window））

- 数组名.forEach(函数（有三个参数）（第一个是数组中的元素，第二个是索引，第三个是数组本身）)；
无返回值

### filter :

- 对数组过滤，基于遍历 ，两个参数为一个函数（（三个参数）第一个是数组中的元素，第二个是索引，第三个是数组本身），第二个参数代表this的指向（可省略（默认为window））

- 执行完会返回一个新的数组。若函数的返回值为true代表当前元素保存在新数组中，为false时则过滤掉。

```js
const a = [1,2,3,4,5,6,7,8,9,10];
const b = a.filter(item=>item%2)
console.log("filter",a,b)

// 输出
// filter  [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]  [1, 3, 5, 7, 9]
```

### map :

- 映射，两个参数为一个函数（（三个参数）第一个是数组中的元素，第二个是索引，第三个是数组本身），第二个参数代表this的指向（可省略（默认为window））
- 函数执行完的返回值决定map返回的值，会返回一个新的数组

```javascript

var newArr = personArr.map(function (ele, index, self) {
	return self[index].name;
});

//可以仅返回数组中每一项中的name属性
console.log(newArr);
```


### every ：

- 数组中每元素都符合什么条件，两个参数，第一个参数为函数（（三个参数）第一个是数组中的元素，第二个是索引，第三个是数组本身）第二个参数代表this的指向（可省略（默认为window））

- 返回值为false则有元素不符合，返回值为true则所有项都符合，只有遇到有返回值为false就停止执行，返回结果为false。

**执行完会返回true或false**。

### some ：

- 数组中是否有元素都符合什么条件，两个参数，第一个参数为函数（（三个参数）第一个是数组中的元素，第二个是索引，第三个是数组本身）第二个参数代表this的指向（可省略（默认为window））

- 返回值为false则所有元素都不符合，返回值为true则至少有一个符合，只有遇到有返回值为true就停止执行，返回结果为true。
执行完会返回true或false。

### slice

可以把类数组转为数组

```js
const lis = document.getElementsByTagName("li");
const temp = [].slice.call(lis)
```
