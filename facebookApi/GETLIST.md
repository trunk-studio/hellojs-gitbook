## 開始使用 GET 功能

#### 定義 constructor
```javascript
constructor({token, userId}) {
    this.FB = FB;
    this.FB.setAccessToken(token);
    this.userId = userId;
  }
```

#### get friends list
```javascript
async getFriends() {
    try {
      let result = await new Promise((resolve, reject) => {
        this.FB.api(`${this.userId}/friends?fields=id,name,birthday,email`, function(res, error) {
          if(error) reject(error);
          resolve(res.data);
        });
      });
      result[0].email = "aaa@gmail.com";
      console.log("result = " + result[0].email);
      return result;
    } catch (e) {
      throw e;
    }
  }
```
