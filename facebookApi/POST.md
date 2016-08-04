## 開始使用 Post 功能

#### 定義 constructor
```javascript
constructor({token, userId}) {
    this.FB = FB;
    this.FB.setAccessToken(token);
    this.userId = userId;
  }
```

#### PO文
```javascript
async publishPost({message}) {
    try {
      let result = await new Promise((resolve, reject) => {
        this.FB.api(`${this.userId}/feed`, 'post', { message }, function(res, error) {
          if(error) reject(error);
          resolve(res);
        });
      });
      return result;

    } catch (e) {
      throw e;
    }
  }
```
