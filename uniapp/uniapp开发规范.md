# uniapp开发规范

- 页面文件遵循Vue单文件组件（SFC）规范

- 组件标签靠近小程序规范 =>https://uniapp.dcloud.io/component/README

  ```vue
  <template>
  	<view>
  		页面内容
  	</view>
  </template>
  
  <script>
  	export default {
  		data() {
  			return {
  			}
  		},
  		methods: {	
  		}
  	}
  </script>
  
  <style>
  </style>
  ```

- 接口能力（JS API）靠近微信小程序规范 => https://uniapp.dcloud.io/api/README

  ```java
  uni.getStorageInfoSync()
  ```

- 数据绑定事件处理同Vue.js规范

  ```vue
  <template>
    <view @click="onClickFn">
        点击事件绑定
    </view>
  </template>
  
  <script>
  export default {
    methods: {
      onClickFn() {
        console.log('click事件')
      }
    }
  }
  </script>
  
  <style lang="scss" scoped>
  </style>
  ```

- 兼容多端运行，使用flex布局进行开发



---



## uniapp开发环境

### 开发工具

uni-app 官方推荐使用 **HBuilderX** 来开发 uni-app 类型的项目。主要好处：

- 模板丰富
- 完善的智能提示
- 一键运行

### 下载 HBuilderX

1. 访问 HBuilderX 的官网首页 https://www.dcloud.io/hbuilderx.html
2. 点击首页的 `DOWNLOAD` 按钮
3. 选择下载 `正式版`/alpha -> `App 开发版`
4. 将下载的 `zip包` 进行解压缩
5. 将解压之后的文件夹，存放到**纯英文**的目录中（且不能包含括号等特殊字符）
6. 双击 `HBuilderX.exe` 即可启动 HBuilderX
7. 详细安装文档：=> https://hx.dcloud.net.cn/Tutorial/install/windows



## 工程搭建

1. 文件 -> 新建 -> 项目

   ![img](./images\008i3skNly1gselljycn2j31hc0joq3c-16487011449324.jpg)

2. 填写项目基本信息

   ![img](https://tva1.sinaimg.cn/large/008i3skNly1gselm265sdj30na0g3di5.jpg)

3. 项目创建成功

   ![img](https://tva1.sinaimg.cn/large/008i3skNly1gselmb4wf0j61hc0sywev02.jpg)



​	**基本目录结构**

```css
项目名称
----【pages】    内部存放所有页面
----【static】   存放所有静态资源，比如图片，字体图标
----【unpackage】存放所有打包生成后的文件
----app.vue     应用配置，用来配置App全局样式以及监听 应用生命周期
----main.js			Vue初始化入口文件
----mainfast.json  配置应用名称、appid、logo、版本等打包信息
----pages.json    配置页面路由、导航条、选项卡等页面类信息
----uni.scss      用途是为了方便整体控制应用的风格。比如按钮颜色、边框风格，uni.scss文件里预置了一批scss变量预置。
```



## 项目运行

### 浏览器运行

1. ![image-20210720101209233](./images\008i3skNly1gsn7079jy3j313q0u0dkk.jpg)

### 小程序运行

1. 填写自己的微信小程序的 AppID：

   ![img](./images\008i3skNly1gselrjw91dj31hc0n7q3v.jpg)

2. 在 HBuilderX 中，配置“微信开发者工具”的**安装路径**：

   ![img](./images\008i3skNly1gsels176jwj31hc0lpab2.jpg)

3. 在微信开发者工具中，通过 `设置 -> 安全设置` 面板，开启“微信开发者工具”的**服务端口**：

   ![image-20210712235549929](./images\008i3skNly1gselum0va7j30tw0nywg0.jpg)

4. 在 HBuilderX 中，点击菜单栏中的 `运行 -> 运行到小程序模拟器 -> 微信开发者工具`，将当前 uni-app 项目编译之后，自动运行到微信开发者工具中，从而方便查看项目效果与调试：

   ![img](./images\008i3skNly1gselv7wqqrj31hc0s8go0.jpg)

5. 初次运行成功之后的项目效果：

   ![img](./images\008i3skNly1gselvryapfj31hc0sygmn.jpg)

### app真机运行

> ​	确保你的手机与电脑是在同一个局域网下面

1. 手机开启开发者模式
2. 选择数据管理
3. hbuildeX选择真机运行
4. 等待基座安装
5. 安装完成手机运行项目

### IOS模拟器运行

1.  Xcode下载
2. 定义版本进行模拟器运行

---
