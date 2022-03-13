# [express](https://www.expressjs.com.cn/4x/api.html#express)

## 使用express方法创建一个express应用


```js
const http = require('http');
const express = require('express');

const app = express(); // 创建一个express应用
// app用来处理请求的函数

const server = http.createServer(app);

server.listen(9527, () => {
    console.log("listen port 9527!")
})


server.on('listening', res => {
    console.log(res)
})

```

等价于：
```js
const express = require('express');
const app = express(); // 创建一个express应用
// app用来处理请求的函数

app.listen(9527, () => {
    console.log('listen port 9527')
})
```

## 配置请求响应函数

```js
app.get('/abc', (req, res) => {
    console.log('请求头：', req.headers); //请求头
    console.log('请求路径:', req.path); //请求路径
    console.log('请求参数:', req.query); //请求参数

    // 发送响应
    res.send('<h1>ab435c</h1>')

})
```

## 中间件

### [基本使用](https://www.expressjs.com.cn/4x/api.html#router)

当匹配到请求时，会交给第一个处理函数处理，函数中要**手动交给**后续的中间件处理。

如果已经没有后续中间件，express发现响应没有结束，express会响应404。

如果中间件发生了错误，不会停止服务器（相当于调用了next（错误处理对象）），会寻找后续的错误处理中间件，如果没有会响应500

```js
const express = require('express');

const app = express();

app.listen(9527, () => {
    console.log('server is listening port 9527')
})

app.get('/news', (rep, res, next) => {
        console.log('第一个处理函数！');
        next(); //需要手动移交
    },
    (rep, resp, next) => {
        console.log('第二个处理函数！');
        next();
    }
)

app.get('/news', (rep, res, next) => {
    console.log('第三个处理函数！');
    res.send('123')
})
```
处理遇到的报错
```js

const express = require('express');

const app = express();

app.listen(9527, () => {
    console.log('server is listening port 9527')
})

app.get('/news', (req, res, next) => {
        console.log('第一个处理函数！');
        next(); //需要手动移交
    },
    (req, res, next) => {
        console.log('第二个处理函数抛出错误！');
        throw new Error('报错了！');
        next();
    },
    (error, req, res, next) => {
        //上一个中间件抛出错误，下一个中间件要捕获错误，需要传入error错误参数
        console.log('第三个处理函数！');
        res.send('123');
        next();
    }
)
```

### 自带中间件

#### [express.static](https://www.expressjs.com.cn/4x/api.html#express.static)

静态服务器

参数一：静态资源的目录

当请求时，会根据请求路径(req.path)，从指定的目录中寻找是否存在该文件，如果存在，直接响应文件内容，而不再移交给后续的中间件;
如果不存在文件，则直接移交给后续的中间件处理;
默认情况下，如果映射的结果是一个目录，则会自动使用index.html文件。

```js
const express = require('express');
const path = require('path');

const app = express();

app.listen(9527, () => {
    console.log('server is listening port 9527')
})

const root = path.resolve(__dirname, '../public')
app.use(express.static(root));

```
#### [express.json](https://www.expressjs.com.cn/4x/api.html#express.json)

解析JSON格式的消息体
```js
app.use(express.json())
```


#### [express.urlencoded](https://www.expressjs.com.cn/4x/api.html#express.urlencoded)

解析application/x-www-form-urlencoded形式消息体。
使用之后可以获取请求体中的数据

```js

app.use(express.urlencoded({
    extended: true,
}))

app.post('/api/student', (req, res) => {
    console.log(req.body)
    res.send('api/student post')
})
```

##  [express路由](https://www.expressjs.com.cn/4x/api.html#router)


```js
const express = require('express');

const app = express();

app.listen(9527, () => {
    console.log('server is listening port 9527')
})

//创建一个路由
const router = express.Router();

router.get('/', (req, res) => {
    res.send('获取学生列表！');
})


router.get('/:id', (req, res) => {
    res.send('获取单个学生的信息！', id);
})

router.put('/:id', (req, res) => {
    res.send('修改学生的信息！');
})

router.post('/', (req, res) => {
    res.send('新增一个学生！');
})

router.delete('/:id', (req, res) => {
    res.send('删除一个学生！')
})

app.use('/api/student', router)
```
