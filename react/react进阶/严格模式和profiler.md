# 严格模式和Profiler

## [严格模式](https://react.docschina.org/docs/strict-mode.html) 

StrictMode（```React.StrictMode```） 本质上是一个组件，该组件不进行UI渲染,作用：在渲染内部组件时，发现不合适的代码


- 识别不安全的生命周期
- 关于使用过时字符串 ref API 的警告
- 关于使用废弃的 findDOMNode 方法的警告
- 检测意外的副作用
副作用：一个函数中，做了一些影响函数外部数据的事情
    1. 异步处理
    2. 改变参数值
    3. setState
    4. 本地存储
    5. 改变函数外部变量

相反的，如果一个函数没有副作用，则可以认为该函数是一个纯函数。
React要求，副作用代码仅出现在一下生命周期函数中：
1. componentDidMount
2. componentDidUpdate 
3. componentWillUnMount

在严格模式下，虽然不能监控到具体的副作用代码，但他会将不能具有副作用的函数调用两遍，以便发现错误（仅在开发阶段这样处理）
- 检测过时的 context API

## [Profiler](https://react.docschina.org/docs/profiler.html)

性能分析工具

分析某一次或多次提交（更新），涉及到的组件的渲染时间