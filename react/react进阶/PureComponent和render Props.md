# PureComponent 和render props

## PureComponent

纯组件，用于避免不必要的渲染（运行render函数），提高效率

PureComponent是一个组件，如果一个组件继承自该组件，则该组件的shouldComponentUpdate会进行优化，会将组件的属性和状态进行浅比较，如果相等则不会重新渲染。

在函数组件中使用React.memo函数制作纯组件。

