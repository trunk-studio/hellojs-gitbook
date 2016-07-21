# [Sequelize](http://docs.sequelizejs.com/en/latest/)
Sequelize 是一款能控制 PostgreSQL、MySQL、SQLite 的 ORM ，ORM 簡單來說就是別人封裝好可以直接操做資料庫的工具，而不直接使用 SQL 語法對資料庫進行操作。
這樣有以下優點：

* 開發人員不用管底層使用哪種資料庫，都能使用同樣的程式碼降低程式與資料庫間的耦合
* ORM 能幫你擋掉大多數的 SQL 注入攻擊 ( SQL Injection )
* 提高開發效率
* 方便轉移資料庫，本地測試時能使用 SQLite，正式上線時再轉移成 MySQL

缺點:
* 效能上的犧牲
* 在複雜的查詢上 ORM 有可能不支援

### [Data Type](http://docs.sequelizejs.com/en/latest/docs/models-definition/#data-types)
## 開始使用 Sequelize

#### 定義 table
```javascript
module.exports = (sequelize, DataTypes) => {
  var User = sequelize.define('User', {
    // 欄位名稱:: 欄位型態
    username: DataTypes.STRING,
    email: DataTypes.STRING,
    password: DataTypes.STRING,
    age: DataTypes.INTEGER,
  }, {
    classMethods: {
      associate: (models) => {
      }
    }
  });

  return User;
};
```

#### 新增 user
```javascript
await models.User.create({
  username: 'test',
  email: 'test@gmail.com',
  password: '123123',
  age: 18,
});
```

#### 根據 id 查詢 user
```javascript
await models.User.findById(userId);
```

#### 根據 email 查詢 user
```javascript
let user = await models.User.findOne({
  where: {
    email: 'test@gmail.com',
  },
});
```

#### 更新 user 資料
```javascript
let user = await models.User.findById(userId);
user.password = '123123';
await user.save();
```

#### 刪除 user
```javascript
let user = await models.User.findById(userId);
await user.destroy();
```

### 進階

#### 一次創建多組資料
```javascript
const userList = [
  { username: 'test1', password: 'test1', email: 'test1@gmail.com', age: 18 },
  { username: 'test2', password: 'test2', email: 'test2@gmail.com', age: 30 },
  { username: 'test3', password: 'test3', email: 'test3@gmail.com', age: 20 },
  { username: 'test4', password: 'test4', email: 'test4@yahoo.com.tw', age: 23 },
];
await models.User.bulkCreate(userList);
```

#### [進階查詢](http://docs.sequelizejs.com/en/latest/docs/querying/#operators)
#### 查找 18 ~ 23 歲的 user
```javascript
const user = await models.User.findAll({
  where: {
    age: {
      $between: [18, 23],
    },
  },
});
```

#### 查找 email 為 gmail 的 user
```javascript
const user = await models.User.findAll({
  where: {
    email: {
      $like: '%@gmail.com',
    },
  },
});
```

#### 根據 age 排序 user
```javascript
const user = await models.User.findAll({
  order: 'age ASC',
});
```
