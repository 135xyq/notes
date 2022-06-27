# [State Hook](https://react.docschina.org/docs/hooks-state.html)

State Hook 是一个在函数组件中使用的函数(useState),用于在函数组件中使用状态。

useState：

- 有一个参数，表示状态的默认值
- 返回值是一个数组，该数组一定包含两项
    1. 第一项：当前状态的值
    2. 第二项：改变状态的函数

一个函数组件可以有多个状态。


```js
import React, {useState} from "react";

export default function StateHookTest() {
	const [count, setCount] = useState(0);
	const [visible, setVisible] = useState(true)
	return <>
		<div style={{
			display:visible?"block":"none"
		}}>
			<button onClick={()=>{
				setCount(count-1)
			}}>-</button>
			<span>{count}</span>
			<button onClick={()=>{
				setCount(count+1)
			}}>+</button>
		</div>
		<p>
			<button onClick={()=>{
				setVisible(!visible)
			}}>切换显示/隐藏</button>
		</p>
	</>;
}
```

```js

// 多个状态合并成一个对象
import React, {useState} from "react";

export default function StateHookTest() {
	const [data, setData] = useState({count:0,visible:true});
	return <>
		<div style={{
			display:data.visible?"block":"none"
		}}>
			<button onClick={()=>{
				setData({
                    ...data,
                    count:data.count-1
                })
			}}>-</button>
			<span>{data.count}</span>
			<button onClick={()=>{
				setData({
                    ...data,
                    count:data.count+1
                })
			}}>+</button>
		</div>
		<p>
			<button onClick={()=>{
				setData({
                    ...data,
                    visible:!data.visible
                })
			}}>切换显示/隐藏</button>
		</p>
	</>;
}
```

**注意**：

1. useState最好写在函数的起始位置，便于阅读
2. useState严禁出现在代码块（判断、循环）中
3. useState返回的第二个参数（函数）的引用不变（节约内存空间）
4. 如果使用函数改变数据，若数据改变前后完全相等(使用Object.is比较)，不会导致重新渲染（优化效率）
5. 使用函数改变数据，传入的值不会和原来的数据混合，会直接替换
6. 实现强制刷新
    - 类组件：使用forceUpdate函数
    - 函数组件：使用一个空对象的useState
7. 如果某些状态之间没有必然的联系，应该分化为不同的状态，最好不要合并成一个对象
8. 函数组件中改变状态可能是异步的（在DOM事件中），多个状态会合并以提高效率，此时不能信任之前的状态，而应该使用回调函数的方式改变状态，如果状态变化要使用之前的状态，尽量传递函数

```js
import React, {useState} from "react";

export default function StateHookTest() {
	const [count, setCount] = useState(0);
	const [visible, setVisible] = useState(true)
	return <>
		<div style={{
			display:visible?"block":"none"
		}}>
			<button onClick={()=>{
                // 异步的，多个状态会合并，应该使用回调函数
				setCount(count=>count-1)
				setCount(count=>count-1)
			}}>-</button>
			<span>{count}</span>
			<button onClick={()=>{
				setCount(count=>count+1)
				setCount(count=>count+1)
			}}>+</button>
		</div>
		<p>
			<button onClick={()=>{
				setVisible(!visible)
			}}>切换显示/隐藏</button>
		</p>
	</>;
}
```