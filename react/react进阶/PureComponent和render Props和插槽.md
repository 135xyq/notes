# PureComponent 和render props和插槽

## PureComponent

纯组件，用于避免不必要的渲染（运行render函数），提高效率

PureComponent是一个组件，如果一个组件继承自该组件，则该组件的shouldComponentUpdate会进行优化，会将组件的属性和状态进行浅比较，如果相等则不会重新渲染。

在函数组件中使用React.memo函数制作纯组件。

## render props

用于解决某些组件的功能大致相同，仅仅是渲染界面不同。（可用高阶组件）

将一个函数作为一个组件的属性，其中函数的返回值作为渲染内容，通常该属性的名字为render(其他名字也行)

## Portals

将会变成虚拟DOM树和真实DOM树不一致

插槽：将一个React元素渲染到指定的DOM容器中

使用```ReactDOM.createPortal(React元素，真实的DOM容器)```,该容器返回一个React元素

**注意**

1. React中的事件是包装过的
2. 它的事件冒泡是根据虚拟DOM树来冒泡的，与真实的DOM树无关