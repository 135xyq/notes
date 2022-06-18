# 高阶组件和ref

## HOC 高阶组件


HOF:Higher-Order Function,高阶函数，以函数作为一个参数，返回一个参数
HOC:Higher-Order Component,高阶组件，以组件作为参数，返回一个组件


可以使用组件实现横切关注点。

**注意**
1. 不要在render中使用高阶组件
2. 不要在高阶组件中更改传入的组件

HocTestA
```js
import React, { Component } from 'react'

export default class HocTestA extends Component {
  render() {
    return (
      <div>HocTestA</div>
    )
  }
}

```


HocTestB
```js
import React, { Component } from 'react'

export default class HocTestB extends Component {
  render() {
    return (
      <div>HocTestB</div>
    )
  }
}
```
WithTestHoc
```js
import React from "react";
/**
 * 高阶组件
 * @param {*} Comp 组件
 * @returns 
 */
export default function WithTest(Comp){
    return class WithTestWrapper extends React.Component{
        componentDidMount(){
            console.log(`组件${Comp.name}被创建`);
        }
        render(){
            return <>
            <Comp {...this.props}></Comp>
            </>
        }
    }
}
```
使用
```js
import React, { Component } from "react";
import WithTest  from "./HOC/WithTestHoc";
import HocTestA from "./components/HocTestA";
import HocTestB from "./components/HocTestB";

const TestA = WithTest(HocTestA);
const TestB = WithTest(HocTestB)
export default class App extends Component {
	render() {
		return (
			<>
			<TestA></TestA>
			<TestB></TestB>
			</>
		)
	}
}

```
## [ref](https://zh-hans.reactjs.org/docs/refs-and-the-dom.html#gatsby-focus-wrapper)

reference：引用
直接使用dom中的某个方法，或使用组件中的某个方法。


1. ref作用于内置的html组件，得到的将是真是的dom对象
2. ref作用于类组件，将得到类的实例
3. ref不能直接作用于函数组件，函数组件内部可以正常使用


ref不推荐使用字串符赋值，推荐使用函数或对象
**字符串** 要删除的使用方法

```js
import React, { Component } from "react";

export default class Ref extends Component {
    onHandleClick = ()=>{
        // 读取input的输入值
        console.log(this.refs.text.value)
    }
	render() {
		return (
			<>
				<input ref="text" type="text" />
                <button onClick={this.onHandleClick}>获取input的值</button>
			</>
		);
	}
}

```

**对象**
通过```React.createRef```函数创建
对象结构
```js
{
  current:null,//刚创建时
}

```

可以通过current属性获取到引用的值

```js
import React, { Component } from "react";

export default class Ref extends Component {
    constructor(props){
        super(props);
        this.input = React.createRef()
    }
    onHandleClick = ()=>{
        // 读取input的输入值
        console.log(this.input.current.value)
    }
	render() {
		return (
			<>
				<input ref={this.input} type="text" />
                <button onClick={this.onHandleClick}>获取input的值</button>
			</>
		);
	}
}

```

**函数**

函数的调用时间：
1. componentDidMount的时候会调用该函数
 - 在componentDidMount事件中可以使用ref
2. 如果ref的值发生了变动（旧的函数被新的函数替代），分别调用旧的函数和新的函数，时间点出现在componentDidUpdate之前
- 旧的函数被调用时，传递参数为null
- 新的函数被调用时，传递参数为引用对象

```js
import React, { Component } from "react";

export default class Ref extends Component {
    constructor(props){
        super(props);
        this.input = React.createRef()
    }
    onHandleClick = ()=>{
        // 读取input的输入值
        console.log(this.input.value)
    }
	render() {
		return (
			<>
				<input ref={el=>this.input = el} type="text" />
                <button onClick={this.onHandleClick}>获取input的值</button>
			</>
		);
	}
}

```

```js
import React, { Component } from "react";

export default class Ref extends Component {
    constructor(props){
        super(props);
        this.input = React.createRef()
    }
    onHandleClick = ()=>{
        // 读取input的输入值
        console.log(this.input.value)
    }

    getRef = (el)=>{
        this.input = el
    }
	render() {
		return (
			<>
				<input ref={this.getRef} type="text" />
                <button onClick={this.onHandleClick}>获取input的值</button>
			</>
		);
	}
  ```