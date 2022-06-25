# 渲染原理

## React元素：

React Element，通过React.createElement创建（语法糖：JSX）

## React节点：

专门用于渲染到UI界面的对象，React会通过React元素创建React节点
ReactDOM一定时通过React节点来进行渲染的

### 节点类型


- React DOM节点(ReactDOMComponent)：创建该节点的React元素是一个字符串
- React 组件节点：创建该节点的React元素类型是一个函数或是一个类
- React 文本节点：由字符串、数字创建
- React 空节点：由null、undefined、false、true创建
- React 数组节点：由一个数组创建

## 真实DOM

通过document.createElement创建的dom元素

## 首次渲染(新节点渲染)

1. 根据参数的值创建节点
2. 不同节点的操作有异
- 文本节点：通过```document.createTextNode```创建真实的文本节点
- 空节点：什么都不做
- 数组节点：遍历数组，将数组每一项递归创建节点
- DOM节点：通过```document.createElement```创建真实的DOM对象，然后立即设置该真实DOM元素的各种属性，遍历React元素的children属性，递归创建节点
- 组件节点：
    + 函数组件：调用函数（该函数必须返回一个可以生成节点的内容），将该函数的返回结果递归创建节点
    + 类组件：
        1. 创建该类的实例
        2. 立即调用对象的生命周期方法：```static getDerivedStateFromProps```
        3. 运行该对象的render方法，拿到节点对象（递归创建节点）
        4. 将该组件的```componentDidMount```加入到执行队列，在整个虚拟DOM树全部构建完毕，并且将真实的DOM对象加入到容器中后，执行该队列
3. 生成出虚拟DOM树，将该树保存起来
4. 将之前生成的真实DOM对象加入到容器中
