# 存储
----------
## cookie
#### cookie：可读可写,依托与http协议
1. cookie不可跨域
2. cookie存储在浏览器里面
3. cookie有大小和数量的限制（超过部分删除）
    1. 数量在50个左右
    2. 大小在4KB左右
    4. cookie的存储时间非常灵活
    5. cookie不光可以服务器设置，客户端也可以设置


#### 前端设置cookie：
document.cookie (键值对形式)只能设置一次cookie

### cookie的属性：
1. name：cookie的名字（唯一性）
2. value: cookie的值（字符串）
3. domain ： 设置cookie在哪个域下是有效的
4. path ： cookie的路径
5. expires : cookie的过期时间（默认是session在浏览器关闭时删除）具体时间点
`document.cookie = 'margin = 20px;expires = ' + new Date(2021, 7, 3);`
6. max-age : cookie的有效期（以秒为单位的时间段），存活时间
`document.cookie = 'margin = 20px;max-age = 10';  //存活时间为10秒`
7. HttpOnly ：有这个标记的cookie前端啊无法获取
8. Secure : 设置cookie只能通过HTTPS协议传输
9. SameSite ：设置cookie在跨域请求时不能被发送


## Web Storage：不依托于http协议 
不能跨域 
#### localStorage：在所有域名下都有效，页面关闭还存在 
#### sessionStorage：仅在当前窗口有效，页面关闭不存在
localStorage和sessionStorage都继承自对象Storage
### 属性和方法：
1. length：本地存储的数量
2. key()：通过索引找到存储的数据，（排序不规范，和添加顺序不一样）
3. getItem（）：通过键名取到本地存储的数据（取到的是一个字符串）
`console.log(localStorage.getItem('color'));`
4. setItem（）：设置一个本地存储数据

`localStorage.setItem('name', 'xyq');`
```javascript
        var color = {
            "c1": "red",
            "c2": "green"
        };
        localStorage.setItem('color', JSON.stringify(color));
        添加对象
```
5. removeItem（）：删除一个本地存储数据
6. clearItem（）：清空本地存储
`localStorage.clear();//全部清空`

#### storage事件：
调用所有同域下其他窗口的storage事件，不过它本身触发storage即当前窗口是不会触发这个事件的`