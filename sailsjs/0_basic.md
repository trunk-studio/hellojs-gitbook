# Node.js Course
  * http
  * express.js
  * sails.js
    * http://sailsjs.org/

```bash
sudo npm install -g sails

sails new demo
cd demo
npm install
sails generate api User
npm start
```


  * 測試應用，採用 postman 進行驗證
    * [postman chrome plugin](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?utm_source=chrome-ntp-icon)
  * 使用 form 表來來送資料
  * touch form.ejs (點兩下)
  * form: 打開 views/form.ejs

```html
<h1>使用者新增表單</h1>
<form action="/user" method="POST">
    <input type="text" name="name" placeholder="姓名" required>
    <input type="text" name="gender" palceholder="性別" required>
    <input type="number" name="age" placeholder="年紀" required>
    <input type="submit" value="送出" name="submit">
</form>
```

  * 打開 /config/routes.js
```javascript
  '/': {
    view: 'homepage'
  },

  '/form': {
    view: 'form'
  }
```

  * 修改 api/controller/UserController.js

```javascript
module.exports = {

    create: function (req, res) {
        var user = req.body;
        User.create(user)
        .exec(function () {
            return res.redirect("/form");
        });
    }
    // index, create, update, destroy
};
```

  * 預設存在的4個 function

```
create
index
update
destroy
```

  * 打開 config/policies.js
    * 可以設定權限

```javascript
"Usercontroller":
```

# EXTRA
  * 要將資料佈署到 HEROKU
  * 修改 config/models.js

```javascript
module.exports.models = {
   migrate: 'drop'
};
```
  * config/env/development.js

```javascript
module.exports = {
  port: process.env.port || 1337
};
```

  * 佈署線上服務
    * http://heroku.com/
    * https://github.com/

# 本周作業
  * 將 SAILS.JS 程式更新到 Heroku 上面

# ref
  * https://github.com/clonn/demosails
