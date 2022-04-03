## 基础API

**参考地址**：https://uniapp.dcloud.net.cn/api/README

### API列表

- **网络请求**

  - uni.request 发起网络请求

    > 为了解决uni.request网络请求API相对简单的问题，可使用@escook/request-miniprogram进行网路请求的处理
    >
    > 参考地址：https://www.npmjs.com/package/@escook/request-miniprogram
    >
    > **在小程序中，无法使用fetch及axios进行网络请求发送**
    
    **测试接口地址：https://study.duyiedu.com/api/herolist**

- 上传、下载

  - uni.unloadFile 上传文件  => https://uniapp.dcloud.net.cn/api/request/network-file
  - uni.downloadFile 下载文件

- 图片处理

  - uni.chooseImage 从相册选择图片，或者拍照 =>https://uniapp.dcloud.net.cn/api/media/image?id=chooseimage
  - uni.previewImage 预览图片
  - uni.getImageInfo 获取图片信息

- 数据缓存 => https://uniapp.dcloud.net.cn/api/storage/storage?id=setstorage

  - uni.getStorage 异步获取本地数据缓存
  - uni.getStorageSync 同步获取本地数据缓存
  - uni.setStorage 异步设置本地数据缓存
  - uni.setStorageSync 同步设置本地数据缓存
  - uni.removeStorage 异步删除本地数据缓存
  - uni.reoveStorageSync 同步删除本地数据缓存

- 交互反馈 => https://uniapp.dcloud.net.cn/api/ui/prompt?id=showtoast

  - uni.showToast 显示提示框
  - uni.showLoading 显示加载提示框
  - uni.hideToast 隐藏提示框
  - uni.hideLoading 隐藏加载提示框
  - uni.showModal 显示模态框
  - uni.showActionSheet 显示菜单列表

- 路由

  - uni.navigateTo 保留当前页面，跳转到应用内某个界面，使用uni.navigateBack 返回原页面

  - uni.redirectTo 关闭当前界面，跳转到应用内的某个界面

  - uni.reLaunch 关闭所有界面，打开应用内的某个界面

  - uni.switchTab 跳转到tab Bar页面

    

## 页面布局相关

**page**

> 页面容器css属性

```css
page:{
  height:100%;
  background-color:red;
}
```

**尺寸单位**

可使用单位：px rpx,upx, rem vh  vw

**外部样式文件引入**

同vue使用相同	



## uniapp生命周期

**参考地址：**https://uniapp.dcloud.net.cn/collocation/frame/lifecycle?id=%e5%ba%94%e7%94%a8%e7%94%9f%e5%91%bd%e5%91%a8%e6%9c%9f

### 应用生命周期

- onLaunch 初始化完成时触发（全局🈯️触发一次）

- onShow uni-app启动，或从后台进入前台显示

- onHide 当uni-app 应用从前台进入后台

  > 只能在App.vue里面进行监听，在其他界面监听无效

### 页面生命周期

- onLoad 监听页面加载（可获取上个界面传递的参数）
- onShow 监听页面显示，每次出现在屏幕上都进行触发
- onReady 监听页面初次渲染完成
- onHide 监听页面隐藏
- onUnload 监听页面卸载
- onReachBottom 页面滚动到底部事件

### 组件生命周期

- beofreCreate 
- created
- boforeMount
- mounted
- boforeDestroy
- destroyed



---




## uniApp特色

### 条件编译

> 条件编译是用特殊的注释作为标记，在编译时根据这些特殊的注释，将注释里面的代码编译到不同平台。

**语法**

![image-20210712225857698](https://tva1.sinaimg.cn/large/008i3skNly1gsek7g2i93j31tm0hk41p.jpg)

**取值**

![image-20210712230042343](https://tva1.sinaimg.cn/large/008i3skNly1gsfadcxx6nj310a0u040t.jpg)

**条件编译支持的文件**

- .vue
- .js
- .css
- pages.json
- 各预编译语言文件，如：.scss、.less、.stylus、.ts、.pug

> ​		条件编译是利用注释实现的，在不同语法里注释写法不一样，js使用 `// 注释`、css 使用 `/* 注释 */`、vue/nvue 模板里使用 `<!-- 注释 -->`；



#### 插件安装

1. ​	**scss安装**

   > 可以使用多种预编译处理器进行安装使用，以scss文件为例
   >
   > 下载地址：**https://ext.dcloud.net.cn/plugin?name=compile-node-sass**

   ![image-20210716175247652](https://tva1.sinaimg.cn/large/008i3skNly1gsixua1hqdj316w0u0gpv.jpg)
