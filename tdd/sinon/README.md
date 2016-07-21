# Sinon

#### sinon 覆寫 function
```javascript
import sinon from 'sinon';

describe('sinon', (done) => {
  before(async (done) => {
    // 假裝已經登入
    sinon.stub(UserService, 'getLoginState', (req) => true);

    // 回傳假裝的 user data
    const userData = {
      id: 1,
      name: 'fuyaode',
    }
    sinon.stub(UserService, 'getLoginUser', (req) => userData);
  )}
  after((done) => {
    // 回復覆寫 function
    UserService.getLoginState.restore();
    UserService.getLoginUser.restore();
    done();
  });
});
```
