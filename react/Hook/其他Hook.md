# 其他 Hook

## [Reducer Hook](https://react.docschina.org/docs/hooks-reference.html#usereducer)

Flux：Facebook 出品的一个数据流框架

1. 规定了数据是单向流动的
2. 数据存储在数据仓库中（目前，可以认为 state 就是一个存储数据的仓库）
3. action 是改变数据的唯一原因（本质上就是一个对象，action 有两个属性）
    1. type：字符串，动作的类型
    2. payload：任意类型，动作发生后的附加信息
    3. 例如，如果是添加一个学生，action 可以描述为：
        1. `{ type:"addStudent", payload: {学生对象的各种信息} }`
    4. 例如，如果要删除一个学生，action 可以描述为：
        1. `{ type:"deleteStudent", payload: 学生id }`
4. 具体改变数据的是一个函数，该函数叫做 reducer
    1. 该函数接收两个参数
        1. state：表示当前数据仓库中的数据
        2. action：描述了如何去改变数据，以及改变数据的一些附加信息
    2. 该函数必须有一个返回结果，用于表示数据仓库变化之后的数据
        1. Flux 要求，对象是不可变的，如果返回对象，必须创建新的对象
    3. reducer 必须是纯函数，不能有任何副作用
5. 如果要触发 reducer，不可以直接调用，而是应该调用一个辅助函数 dispatch
    1. 该函数仅接收一个参数：action
    2. 该函数会间接去调用 reducer，以达到改变数据的目的

## [Context Hook](https://react.docschina.org/docs/hooks-reference.html#usecontext)

获取上下文数据

```js
const value = useContext(MyContext);
```

接收一个 context 对象（React.createContext 的返回值）并返回该 context 的当前值。当前的 context 值由上层组件中距离当前组件最近的 <MyContext.Provider> 的 value prop 决定。

```js
import React, { useContext } from "react";

const ctx = React.createContext();

function Test() {
	const value = useContext(ctx);
	return <p>上下文数据为：{value}</p>;
}
export default function ContextHookTest() {
	return (
		<div>
			<ctx.Provider value="xyq">
				<Test />
			</ctx.Provider>
		</div>
	);
}
```

## [Callback Hook](https://react.docschina.org/docs/hooks-reference.html#usecallback)

`useCallback`

用于得到一个固定引用值的函数，通常用来进行性能优化

useCallback：

该函数有两个参数：

1. 函数，useCallback 会固定该函数的引用，只要依赖项没有发生变化，则始终返回之前函数的地址
2. 数组，记录依赖项

```js
const memoizedCallback = useCallback(() => {
	doSomething(a, b);
}, [a, b]);
```

## [Memo Hook](https://react.docschina.org/docs/hooks-reference.html#usememo)

用于保持一些比较稳定的数据，通常用于性能优化

## [Ref Hook](https://react.docschina.org/docs/hooks-reference.html#useref)

useRef:

1. 一个参数：默认值
2. 返回值：一个固定的对象，`{current:值}`， r 变更 `.current `属性不会引发组件重新渲染。

```js
import React, { useRef } from "react";

export default function RefHookTest() {
	const inputRef = useRef();
	return (
		<div>
			<input ref={inputRef} type="text" />
			<button
				onClick={() => {
					console.log(inputRef.current.value);
				}}
			>
				获取input数据
			</button>
		</div>
	);
}
```

```js
// 将useRef当成一个固定对象使用
import React, { useRef, useState, useEffect } from "react";

export default function RefHookTest() {
	const [n, setN] = useState(10);
	const nRef = useRef(n);
	useEffect(() => {
		let timer = setInterval(() => {
			setN(nRef.current - 1);
			nRef.current--;
			if (nRef.current === 0) {
				clearInterval(timer);
			}
			return () => {
				clearInterval(timer);
			};
		}, 1000);
	}, []);
	return <div>{n}</div>;
}
```

## [ImperativeHandle Hook](https://react.docschina.org/docs/hooks-reference.html#useimperativehandle)

useImperativeHandle 可以让你在使用 ref 时自定义暴露给父组件的实例值

```useImperativeHandle(ref, createHandle, [deps])```
参数一：Ref
参数二：一个函数，返回值可以通过ref获取
参数三：依赖列表，第一次运行之后，只有依赖项发生变化才会运行

index.js

```js
import React, { useImperativeHandle } from "react";

function ImperativeHandleHookTest(props, ref) {
	useImperativeHandle(ref, () => {
		return {
			method: () => {
				console.log("ImperativeHandleHookTest里面的method方法！");
			},
		};
	}),[];
	return <div>ImperativeHandleHookTest</div>;
}

export default React.forwardRef(ImperativeHandleHookTest);
```

test.js

```js
import React, { useRef } from "react";
import ImperativeHandleHookTest from "./index";

export default function Test() {
	const componentRef = useRef();
	return (
		<div>
			<ImperativeHandleHookTest ref={componentRef} />
			<button
				onClick={() => {
					componentRef.current.method();
				}}
			>
				调用ImperativeHandleHookTest里面的一个method方法
			</button>
		</div>
	);
}
```
