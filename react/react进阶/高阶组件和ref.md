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
## ref