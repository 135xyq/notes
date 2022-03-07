# mysql驱动程序

## 驱动程序

驱动程序是连接内存和其他存储介质的桥梁

mysql驱动程序是连接内存数据和mysql数据的桥梁

## 驱动程序mysql2的使用    [npm](https://www.npmjs.com/package/mysql2)     [github](https://github.com/sidorares/node-mysql2)

### 使用createConnection创建一个连接

#### createConnection 配置参数

- host：主机名
- user：用户名
- password：用户密码
- database：连接的数据库
- mutipleStatements:是否允许一次运行多条SQL语句


#### connection.query()的使用

第一个参数：mysql语句
第二个参数：回调函数（第一个参数错误信息，第二个参数为结果）

#### 回调操作

```js
const mysql = require('mysql2');
const { createConnection } = require('mysql2/promise');

//创建一个数据库连接

const connection = mysql.createConnection({
    host: '127.0.0.1',
    user: 'root',
    password: 'xyq2386152296',
    database: 'my_mysql_test'
})

//简单使用

connection.query(
    'select * from company',
    (error, result) => {
        console.log('error: ', error);
        console.log('result: ', result)
    }
)

connection.end();//关闭连接

输出：
error:null
result:
[
  {
    id: 1,
    name: '腾讯科技',
    location: '广东省深圳市腾讯大厦',
    buildDate: 2009-07-09T16:00:00.000Z
  },
  {
    id: 2,
    name: '渡一教育',
    location: '黑龙江哈尔滨',
    buildDate: 2004-02-09T16:00:00.000Z
  },
  {
    id: 3,
    name: '蚂蚁金服',
    location: '中国杭州市西湖区西溪路556号蚂蚁Z空间',
    buildDate: 2010-04-03T16:00:00.000Z
  }
]

```
#### 异步操作

```js

const mysql = require('mysql2/promise');


mysql.createConnection({
    host: '127.0.0.1',
    user: 'root',
    password: 'xyq2386152296',
    database: 'my_mysql_test'
}).then(resp => {
    resp.query('select * from company').then(resp => {
        console.log(resp[0]);// 返回值为数组，第一项为error或data 
    });
    resp.end();
})

输出：
[
  {
    id: 1,
    name: '腾讯科技',
    location: '广东省深圳市腾讯大厦',
    buildDate: 2009-07-09T16:00:00.000Z
  },
  {
    id: 2,
    name: '渡一教育',
    location: '黑龙江哈尔滨',
    buildDate: 2004-02-09T16:00:00.000Z
  },
  {
    id: 3,
    name: '蚂蚁金服',
    location: '中国杭州市西湖区西溪路556号蚂蚁Z空间',
    buildDate: 2010-04-03T16:00:00.000Z
  }
]

```

#### 使用语句操作，不使用query防止进行SQL注入，危害数据库安全，使用[execute](https://github.com/sidorares/node-mysql2#using-prepared-statements)

```js
// 使用execute防止SQL注入

function test(id) {
    const mysql = require('mysql2');

    //创建一个数据库连接
    const connection = mysql.createConnection({
        host: '127.0.0.1',
        user: 'root',
        password: 'xyq2386152296',
        database: 'my_mysql_test'
    })

    const sql = `select * from company where id = ?`
    connection.execute(sql, [id], (error, result) => {
        console.log(result);
    })

    connection.end();
}

```

##### excute参数

第一个参数SQL语句，每一个需要传递的参数，需要使用 ？ 占位，（当使用模糊查询时，可以使用 like concat('%',?,‘%’））；
第二个参数依次表示SQL语句中使用？占位的数据。

### 使用[createPool](https://github.com/sidorares/node-mysql2#using-connection-pools)创建一个连接池

每次开启的数据库连接不能超过规定的数量，超过的部分需要排队，等候连接池中的空闲连接。 防止数据库连接过多卡顿。不用手动关闭连接，会自动管理。

```js
// 使用createPool连接池
const mysql = require('mysql2');

//创建一个数据库连接
const pool = mysql.createPool({
    host: '127.0.0.1',
    user: 'root',
    password: 'xyq2386152296',
    database: 'my_mysql_test'
})


function test(id) {
    const sql = `select * from company where id = ?`
    pool.execute(sql, [id], (error, result) => {
        console.log(result);
    })
}

test(1);

```

##### 配置参数

- waitForConnections：当连接池满的时候，新来一个连接是否等待，如果不等待则直接报错，默认为true；
- connectionLimit: 连接池中最大的连接数量，默认为10 ；
- queueLimit: 新来连接的排队长度，如果为0表示不限制长度；