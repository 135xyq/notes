# sequelize中的[模型定义](https://demopark.github.io/sequelize-docs-Zh-CN/core-concepts/model-basics.html)和同步

## [创建数据库连接](https://demopark.github.io/sequelize-docs-Zh-CN/core-concepts/getting-started.html)

```js
const { Sequelize } = require('sequelize');

// 创建一个实例

const sequelize = new Sequelize('my_school_db', 'root', 'xyq2386152296', {
    host: 'localhost',
    dialect: 'mysql'
});

//测试连接
(async function() {
    try {
        await sequelize.authenticate();
        console.log('Connection has been established successfully.');
    } catch (error) {
        console.error('Unable to connect to the database:', error);
    }
})()
```

## [模型的定义](https://demopark.github.io/sequelize-docs-Zh-CN/core-concepts/model-basics.html)

模型是代表数据库中表的抽象. 在 Sequelize 中,它是一个 Model 的扩展类.
该模型告诉 Sequelize 有关它代表的实体的几件事,例如数据库中表的名称以及它具有的列(及其数据类型).
Sequelize 中的模型有一个名称. 此名称不必与它在数据库中表示的表的名称相同.


### 使用 sequelize.define:

```js
const { Sequelize, DataTypes } = require('sequelize');
const sequelize = new Sequelize('sqlite::memory:');

const User = sequelize.define('User', {
  // 在这里定义模型属性
  firstName: {
    type: DataTypes.STRING,
    allowNull: false
  },
  lastName: {
    type: DataTypes.STRING
    // allowNull 默认为 true
  }
}, {
  // 这是其他模型参数
});

// `sequelize.define` 会返回模型
console.log(User === sequelize.models.User); // true

```

### 扩展 Model

```js
const { Sequelize, DataTypes, Model } = require('sequelize');
const sequelize = new Sequelize('sqlite::memory:');

class User extends Model {}

User.init({
  // 在这里定义模型属性
  firstName: {
    type: DataTypes.STRING,
    allowNull: false
  },
  lastName: {
    type: DataTypes.STRING
    // allowNull 默认为 true
  }
}, {
  // 这是其他模型参数
  sequelize, // 我们需要传递连接实例
  modelName: 'User' // 我们需要选择模型名称
});

// 定义的模型是类本身
console.log(User === sequelize.models.User); // true

```

## 同步

- 模型名.sync() - 如果表不存在,则创建该表(如果已经存在,则不执行任何操作)
- 模型名.sync({ force: true }) - 将创建表,如果表已经存在,则将其首先删除
- 模型名.sync({ alter: true }) - 这将检查数据库中表的当前状态(它具有哪些列,它们的数据类型等),然后在表中进行必要的更改以使其与模型匹配.