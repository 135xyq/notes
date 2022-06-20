# Context

上下文：做某一些事情的环境


React上下文的特点：
1. 当某个组件创建上下文后，上下文中的数据会被所有后代组件共享;
2. 如果某个组件依赖了上下文，会导致该组件不再纯粹(数据仅来自于属性props)

## 旧版API

**创建上下文**

只有类组件才能创建上下文

1. 给类组件书写一个静态属性```childContextTypes```,对上下文中的数据类型进行约束;
2. 添加实例方法 ```getChildContext```,该方法返回的对象就是上下文中的数据，该数据必须满足类型约束，该方法会在每次render之后运行

**使用上下文中的数据**

要求：如果要使用上下文中的数据，组件中必须有一个静态属性```contextTypes```,该属性描述了需要获取的上下文中的数据类型

1. 可以在组件的构造函数中，通过构造函数的第二个参数，获取上下文数据
2. 从组件的context属性中获取
3. 在函数组件中通过第二个参数获取上下文数据

**上下文中的数据变化**

上下文中的数据不可以直接变化，最终都是通过状态改变

后代组件想要修改上下文中的数据，可以通过调用上下文中的函数来修改。


```js
import React, { Component } from "react";
import PropTypes from "prop-types";

/**
 * 在函数组件使用上下文数据
 * @param {*} props
 * @param {*} context
 * @returns
 */
function CompA(props, context) {
	return (
		<>
			CompA
			<h2>name:{context.name}</h2>
			<h2>age:{context.age}</h2>
            <p>
            <button onClick={()=>{
                context.onChange && context.onChange("age",context.age+1)
            }}>年龄加一</button>
            </p>
		</>
	);
}

CompA.contextTypes = {
	name: PropTypes.string,
	age: PropTypes.number,
	onChange: PropTypes.func, //提供后代组件修改上下文数据的函数
};

/**
 * 在类组件终身使用上下文组件
 */
class CompB extends Component {
	static contextTypes = {
		name: PropTypes.string,
		age: PropTypes.number,
        onChange: PropTypes.func, //提供后代组件修改上下文数据的函数
	};
	render() {
		return (
			<>
				<CompA></CompA>
				CompB
				<h2>name:{this.context.name}</h2>
				<h2>age:{this.context.age}</h2>
                <p>
                    <button onClick={()=>{
                        this.context.onChange && this.context.onChange("name","谢永强")
                    }}>修改名字为中文名</button>
                </p>
			</>
		);
	}
}

export default class OldApi extends Component {
	state = {
		name: "xyq",
		age: 21,
	};
	/**
	 *对上下文中的数据类型进行约束
	 *
	 * @static
	 * @memberof OldApi
	 */
	static childContextTypes = {
		name: PropTypes.string,
		age: PropTypes.number,
		onChange: PropTypes.func, //提供后代组件修改上下文数据的函数
	};
	getChildContext() {
		return {
			name: this.state.name,
			age: this.state.age,
			onChange: (key, newData) => {
				this.setState({
					[key]: newData,
				});
			},
		};
	}
	render() {
		return (
			<div>
				<CompB></CompB>
			</div>
		);
	}
}
```

## 新版API

旧版API存在效率问题，并且容易导致滥用

**创建上下文**


上下文是一个独立于组件的对象，该对象通过```React.createContext(默认值)```创建
返回的是一个包含两个属性的对象
1. Provider属性：生产者。一个组件，该组件会创建一个上下文，该组件有一个value属性，通过value为其赋值，同一个Provider不要运用到多个组件中
2. Consumer属性：消费者。一个组件，它的子节点是一个函数（props.children需要传递一个函数），会将上下文数据作为函数的参数，会将函数的返回值渲染出来


**使用上下文中的数据**

1. 在类组件中，可以直接通过this.context获取上下文数据，必须要有静态属性```contextType```,应该赋值为创建的上下文对象；也可以使用Consumer获取数据
2. 在函数组件中，需要使用Consumer获取上下文数据
- Consumer是一个组件
- 它的子节点是一个函数（props.children需要传递一个函数），会将上下文数据作为函数的参数，会将函数的返回值渲染出来




如果上下文提供者(Context.Provider)中的value属性发生变化，会导致该上下文提高的所以后代元素全部重新渲染，无论孩子元素是否存在优化。

```js
import React, { Component } from "react";
import PropTypes from "prop-types";

const ctx = React.createContext();


class CompA extends Component {
    static contextType = ctx;
	render(){
        return (
            <>
                CompA
                <h2>name:{this.context.name}</h2>
                <h2>age:{this.context.age}</h2>
                <p>
                <button onClick={()=>{
                    this.context.onChange && this.context.onChange("age",this.context.age+1)
                }}>年龄加一</button>
                </p>
            </>
        );
    }
}


/**
 * 在类组件上使用上下文组件
 */
class CompB extends Component {
	static contextTypes = {
		name: PropTypes.string,
		age: PropTypes.number,
        onChange: PropTypes.func, //提供后代组件修改上下文数据的函数
	};
	render() {
		return (
			<>
				<CompA></CompA>
				CompB
			</>
		);
	}
}

export default class NewApi extends Component {
	state = {
		name: "xyq",
		age: 21,
        onChange: (key, newData) => {
            this.setState({
                [key]: newData,
            });
        },//提供后代组件修改上下文数据的函数
	};
	render() {
        const Provider = ctx.Provider;
		return (
			<Provider value={this.state}>
				<CompB></CompB>
			</Provider>
		);
	}
}
```


```js
import React, { Component } from "react";
import PropTypes from "prop-types";

const ctx = React.createContext();

function CompA(props) {
	return (
		<ctx.Consumer>
			{(value) => (
				<>
					CompA
					<h2>name:{value.name}</h2>
					<h2>age:{value.age}</h2>
					<p>
						<button
							onClick={() => {
								value.onChange &&
									value.onChange("age", value.age + 1);
							}}
						>
							年龄加一
						</button>
					</p>
				</>
			)}
		</ctx.Consumer>
	);
}

class CompB extends Component {
	static contextTypes = {
		name: PropTypes.string,
		age: PropTypes.number,
		onChange: PropTypes.func, //提供后代组件修改上下文数据的函数
	};
	render() {
		return (
			<>
				<CompA></CompA>
				CompB
			</>
		);
	}
}

export default class NewApi extends Component {
	state = {
		name: "xyq",
		age: 21,
		onChange: (key, newData) => {
			this.setState({
				[key]: newData,
			});
		}, //提供后代组件修改上下文数据的函数
	};
	render() {
		const Provider = ctx.Provider;
		return (
			<Provider value={this.state}>
				<CompB></CompB>
			</Provider>
		);
	}
}
```