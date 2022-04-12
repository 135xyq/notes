# uniCloude

## hbuilderX中使用unicloud云开发平台

### 文档

- 参考文档：https://uniapp.dcloud.io/uniCloud/README
- web控制台文档：https://unicloud.dcloud.net.cn/login



### 传统业务开发流程

> ​	前端 => 后端 => 运维 => 发布上线



**使用unicloud云开发平台**

> 前端 => 运维 => 发布上线



### 什么是unicloud

> `uniCloud` 是 DCloud 联合阿里云、腾讯云，为开发者提供的基于 serverless 模式和 js 编程的实现后端服务的云开发平台。不需要服务器的购买配置即可快速创建一个完整的后端服务。



### unicloud优点

- 用JavaScript开发前后台整体业务
- 非h5项目免域名使用服务器
- 敏捷性业务处理，不需要前后端分离开发



## 开发流程



![image-20210714094129125](./images\008i3skNly1gsg8eblz9cj30ue0p0qge-16489954981379.jpg)



### uncloud构成

![image-20210714094241143](./images\008i3skNly1gsg8fn8yurj61520ni4g702-164899550123411.jpg)



#### 云数据库

​	![image-20210714094356661](./images\008i3skNly1gsg8h45qchj30la0putor-164899550418713.jpg)



#### 云存储及CDN

> 可进行文件的相关存储操作

参考文档：https://uniapp.dcloud.io/uniCloud/storage

---





#### 创建云函数工程



1. **指定unicloud工程创建**

​	![image-20210714095337821](./images\008i3skNly1gsg8qxpf2xj613k0tudkm02-164899551172315.jpg)

2. **保证uni-app应用标识appID填写**（保证用户为登录状态）

   ![image-20210714095821885](./images\008i3skNly1gsg8w79025j31mc0iu77u-164899551658117.jpg)

3. **进行云服务空间创建**

   ![image-20210714100204541](./images\008i3skNly1gsg8zr9qc8j31fz0u0164-164899558987323.jpg)

   > 如果未进行实名认证，会跳转至实名认证页面进行实名认证，等待实名认证审核之后可以开通服务空间。若腾讯云实名认证提示身份证下已创建过多账户，则需要在腾讯云官网注销不用的账户

4. 进行云函数创建

   ![image-20210714100454958](./images\008i3skNly1gsg92o8dg6j30y60h00y3-164899551946519.jpg)

   ```js
   'use strict';
   // 一个通过nodeJS运行的函数在服务器端使用
   exports.main = async (event, context) => {
   	//event为客户端上传的参数
   	//context 包含了调用信息及运行状态,获取每次调用的上下文
   	console.log('event : ', event)
   	
   	//返回数据给客户端
   	return {
   		"code":0,
   		"msg":"云函数调用成功"
   	}
   };
   ```

   

5. **云WEB控制台查看**

   ![image-20210714100831644](./images\008i3skNly1gsg96hdcovj32gl0u0qga-164899552169021.jpg)

6. **云数据库操作**

   > 在云数据库中进行数据操作，全部使用双引号进行值的定义

7. 云存储

   > 在云存储中进行文件的上传
   >
   > api使用：
   >
   > ```js
   > uniCloud.uploadFile({})
   > ```

8. 跨域处理

   参考文档https://uniapp.dcloud.io/uniCloud/quickstart?id=useinh5

## unicloud api操作

### 云函数调用

**参考文档**：https://uniapp.dcloud.net.cn/uniCloud/cf-functions?id=clientcallfunction

```js
// promise方式
uniCloud.callFunction({
    name: 'test', // 云函数名称
    data: { a: 1 }   // 请求参数
  })
  .then(res => {});

// callback方式
uniCloud.callFunction({
    name: 'test',
    data: { a: 1 },
    success(){},  // 成功
    fail(){},   // 失败
    complete(){}   // 完成（不管成功与失败）
});
```

### 云函数实现云数据库基本增删改查

#### 1. 获取数据库引用

```js
const db = uniCloud.database()
```

2. 获取数据库集合引用

   ```
   const collection = db.collection('unicloud-test-714') // uncloud-test-714 为数据表名称
   ```

3. 新增记录

   ```js
   const res = collection.add({user:'alan'})
   ```

   ```js
   'use strict';
   const db = uniCloud.database() // 获取数据库引用
   
   exports.main = async (event, context) => {
   	// 获取集合引用
   	const collection = db.collection('unicloud-test-714')
   	// 新增数据
   	const res = await collection.add({user:'alan'})
   	console.log(res)
   	return {
   		"code":0,
   		"msg":"云函数调用成功"
   	}
   };
   ```

4. 删除记录

   ```js
   	const res = await collection.doc('60ee51103b7d3500014124c1').remove()
   ```

5. 数据更新

   ```js
   const res = await collection.doc('60ee52a1827eca0001e56bc4').update({
   		name:"joob"
   	})
   
   const res = await collection.doc('60ee52a1827eca0001e56bc4').set({   // 如果说获取不到内容，从新进行插入记录的操作
   		name:"joob",
     	type:"javascript"
   	})
   ```

   > update与set的区别：
   >
   > 当没有找到指定记录时，使用update无法进行更新操作，set在没有查找到指定记录的时候，可以进行新增内容的操作（不存在进行创建添加操作）

5. 数据查找

   ```js
   // 查询全部
   	const res = await collection.get()
   // 指定条件进行查询-id查询
     const res = await collection.doc('id').get()  // id为需要查询的指定id
   // 指定条件查询-其他条件进行查询
     const res = await collection.where({name:"alan"}).get()
   ```

   

   #### 云存储操作

   1. 使用uni.chooseImage方法进行图片选择获取

      参考地址：https://uniapp.dcloud.io/api/media/image?id=chooseimage

      ```js
      	uni.chooseImage({
      					count: 1,
      					success(res) {
      						console.log(JSON.stringify(res.tempFilePaths))
      					}
      				})
      ```

   2. 使用uniCloud.uploadFile进行文件上传

      参考文档：https://uniapp.dcloud.io/uniCloud/storage?id=clouduploadfile

      ```js
      uni.chooseImage({
      					count: 1,
      					async success(res) {
      						let result = await uniCloud.uploadFile({
      							filePath:res.tempFilePaths[0],
      							cloudPath:'a.jpg',
      							success(res) {
      								console.log(res)
      							},
      							fail(err) {
      								console.log(err)
      							}
      						});
      					}
      				})
      ```

   3. 使用uniCloud.deleteFile进行图片删除

      参考文档：https://uniapp.dcloud.io/uniCloud/storage?id=clouddeletefile

      **阿里云函数删除不能在客户端进行删除操作，下列代码在云函数中进行使用**

      ```js
      let result = await uniCloud.deleteFile({
      	   fileList:['https://vkceyugu.cdn.bspapp.com/VKCEYUGU-6ce25980-c28e-4e78-bdef-a96eb40ad98b/06a1cb3a-84b7-47a0-b554-8aff299cb255.jpg'],
      	});
      	console.log(result)
      ```

