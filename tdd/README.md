# TDD (Test-driven development) 測試驅動開發
  TDD 是一種程式開發的技巧，簡單來說就是先寫測試程式，然後才實作功能，藉由先定義規格，在尚未實作前就能知道開發方向是否正確，實作完成後能讓下一個開發者藉由測試快速得知輸入和輸出結果。

  ![TDD lift circle](http://www.agilenutshell.com/assets/test-driven-development/tdd-circle-of-life.png)

  剛開始寫測試時會先定義 function 的輸入輸出，一開始測試會 Test fail，實作 function 後能讓測試能順利通過，實作完成為了增加程式碼的可讀性、重用性、效能等等因素重構，導致 Test fail 直至重構完成，測試能快速驗證重構後的結果，不會導致其他狀況發生，形成 TDD 的正向循環。

## TDD 的優點
* 寫測試就是寫文件，有輸入輸出
* 程式完成後不怕重構
* 快速驗證 function 正確性
* 多人有效並無障礙的溝通

## 一個完整的測試
* 準備環境
* 準備資料
* 定義輸入
* 執行 function
* 驗證輸出  

## [Mocha](https://mochajs.org/) 測試框架

```javascript
describe('要測試的項目描述', (done) => {
  describe('項目 1', (done) => {

    it('項目 1-1', (done) => {
      try {
        // ...
        done()
      } catch (e) {
        done(e)
      }
    });
  });
  describe('項目 2', () => {
    beforeEach((done) => {
      // 個小項開始前，都會執行這裡
      done()
    });
    afterEach((done) => {
       // 每個小項執行完成後，都會執行這裡
       done()
    });
    it('項目 2-1', (done) => {
      // ...
      done()
    });

    it('項目 2-2', (done) => {
      // ...
      done()
    });
  });
});
```


#### 使用 Mocha 範例
```javascript
// 這一個大項目的測試名稱
describe('測試設定時間', () => {

  // 準備環境，new 一個 Date 物件
  let today = null;
  beforeEach(async (done) => {
    try {
      today = new Date();
      done()
    } catch (e) {
      done(e)
    }
  });

  // 這項目中的一項小測試
  it('設定日期', async (done) => {
    try {
      // 準備資料，我們會把日期設定為 1 號
      let newDate = 1;

      // 定義輸入，setDate 要給予一個數字的參數
      // 執行 function
      today.setDate(newDate);

      // 驗證輸出
      let check = today.getDate();
      check.should.be.eq(newDate);
      done()
    } catch (e) {
      done(e)
    }
  });

  afterEach(async (done) => {
    // 測試完成後把 today 清空，以便下次測試
    today = null;
    done();
  })

});
```

#### 單獨測試
```javascript
it.only('單獨測試', async (done) => done());
```

#### 略過測試
```javascript
it.skip('略過測試', async (done) => done());
```

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
