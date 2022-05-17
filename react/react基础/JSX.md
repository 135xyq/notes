# JSX

## 什么是 JSX

-   Facebook 起草的 JS 扩展语法
-   本质是一个 JS 对象，会被 babel 编译，最终会被转换为 React.createElement
-   每个 JSX 表达式，有且仅有一个根节点
    -   多个节点同级是可以使用 React.Fragment 或 <> 直接包裹
-   每个 JSX 元素必须结束（XML 规范）
-   类名要写成className

```JSX
const h1 = (
	<React.Fragment>
		<h1> javascript </h1>
        <p> 你好 </p>
	</React.Fragment>
);
```

```JSX
const h1 = (
	<>
		<h1> javascript </h1>
        <p> 你好 </p>
	</>
);
```

## 在 JSX 中嵌入表达式

使用 {} 包裹要放置的表达式

-   在 JSX 中使用注释: {/* 注释内容 */}
-   将表达式作为内容的一部分
    -   null、undefined、false 不会显示在页面上，结构上会存在
    -   普通对象，不可以作为子元素
    -   可以放置 React 元素对象
    -   可以放置数组（会遍历数组，将数组的每一项作为子元素添加进去）
-   将表达式作为元素属性
-   属性使用小驼峰命名法
-   防止注入攻击
    -   自动编码
    -   dangerouslySetInnerHTML:来实现类似innerHTML的功能

```JSX
const a = 1234,  b = 4321;
const h1 = (
	<React.Fragment>
		<p>
			{a}*{b} = {a * b}
		</p>
	</React.Fragment>
);
```

```jsx 
const imgClassName = "image"
const imgUrl= "http://qzapp.qlogo.cn/qzapp/101983660/F61F6EEE51E483105E9C9686BFFF61A2/100"
const h1 = (
	<React.Fragment>
		<img src={imgUrl}  className={imgClassName} alt="" style={{
			marginLeft:'50px',
			width:"220px"
		}}/>
	</React.Fragment>
);
```

```jsx

const divContent = "<h1>测试dangerouslySetInnerHTML</h1><p>必须传入一个对象，将__html属性赋值为想要展示的html字符串</p>"
const div = (
    <div dangerouslySetInnerHTML={{
        __html:divContent
    }}></div>
);
```

## 元素的不可变性

-   虽然 JSX 元素是一个对象，但是该对象中的所有属性不可更改
-   如果确实需要更改元素的属性，需要重新创建 JSX 元素
