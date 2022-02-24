vue3中不存在Vue构造函数，需要使用具名导出createApp来创建一个vue应用

## [vue3中为数据设置响应式数据](https://v3.cn.vuejs.org/api/computed-watch-api.html#computed):
1. 从vue中导入ref 函数
2. 通过 ref 定义变量，变量即为响应式数据，参数为数据初始值，返回的数据是一个对象
3. 在模板中可以直接使用变量名的获取数据(vue3内部处理)，但是在js环境中需要注意这个变量是一个对象，获取数据需要使用 变量名.value
```vue
import {ref } from 'vue';
let data = ref(dataInfo);//括号内为数据的初始值
```

## vue3监控响应式数据变化
1. 从vue中导入watchEffect(立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更时重新运行该函数。)
2. 将响应式数据在watchEffect函数中使用
```javascript
import {ref ,watchEffect} from 'vue';
let data = ref(dataInfo);//括号内为数据的初始值
watchEffect(()=>{
	console.log(data.value)
})
```

在vue2中引入外部css文件，为防止样式冲突，可以使用src属性以引入文件。下面的子组件也不能使用该样式。