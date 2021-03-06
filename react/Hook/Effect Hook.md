# [Effect Hook](https://react.docschina.org/docs/hooks-effect.html)

Effect Hook用于在函数组件中处理副作用。

副作用：
1. Ajax请求
2. 计时器
3. 其他异步操作
4. 更改真实DOM对象
5. 本地存储
6. 其他会对外部产生影响的操作

useEffect：该函数接收一个函数作为参数，接收的函数就是需要副作用的函数。

1. 副作用函数运行时间：在页面完成真实的UI渲染之后，它的执行是异步的，不会阻塞浏览器
    - 与类组件componentDidMount和componentDidUpdate的区别：componentDidMount和componentDidUpdate更改了真实DOM，但是用户还没有看到UI更新，是同步的；useEffect中副作用函数，更改了真实DOM，并且用户看到了UI更新，是异步的。
2. 每个函数组件中可以多次使用useEffect，但不要放入循环和判断等代码块中
3. useEffect中副作用函数，可以有返回值,返回值也必须是函数，该函数叫做清理函数
    - 清理函数运行时间点：在每次运行副作用函数之前，首次渲染组件不会运行，组件被销毁时一定会运行
4. useEffect可以传递第二个参数
    - 第二个参数是一个数组
    - 数组中记录该副作用的依赖数据
    - 当该组件重新渲染后，只有依赖数据与上一次不一样时，才会执行副作用
    - 当传递依赖数据后，如果数据没有发生变化，副作用仅在第一次渲染后运行，清理函数仅在卸载组件后运行
5. 副作用函数中，如果使用了函数上下文中的变量，则由于闭包的影响，会导致副作用函数中变量不会实时变化。

```js
import React, { useState, useEffect } from "react";

export default function EffectHookTest() {
	const [n, setN] = useState(0);
    useEffect(()=>{
        document.title = `计数器  ${n}`
        return ()=>{
            console.log('清理函数：在每次运行副作用函数之前，首次渲染组件不会运行，组件被销毁时一定会运行')
        }
    },[n]);//数组记录该副作用的依赖数据,当该组件重新渲染后，只有依赖数据与上一次不一样时，才会执行副作用
	return (
		<div>
			<span>计数器：</span>
			{n}
			<button
				onClick={() => {
					setN(n + 1);
				}}
			>
				+
			</button>
		</div>
	);
}
```